接著要觀察主要程式邏輯的內容囉。打開 「src/com/demo/android/bmi」 目錄下的 「Bmi.java」檔案，Eclipse+Android 開發工具已經幫我們預先建立好了基本的程式邏輯。其預設的內容如下：

```
1  package com.demo.android.bmi;
2
3  import android.app.Activity;
4  import android.os.Bundle;
5
6  public class Bmi extends Activity {
7      /** Called when the activity is first created. */
8      @Override
9      public void onCreate(Bundle savedInstanceState) {
10         super.onCreate(savedInstanceState);
11         setContentView(R.layout.main);
12     }
13 }
```

# 講解 #

比起什麼標籤都對稱的 XML 介面描述檔來說，這個以 Java 程式語言寫成的檔案雖然篇幅短，但反而要難讀得多。

我們將程式直接拆開，分成幾個部份來講解這個「Bmi.java」 檔案的內容：

第 1 行:
```
package com.demo.android.bmi;
```
這一行的作用是指出這個檔案所在的名稱空間。「package」(套件)是其關鍵字。使用名稱空間的原因是程式一旦擴展到某個大小，程式中的變數名稱、方法名稱、類別名稱難免重複，
這時就可以將定義的名稱區隔管理在 package 下，以避免相互衝突的情形發生。Java 的 package 設計成與檔案系統結構相對應，如我們的 package 設定是 「package com.demo.android.bmi」，則這個類別就該在指定目錄的「com/demo/android/bmi」路徑下可以找到。

同時也別忘了 Java 程式語言每段敘述語句的結尾處，與大部分的程式語言一樣需加上一個分號「;」，以表示一行程式敘述的結束。

第 3,4  行:
```
import android.app.Activity;
import android.os.Bundle;
```
程式中預設導入了 「android.app.Activity」跟「android.os.Bundle」兩個 Package，在所有的 Android 應用程式中都會用到這兩個 Package。「import」(導入)是用作導入 Package 的關鍵字。在 Java 語言中，使用到任何 API 前都要事先導入相對應的 Package。我們馬上將學到這兩個 Package 的用途。

Android 支援的 Package 與標準的 Java(j2se) 不盡相同。在寫 Android 應用程式時，你偶而可能需要參考可用的 API 列表，以確認使用到的 Package 是否有內建支援。後續章節中也將講解如何透過新增「jar」檔來呼叫額外的 Package。

完整的 API 可查閱官方的 package 列表：
http://code.google.com/android/reference/packages.html

第 6,13  行:
```
public class Bmi extends Activity {
}
```

第6行開始了程式的主體。其組成是這樣的：
```
public class Bmi
```

「Bmi」是這個類別的名稱。「class」則是用作宣告類別關鍵字。「public」關鍵字是用來修飾「Bmi」這個類別。表示「Bmi」是個「公開」的類別，可以從 package 外部取用。

「public class Bmi」後面再加上「extends Activity」敘述，則表示 「Bmi」 這個類別的功能、型別等全繼承自「Activity」類別。「extends」是繼承(Inherit)類別的關鍵字。「Activity」是來自於我們在第3行剛導入的Package。

因此整句話的含意即：「宣告一個公開的 Bmi 類別。這個 Bmi 類別繼承了程式開頭導入的 Activity 類別」。

「{}」大括號規範了一個程式區塊。大括號中的程式表達的這個程式區塊的主要內容。

第 7 行:
```
    /** Called when the activity is first created. */
```
第 7 行提供了位於其下的函式的註釋。`「/*  */」` 是 Java 語言的多行註解符號，位於其中的文字內容不會被編譯。`「/*」`敘述後多出來的一個`「*」`號被視為內文。順便提醒一下，Java 程式語言中兩個斜線「//」表示的是單行註解符號。單行註解符號「//」與多行註解符號`「/*  */」`不同的地方是，只有與「//」符號同行的文字才不會被編譯。

第 8-9, 12 行:
```
@Override
public void onCreate(Bundle savedInstanceState) {
}
```

第9行開始了這個方法(Method)的主體。其組成是這樣的：
```
public void onCreate(Bundle savedInstanceState) {
}
```

「onCreate」是這個方法的名稱。「void」則是宣告了這個方法的回傳值的型別(type)。「public」關鍵字是用來修飾「onCreate」這個方法。表示「onCreate」是個「公開」的方法，可以由 bmi 類別外部取用。

方法的回傳值的型別，即是這個方法的型別。「onCreate」這個方法使用「void」型別，表示「onCreate」這個方法不需回傳值。

同時，這個方法傳入了一個名為「savedInstanceState」的「Bundle」型別參數，「Bundle」型別正是來自我們前面所導入的 Package 之一。我們並不需要知道太多「Bundle」型別或「savedInstanceState」實體的細節，只要知道「Bundle」的內容與手機平台的記憶體管理有關。

當 Android 應用程式啟動、換到背景等待、關閉時，都會用到 「savedInstanceState」 這個實體來處理記憶體相關的事宜。當然，你也可以用其他名稱來代替它。還好「onCreate」這個方法永遠都是傳入「Bundle savedInstanceState」這個參數，寫應用程式時只要正確照規定傳入即可，你可以不用太去在意它。

> 給對 Bundle 是什麼有興趣的讀者：

> 「Bundle」可以保存程式上一次關閉（凍結）時的狀態。你可以透過覆寫 onFreeze 方法(與 onCreate 方法的作用類似) 來保存凍結前的狀態。
> 當程式啟動（Activity 重新初始化）時，會再次呼叫 onCreate 方法，你就能從 savedInstanceState 中得到前一次凍結的狀態。我們也可以透過「Bundle」來將這個 Activity 的內容傳到下一個 Activity 中。
> 之後講 Activity 時，也會講解 onCreate/onFreeze 等方法的關係。


「{}」大括號規範了一個程式區塊。大括號中的程式表達 onCreate 這個程式區塊的主要內容。
```
@Override
public void onCreate(Bundle savedInstanceState)
```

從前面的講解中，我們學到了在任何一個 Android 專案目錄裡，只要打開「Referenced Libraries」 目錄的「android.app」 分類，都可以找到 「Activity.class」這個類別。現在我們再深入一些查看「Activity.class」 類別。你要做的，只是依照圖示，找到 Android 工具中的「Referenced Libraries」 目錄，從「android.app」 分類裡找到「Activity.class」類別，並按下「Activity.class」 類別左側的三角形圖示，如此即可展開這個類別的屬性/方法列表。

我們在Activity類別的屬性/方法列表中，發現了現在正要講解的 onCreate 方法(Method)。

因為「bmi」 類別繼承自 Activity 類別，所以預設「bmi」 類別中其實已經有「onCreate」方法了。

事實上，「onCreate」 方法正是每個 Activity 類別初始化時都會去呼叫的方法。「@」開頭的語句表示裝飾子(decorator)語句，「@Override」語句的作用是告訴程式我們要覆寫這個「onCreate」方法。當我們打開程式時，程式不再使用從「bmi」 類別中繼承來的「onCreate」方法，而是使用我們在程式中自訂的行為。
```
@Override
public void onCreate(Bundle savedInstanceState) {
}
```
我們講解了整段程式，其含意是「覆寫 bmi 類別中公開的 onCreate 方法。這個 「onCreate」 方法無回傳值型別，而且這個方法傳入了一個名為 「savedInstanceState」 的 Bundle 型別參數。
現在來看看「onCreate」方法中包含的程式內容。

第 10, 11 行:
```
super.onCreate(savedInstanceState);
```
「super」是關鍵字。代表著這個 「Bmi」 類別的上層類別(Activity)。「super.onCreate(savedInstanceState);」的意思就是：「執行 Activity 類別中 onCreate 方法的內容」。這麼做的目的是什麼呢？

Google Android 將其應用程式的介面稱為視圖(View)，而負責控制各種動作行為的程式主體(Controller)，則稱為活動(Activity)。因此一個 Android 應用程式，必定會對應到一個以上的 Activity。 「onCreate」 方法則是每個 Activity 類別初始化時都會去呼叫的方法。我們想做的事，是保持原本「onCreate」 方法預設的動作，然後在其中加入我們想要的內容。

而 Android 產生的程式預設卻覆載(@Override)了「Bmi」 類別的「onCreate」 方法。原本繼承自 「Activity」類別的「onCreate」方法，其原本內容都被覆載掉了。因此想將原本的「onCreate」方法內容保留，並在其中加入我們的內容的話，就要使用「super」語句。當程式運行到我們覆寫的「onCreate」 方法時，透過「super.onCreate(savedInstanceState);」語句，會先將原本「Activity」類別中的「onCreate」方法執行一次，然後再執行我們覆寫的「onCreate」方法裡面其他的程式內容。

我們要執行原本的「onCreate」 方法時，仍然需要提供原本「onCreate」方法所需的傳入參數。因此「super.onCreate(savedInstanceState);」語句中，我們將「savedInstanceState」這個參數傳入原本的「onCreate」函式中。「savedInstanceState」是我們在「public void onCreate(Bundle savedInstanceState)」語句中所宣告的傳入參數。

```
setContentView(R.layout.main);
```
透過螢幕顯示的各種元素是按照介面層次結構來描述的。要將一個顯示元素的層次結構轉換顯示到一個螢幕上，Activity 會呼叫它用來設定 View 的 「setContentView」 方法，並傳入想引用的 XML 描述文件。當 Activity 被啟動並需要顯示到螢幕上時，系統會通知 Activity，並根據引用的 XML 文件敘述來描繪出使用者介面。上一章中我們定義好的 res/layout/main.xml 描述檔，就是透過這個機制繪出到螢幕上。

setContentView 方法也可以在 Activity 類別中找到。

你可能也注意到 「setContentView」 方法確實是透過 「R.layout.main」來引用 XML 文件描述檔的資源，而不是直接透過 res 目錄來引用。

< [存取識別符號](XmlR.md) | [回目錄](DiveIntoAndroid.md) | [完成 BMI 程式](BmiLogic.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！