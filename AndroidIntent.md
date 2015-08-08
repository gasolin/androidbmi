
```
Intent 是一個動作與內容的集合。Intent 像是一串網址，傳送到系統並意圖靠其他 Activity 來處理網址中所指定的動作跟內容。
```

前一章中，我們已學過獨立的 Activity。Android 使用 Intent 來完成在螢幕間切換的動作。Intent 包含 Activity 間切換所需的動作、分類、傳送資料等訊息，就像是 Activity 之間的宅急便一樣。

因此當我們得在 Activity 之間交換資料時，需要先了解 Intent 的用法。

Intent 可以分為兩種類型：「現成的 Intent」與「自訂的 Intent」。使用現成的 Intent 的例子，可以參考「[初見 Intent](AndroidUrl.md)」一章。在 Android 清單中作設定時，我們還可以使用 IntentFilter，來過濾和找尋對應的 Intent。而一般開發者在程式中所自行撰寫的 Intent，則是透過自訂 Intent 來做很多事情。比如切換 Activity、在其間傳遞各式的資料。

要完成在 Activity 之間透過 Intent 傳送資訊的動作，可以分成「傳遞資訊」與「接收資訊」兩部分。

## 使用 Intent 傳遞資訊 ##

上一章的範例中，我們新增了一個 Report Activity 頁面，但是還沒有為新頁面填入實值內容。在本章中我們會完成將 BMI 應用程式從一個頁面改寫成為兩個頁面：「輸入頁面」(原本的 Bmi Activity)，與「結果頁面」(Report Activity)的應用程式。「輸入頁面」從介面上取得身高、體重值，透過傳送 Intent，將值攜帶到「結果頁面」。「結果頁面」從 Intent 中取出其攜帶的身高、體重值，用這兩個參數來產生 BMI 報告結果。

打開 「src/com/demo/android/bmi/Bmi.java」，修改「Button.OnClickListener」 函式：

```
1    private Button.OnClickListener calcBMI = new Button.OnClickListener()
2    {
3    	  public void onClick(View v)
4    	  {	
5    		  //Switch to report page
6    		  Intent intent = new Intent();
7            intent.setClass(Bmi.this, Report.class);
8            Bundle bundle = new Bundle();
9            bundle.putString("KEY_HEIGHT", field_height.getText().toString());
10          bundle.putString("KEY_WEIGHT", field_weight.getText().toString());
11          intent.putExtras(bundle);
12          startActivity(intent);
13      }
14  };
```

### 講解 ###

```
Intent intent = new Intent();
intent.setClass(Bmi.this, Report.class);
...
startActivity(intent);
```

是的，如果你真的有學懂上一章的內容，那麼你可能會發現：我們準備講解的這段程式碼主體，與上一章中所提到的程式碼其實一模一樣。這段程式碼的作用是透過 Intent 通知系統(Android 框架)：我們將要從 Bmi Activity 這個頁面（輸入頁面）前往 Report Activity 頁面（結果頁面）。如果把我們多加的用來附加資料的程式碼拿掉，這段程式碼即原來獨立的 Activity 的程式碼。

```
Bundle bundle = new Bundle();
...
intent.putExtras(bundle);
```

相依的 Activity 與獨立的 Activity 不同之處，就在於相依的 Activity 會附帶傳送額外資訊到新的 Activity。這些額外資訊都是靠著 Intent 物件來攜帶的。

傳送 intent 時，我們可以在其上附加一些訊息，比如說本例中我們從輸入介面中取出了的身高、體重值，要將身高、體重值傳送給 Report Activity 後作計算。這些附加在 Intent 上的訊息都儲存在 Bundle 物件中。透過「intent.putExtras(bundle)」敘述，我們將「bundle」 物件附加在 Intent 上，隨著 Intent 送出而送出。

```
bundle.putString("KEY_HEIGHT", field_height.getText().toString());
bundle.putString("KEY_WEIGHT", field_weight.getText().toString());
```

這段程式是實際用來附加資料的程式碼。將使用者輸入的身高、體重值，儲存到 bundle 物件中。
Bundle 其實是一種特別定義的映射（map）型別。「KEY\_HEIGHT」、「KEY\_WEIGHT」是我們為儲存在 bundle 物件中的身高、體重值，所指定的「識別符號」。在這邊，我們直接把身高、體重值都儲存成字串。因為整個程式都是我們控制，到時候在接收的 Activity 一端，再透過「KEY\_HEIGHT」、「KEY\_WEIGHT」這兩個「識別符號」來取得實際的身高、體重值。讀出的值也是字串，等值讀出來以後，再去做型別轉換就好了。當然你也可以直接把身高、體重值存成數字。

Bundle 型別額外提供了很多 API。在傳送 Intent 時，使用 Bundle 型別的物件來攜帶資料，相當方便。

## 使用 Intent 接收資訊 ##

在使用 Intent 接收資訊前，我們先來加上「Report」這個 Activity 的介面。

### 相關工作 ###

打開「res/values/report.xml」檔案，修改如下：
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    <string name="report_title">BMI 報告</string>
    <string name="report_back">前一頁</string>
</resources>
```

打開「res/layout/report.xml」檔案，修改如下：
```
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
	android:orientation="vertical"
	android:layout_width="fill_parent"
	android:layout_height="fill_parent"
	>
	 <TextView android:id="@+id/result" 
	    android:layout_width="fill_parent" 
	    android:layout_height="wrap_content" 
	    android:text=""
	    />
	 <TextView android:id="@+id/suggest" 
	    android:layout_width="fill_parent" 
	    android:layout_height="wrap_content" 
	    android:text=""
	    />
	<Button android:id="@+id/report_back" 
            android:layout_width="wrap_content" 
            android:layout_height="wrap_content" 
            android:text="@string/report_back"
            />
</LinearLayout>
```

這時打開 Eclipse 開發環境的 layout 檢視，或是執行模擬器，我們可以看到一個「前一頁」按鈕，按鈕前其實還有兩個沒有內容的 TextView 介面元件，下一節中我們將在「Report」這個 Activity 中取得從「Bmi」Activity 傳過來的身高體重資料，根據這些資料產生報告資訊。

### 在 Activity 中解開資訊 ###

用作接收 Intent，透過 Intent 攜帶的資訊來計算出 BMI 值的「src/com/demo/android/bmi/Report.java」完整程式碼如下：

```
1  package com.demo.android.bmi;
2
3  import java.text.DecimalFormat;
4  import android.app.Activity;
5  import android.os.Bundle;
6  import android.view.View;
7  import android.widget.Button;
8  import android.widget.TextView;
9
10 public class Report extends Activity {
11	 /** Called when the activity is first created. */
12 @Override
13	 public void onCreate(Bundle savedInstanceState) {
14		 super.onCreate(savedInstanceState);
15		 setContentView(R.layout.report);
16		 findViews();
17		 showResults();
18		 setListensers();
19 }
20
21	 private Button button_back;
22 private TextView view_result;
23 private TextView view_suggest;
24
25 private void findViews()
26 {
27     button_back = (Button) findViewById(R.id.report_back);
28    	 view_result = (TextView) findViewById(R.id.result);
29    	 view_suggest = (TextView) findViewById(R.id.suggest);
30 }
31
32 //Listen for button clicks
33 private void setListensers() {
34    	 button_back.setOnClickListener(backMain);
35 }
36    
37 private Button.OnClickListener backMain = new Button.OnClickListener()
38 {
39     public void onClick(View v)
40     {
41        // Close this Activity
42        Report.this.finish();              
43     }
44 };
45
46 private void showResults() {
47     DecimalFormat nf = new DecimalFormat("0.00");
48
49     Bundle bundle = this.getIntent().getExtras();
50    	double height = Double.parseDouble(bundle.getString("KEY_HEIGHT"))/100;
51    	double weight = Double.parseDouble(bundle.getString("KEY_WEIGHT"));
52     double BMI = weight / (height * height);
53     view_result.setText(getString(R.string.bmi_result) +nf.format(BMI));
54        
55     //Give health advice
56     if(BMI>25){
57         view_suggest.setText(R.string.advice_heavy);
58     }else if(BMI<20){
59         view_suggest.setText(R.string.advice_light);
60     }else{
61         view_suggest.setText(R.string.advice_average);
62     }
63
64   }
65 }
```

### 講解 ###

整個程式的架構我們在「[完成 BMI 程式](BmiLogic.md)」與「[重構程式](BmiRefactor.md)」兩章中已經詳細說明過了。

```
Bundle bundle = this.getIntent().getExtras();
```
當我們透過 Intent 傳到新的 Activity 後，只要使用 Activity.getIntent() 函數，就可以得到傳來的 Intent 物件。然後使用「getExtras」函式，就能取得附加在 Intent 上的 bundle 物件。

```
		double height = Double.parseDouble(bundle.getString("KEY_HEIGHT"))/100;
		double weight = Double.parseDouble(bundle.getString("KEY_WEIGHT"));
```

在當前的 Activity 取得了 bundle 物件後，我們可以透過指定儲存在 bundle 物件中的身高、體重值的識別符號「KEY\_HEIGHT」、「KEY\_WEIGHT」來取出身高、體重值的資料。由於我們傳參數值來時，所使用的是是字串格式，所以我們在此得做個型別轉換，將參數從字串轉換成雙倍精度浮點數(Double)型別。


```
    private Button.OnClickListener backMain = new Button.OnClickListener()
    {
        public void onClick(View v)
        {
           // Close this Activity
           Report.this.finish();              
        }
    };
```

當按下 backMain 按鈕元件後，結束 Report Activity，顯示出原本的 Bmi Activity。


## 不透過 Bundle 交換資訊 ##

使用 Intent 傳遞資訊時，我們看到可以用「setClass」方法來指定要傳送到的 Activity。我們也可以使用類似的「setString」、「setInt」方法來指定要透過 Intent 附帶傳送的參數。

在使用 Intent 接收資訊時，我們再使用「this.getIntent().getData()」方法就能取到參數了。「getData」方法取到的參數一般是字串型態的。
若事先已經知道傳來參數的型別，還可以用比「getData」方法更精確的「getString」、「getInt」等方法來取得參數值。

不過既然有好用的 Bundle 類別可用，為什麼要自己把事情弄得複雜呢？


< [加入新 Activity](AndroidActivity.md)  | [回目錄](DiveIntoAndroid.md) | [記錄與偵錯](AndroidDebug.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！