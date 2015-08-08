直觀來看，每個 Activity 通常會負責處理一個螢幕的內容(包含介面、選單、彈出對話框、程式動作等)。當我們需要從一個螢幕畫面切換到另一個螢幕畫面的時候，就涉及到了 Activity 切換的動作。
我們可以將 Activity 看成 MVC 模式中的 Control。Activity 負責管理 UI（詳細的UI細節可以由資源檔讀入），並接受事件觸發。

以是否需要與其他 Activity 交換資料來區分，Activity 可以粗分為兩種類型：「獨立的 Activity」與「相依的 Activity」。不同類型的 Activity，其動作也不盡相同：

### 獨立的 Activity ###

獨立的 Activity 是不需要從其他地方取得資料的 Activity。只是單純的從一個螢幕跳到下個螢幕，不涉及資料的交換。
從一個獨立的 Activity 呼叫另一個獨立的 Activity 時，我們只要填好 Intent 的內容和動作，使用 startActivity 函式呼叫，即可喚起獨立的 Activity。例如前幾章中，用作開啟特定網頁的 Activity。

### 相依的 Activity ###

相依的 Activity 是需要與其他 Activity 交換資料的一種 Activity。相依的 Activity 又可再分為單向與雙向。從一個螢幕跳到下個螢幕時，攜帶資料供下一個螢幕（Activity）使用，就是單向相依的 Activity; 要在兩個螢幕之間切換，螢幕上的資料會因另一個螢幕的操作而改變的，就是雙向相依的 Activity。
與獨立的 Activity 比起來，相依的 Activity 變化更加精采。

我們會在後續章節中，對相依的 Activity 做進一步的說明。

# 獨立的 Activity #

本章將繼續透過改進 BMI 應用程式來講解 Android 應用程式設計。在這個過程中，我們將使用到獨立的 Activity。

這章中所做的改動都是為了介紹獨立的 Activity，而不是為了讓 BMI 程式變得更完整。因此你不妨先將寫好的 BMI 程式先壓縮備份到其他目錄中，再隨著後面的教學繼續探索 Android。

本章的目的是介紹獨立的 Activity，會用到兩個螢幕，因此除了原本的一個 XML 描述檔與一個程式碼檔案之外，我們還會額外再定義一個 XML 描述檔與一個程式碼檔案，以支援第二個螢幕的動作。

要完成獨立的 Activity 的動作，我們要做幾件事：

  1. 在程式碼中建立新 Activity 類別檔案
  1. 在清單中新增 Activity 描述
  1. 在原 Activity 類別中加入 startActivity 函式

## 程式碼中建立新的 Activity 類別檔案 ##

首先，使用 Navigator 檔案瀏覽視窗，切換到「src/com/demo/android/bmi」資料夾。在「bmi」資料夾中，現存有 「Bmi.java」與「R.java」兩個檔案。我們準備在此建立一個新的 Activity 類別檔案。

在「bmi」資料夾圖示上按右鍵，選擇「New->Class」選項。 Eclipse 會跳出一個「New Java Class」對話框。

在對話框中的「Name」一欄上填入「Report」。「Report」的字頭需大寫，這是 Java 程式語言的默認規則。

在「Superclass」一欄右方，按下「Browse...」，Eclipse 會跳出「Superclass Selection」對話框。在對話框中的「Choose a type」欄位中輸入「activity」，輸入框下方的「Matching items」欄位中，會顯示出所有可能的類別。我們選擇「Activity - android.app - ...」這個選項，點擊右下方的「ok」按鈕，回到上一個對話框。

此時，「Superclass」欄位中將填入「android.app.Activity」訊息。按下對話框右下角的「Finish」鍵，Eclipse 會在「bmi」資料夾中，產生一個對應的「Report.java」檔案。

剛產生（尚未修改過的）的「Report.java」檔案如下：

```
1  package com.demo.android.bmi;
2
3  import android.app.Activity;
4
5  public class Report extends Activity {
6
7  }
```

在[解讀程式流程](AndroidLogic.md)一章中，我們已講解過 Android 程式碼的基本架構，即 XML 描述檔與程式碼兩個主要組成部分。稍後我們要處理建立新程式碼的相關工作，包含定義對應的 XML 描述檔，與在程式碼中，填入這個 class 的內涵。

### 相關工作 ###

在「res/layout」中新增一個「report.xml」檔案，並把[描述使用者介面](AndroidUI.md) 一章中講解過的 xml 檔案複製一份過來：

```
1  <?xml version="1.0" encoding="utf-8"?>
2  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
3  	    android:orientation="vertical"
4      android:layout_width="fill_parent"
5	    android:layout_height="fill_parent"
6	>
7	<TextView
8		android:layout_width="fill_parent"
9		android:layout_height="wrap_content"
10		android:text="Hello World, Bmi"
11 />
12 </LinearLayout>
```

打開「src/com/demo/android/bmi/Report.java」，把[解讀程式流程](AndroidLogic.md)一章中講解過的預設的程式碼複製進來：

```
1   package com.demo.android.bmi;
2
3   import android.app.Activity;
4   import android.os.Bundle;
5
6   public class Report extends Activity {
7	 /** Called when the activity is first created. */
8	 @Override
9	 public void onCreate(Bundle savedInstanceState) {
10		 super.onCreate(savedInstanceState);
11		 setContentView(R.layout.report);
12	 }
13 }
```

上面的程式碼中，我們將

```
setContentView(R.layout.main);
```

換成了：

```
setContentView(R.layout.report);
```

以對應我們新定義的 XML 描述檔產生的資源識別符號。

## 清單中新增 Activity 描述 ##

我們再打開「AndroidManifest.xml」檔案，並切換到「Application」分頁。在「Application」分頁的左下角，我們可以看到「Application Nodes」欄位中，列出目前已在「AndroidManifest.xml」檔案中定義的所有「Activity」。現在我們就來將 「Report」這個新的 Activity 加入到「AndroidManifest.xml」檔案中。

點擊「Application Nodes」欄位右側的「Add...」按鈕，彈出一個小對話框。
選擇「Activity」後，按下「ok」回到「Application」分頁。「Application Nodes」欄位中會增加一個「Activity」項目。選擇這個「Activity」項目後，在「Application Nodes」欄位右方會出現新的「Attributes for Activity」相關欄位。

我們點選 「Name**」欄位右側的 「Browse...」按鈕，開啟另一個對話框。新的對話框中我們可以選擇在程式中現有定義的 Activity。我們選擇「Report - com.demo.android.bmi」後，按 「ok」 鍵回到「Application」分頁。此時「Name**」欄位的內容變成了「Report」，「Application Nodes」欄位中的名稱也更新成「Report(Activity)」了。

### activity 標籤的內容 ###

我們從「Application」分頁切換到「AndroidManifest.xml」分頁，查看剛剛的動作實際上作了些什麼事。

我們發現，在原本的 activity 敘述下方，新增了一行名為「Report」的 activity 標籤，完整的「AndroidManifest.xml」清單內容如下：

```
1  <?xml version="1.0" encoding="utf-8"?>
2  <manifest xmlns:android="http://schemas.android.com/apk/res/android"
3      package="com.demo.android.bmi">
4     <application android:icon="@drawable/icon">
5         <activity android:name=".bmi" android:label="@string/app_name">
6            <intent-filter>
7               <action android:name="android.intent.action.MAIN" />
8                <category android:name="android.intent.category.LAUNCHER" />
9            </intent-filter>
10        </activity>
11      <activity android:name="Report"></activity>
12   </application>
13 </manifest>
```

### 手動新增 activity 標籤 ###
Android 提供了多種方式來協助我們定義「AndroidManifest.xml」清單檔案，除了使用對話框選擇的方式之外，你也可以在原本的「AndroidManifest.xml」檔案中直接修改原始碼，加入如下敘述：

```
<activity android:name="Report"></activity>
```

來得到相同的效果。

### 修改頁面標題文字 ###

如果希望在打開 Report Activity 頁面時，標題欄上的文字將會是「BMI 報告」，而不是預設跟 Activity 名稱相同的「Report」，我們可以在清單裡的「report activity」標籤中，加入標籤（label）屬性的描述。步驟如下。

1. 在「res/values/」目錄下，新建一個 report.xml 描述檔，存放 Report 活動頁面用到的字串。檔案內容如下：
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="report_title">BMI 報告</string>
</resources>
```

2. 有了描述檔後，我們可以再修改「AndroidManifest.xml」清單，為 Report activity 添加標籤(label)屬性：

```
<activity android:name="Report" android:label="@string/report_title"></activity>
```

## 原 Activity 類別中加入 startActivity 函式 ##

在準備好相關資源、並在「AndroidManifest.xml」清單添加新 activity 描述後，我們來到實際控制整個程式流程的程式碼部份。

在程式碼中，我們要把原本按下按鈕即開始計算，並顯示 Bmi 值到同一螢幕的按鈕動作，改成按下按鈕後跳轉到 「Report」 這個 Activity。

首先修改「BMI」這個 Activity。打開「src/com/demo/android/bmi/Bmi.java」檔案，修改「OnClickListener」函式(定義按下按鈕時做的動作)的內容。按下按鈕後從 Bmi Activity 切換（跳轉）到 Report Activity 的程式片段如下：

```
1   private Button.OnClickListener calcBMI = new Button.OnClickListener()
2   {
3      public void onClick(View v)
4      {
5          //Switch to report page
6          Intent intent = new Intent();
7          intent.setClass(Bmi.this, Report.class);
8          startActivity(intent);
9       }
10 };
```

修改好後，開啟 Android 模擬器。當我們按下「計算 BMi 值」按鈕後，螢幕會切換到「Hello World, Bmi」頁面(已經進入了 Report Activity)。在這個頁面上，我們並沒有辦法可以直接回到前一個頁面，因為這兩個頁面都是獨立的 Activity。但我們還是可以透過按下硬體的「Undo」鍵，使螢幕切換回原本輸入身高體重的頁面 (即回到 Bmi Activity)。

### 講解 ###

```
Intent intent = new Intent();
```

我們建立一個新的「意圖」(Intent) 實體。

```
intent.setClass(Bmi.this, Report.class);
```

為這個意圖指定來源的 Activity 所在 class，與要前往的 Activity 所在的 class。

```
startActivity(intent);
```

將定義好的 intent 傳入「startActivity」函式中。「startActivity」函式會將 intent 傳入 Android 框架，Android 框架會根據各應用程式在系統中註冊的資料(有沒有聯想到我們剛剛為 Report Activity 增加的 activity 清單描述?)，找出 Report 這個 Activity，並呼叫它。

搞懂之後，原來呼叫一個獨立的 Activity，所需的功夫其實很單純呀。


< [定義 Android 清單](AndroidManifest.md) | [回目錄](DiveIntoAndroid.md) | [傳送資料到新 Activity](AndroidIntent.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！