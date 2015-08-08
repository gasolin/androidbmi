
```
將一份創意落實到可執行的應用程式，背後需要的是從閱讀與寫作程式碼中累積的經驗，並有堅持理念、直到完成的耐心。
```

# 表達使用者介面 #

我們可以先用前幾章教的方法設定並執行模擬器，看看模擬器運作後的結果。

我們看到一個文字欄位，上面有一串文字 「Hello World, Bmi!」。這就是 Android 預設程式架構的範例囉。

由於才剛開始實際接觸到 Android 應用程式，我們先從簡單的開始：這一節中，我們的目標是將 「Hello World, Bmi!」 換成別的文字。

那麼，「Hello World, Bmi!」，這串字串藏在哪裡呢？

先打開 「res/layout/main.xml」
```
    1  <?xml version="1.0" encoding="utf-8"?>
    2  <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    3     android:orientation="vertical"
    4     android:layout_width="fill_parent"
    5     android:layout_height="fill_parent"
    6     >
    7      <TextView 
    8          android:layout_width="fill_parent"
    9          android:layout_height="wrap_content"
    10        android:text="＠string/hello"
    11        />
    12 </LinearLayout>
```

原來「Hello World, Bmi!」字串就藏在「res/layout/main.xml」這個檔案的第 10 行中。我們只要簡單地將第 10 行修改成如下
```
android:text="Hello World, Bmi!”
```

再執行一次模擬器，就可以得到一個相似的應用程式，只是內文變成了我們剛剛修改的內容。

既然找到了「Hello World, Bmi!」字串，我們就試著將「android:text」屬性值從「Hello World, Bmi!」改成「哈囉，BMI」，然後執行看看吧。
```
android:text="哈囉，BMI"
```
結果發現 Android 模擬器中文嘛也通，字型也相當漂亮。

要開始學習 Android 應用程式確實很簡單吧？不過為了顯示「Hello World, Bmi」，也用到了許多程式碼。到底這些程式碼有什麼含意呢？

我們馬上來學習 「main.xml」這個 XML 介面描述檔的內涵吧。

Android 平台裡，使用者介面都是透過 ViewGroup 或 View 類別來顯示。ViewGroup 和 View 是 Android 平台上最基本的使用者介面表達單元。我們可以透過程式直接呼叫的方法，調用描繪使用者介面，將螢幕上顯示的介面元素，與構成應用程式主體的程式邏輯，混合在一起編寫。或是，也可以將介面顯示與程式邏輯分離，照著 Android 提供的這個較優雅的方式，使用 XML 描述檔，來描述介面元件的組織。

# 講解 #

我們看到的「Hello World, Bmi」就包含在「main.xml」 這個檔案中。
接著，我們就直接分部份來講解這個「main.xml」 檔案裡的內容：

第 1 行
```
    <?xml version="1.0" encoding="utf-8"?>
```
XML (Extensible Markup Language) 是一種標記描述語言，不管是語法還是看起來的樣子，都相當類似網頁所使用的 HTML 標記語言。XML 被廣泛地運用在 Java 程式的設定中。「main.xml」 文件裡，第一行是每個 XML 描述檔固定的開頭內容，用來指示這個文字檔案是以 XML格式描述的。

第 2, 6 與 12 行
```
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"></LinearLayout>
```
接著我們看到第一個標籤，與 HTML 網頁標籤相當類似。
```
    <LinearLayout></LinearLayout>
```
"線性版面配置"(LinearLayout)標籤，使用了兩個「LinearLayout」標籤，來表示一個介面元件的區塊。後頭的標籤前加上一個「/」符號來表示結束標籤。"線性版面配置" 所指的是包含在 「LinearLayout」 標籤中，所有元件的配置方式，是將一個接一個元件由上而下排隊排下來的意思。
```
     xmlns:android="http://schemas.android.com/apk/res/android"
```
xmlns 開頭的這串敘述，是用來宣告這個 XML 描述檔案的的名稱空間(NameSpace)，後面接的URL(網址)，表示這個描述檔案會參照到 Android 名稱空間提供的定義。
所有 Android 版面配置檔案的最外層標籤中，都必須包含這個屬性。

注意標籤需要兩兩對稱。一個標籤「

&lt;LinearLayout&gt;

」在一串敘述的前頭，另一個標籤「

&lt;/LinearLayout&gt;

」在敘述的末尾。
如果你修改過的標籤沒有閉合(忘了加 <、/、> 等符號)，Eclipse 畫面上也會出現小小的警示符號來提醒你。

第 3-5 行
```
    android:orientation="vertical"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
```
這些包含在「

&lt;LinearLayout&gt;

」標籤中的敘述被稱為「LinearLayout」標籤的「屬性」。Android 應用程式在 layout 目錄中的標籤，大多數的屬性前都有一個「android:」前綴。同一個介面元件的屬性之間，是以空白做區隔，因此事實上你也能將多個屬性寫在同一行。當然，將屬性排成多行更易於閱讀。我們應該保持這個好習慣。

介面元件都有許多共同的屬性，例如介面元件的長，寬度設定屬性。Android 介面元件的寬度、長度設定屬性分別叫做「android:layout\_width」、「android:layout\_height」。兩個都設定為 「fill\_parent」參數值。「fill\_parent」 如其名，所表達的的意思就是"填滿整個上層元件"。預設 LinearLayout 介面元件就會佔滿整個螢幕空間。

介面元件彼此間也會有一些不同的屬性，例如 「LinearLayout」(線性版面配置) 標籤的「android:orientation」(版面走向) 屬性。在此填入 「vertical」 (垂直)屬性值，表示這個介面的版面配置方式是從上而下垂直地排列其內含的介面元件。

「android.view.ViewGroup」 是各種佈局配置(layout)元件的基礎類別。常見的實現有

LinearLayout(線性版面配置)、FrameLayout(框架版面配置)、TableLayout(表格版面配置)、AbsoluteLayout(絕對位置版面配置)、RelativeLayout(相對位置版面配置)等。

雖然有這麼多種版面配置方式可以選用，但大多數的應用程式並不需特地去改變預設的 LinearLayout 的配置，只要專注在其中填入需要的介面元件即可。所以從第 7 行之後的內容才是一般應用程式開發時較常修改之處。

第 7 和 11 行
```
    <TextView
        />
```
TextView (文字檢視)是我們看到的第一個熟悉的介面元件。其作用是顯示文字到螢幕上。你可能注意到這個標籤結尾使用了 「/>」 符號。
「/>」符號表示這個XML敘述中沒有內文，亦即此介面元件描述中不再包含其他介面元件，也表示這個介面元件就是這個螢幕中最小的組成單元了。

第 8-10 行
```
    android:layout_width="fill_parent"
    android:layout_height="wrap_content"
    android:text="Hello World, bmi"
```
我們來看看 TextView 介面元件中包含了哪些屬性。

「android: layout\_width」和「android:layout\_height」我們剛剛已經學過了，分別代表寬度跟長度。「android: layout\_width」 的 「fill\_parent」 參數值表示寬度填滿整個上層介面元件(即 LinearLayout 介面元件)。「android:layout\_height」則是用上一個新的參數值「wrap\_content」(包住內容)，亦即隨著文字欄位行數的不同而改變這個介面元件的高度。最後的 「android:text」 屬性則是 TextView 介面元件的主要屬性，亦即文字欄位中顯示的文字內容。至於「@string/hello 」這段字串所代表的意義，馬上會接著在後面章節說明。我們現在已知道是：只要將「android:text」屬性內容替換成我們想要文字，在預覽畫面或在模擬器中就會顯示對應的文字。

將以上的 XML 描述綜合起來，我們就可以得知「main.xml」 想表達的介面。

< [建立新程式](ReadSource.md) | [回目錄](DiveIntoAndroid.md) | [設計使用者介面](BmiUI.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！