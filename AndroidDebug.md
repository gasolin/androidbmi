記錄與偵錯可以分成「在程式中加上除錯訊息」，與「在偵錯環境中查看除錯訊息」兩部分。


# 在程式中加上除錯訊息 #

程式幾乎行行都可以出錯。要看程式中的哪一部分可能會出錯，實在是門很深的學問。要是沒有線索，光靠我們的腦袋來追蹤判斷，或是靠直覺東試試、西改改，這種作法就跟使用巫毒術扎娃娃一樣，直到被扎的人哪天身體疼了，就算巫毒作法有效。這樣實在不是一種好的除錯方式。

如果是程式碼語法格式上的問題，我們可以在編譯前，就透過開發工具提供的預先編譯警示，得到提醒並及早改正。在我們改正好這些語法格式上的問題後，開發工具才允許我們實際編譯應用程式。接著，才能將編譯好的應用程式上傳至模擬器，再開始進一步的測試。

除了程式碼語法格式上的問題，絕大部分會造成大麻煩的，是隱藏在程式邏輯中的問題。這些問題只有在模擬器甚至在實際機器上運行時才會出現。為了解決這些問題，我們需要一些協助工具。在 Android 平台上，我們可以透過「Log」函式，來達到自行在程式碼中加入一個個自訂的「記錄點」或「檢查點」。並可以透過開發環境中的「LogCat」工具來查看記錄。當程式流程每次運作到「記錄點」時，相應的「記錄點」就會在開發工具記錄中輸出一筆偵錯用的訊息。開發者透過這份記錄，來檢查程式執行的過程、使用到的參數，是否與我們期望的結果符合。並依此來辨別程式碼中可能出錯的區域，好能對症根治造成問題的程式碼。

## 導入 Log 函式 ##

打開「src/com/demo/android/bmi/Bmi.java」檔案，我們在程式中加入一些除錯訊息。一段含有記錄點(Log)的程式碼片段如下

```
import android.util.Log
....
public class Bmi extends Activity {
    private static final String TAG = "Bmi";
....
Log.d(TAG, "find Views");
Log.d(TAG, "set Listensers");
```

## 講解 ##

就像許多人在學生時代k書時，會在課本上使用不同顏色作記號。用不同顏色的色筆，來代表各段課文不同的重要性或是意義。「Log」函式的作用，就像是色筆一樣，協助我們在程式碼中「作記號」，這些數位記號，會在稍後就介紹到的「LogCat」工具中顯示。

Log 的使用格式如下

```
Log.代號(標籤, 訊息);
```

### 代號 ###

依據訊息的類型，我們有五種 Log 訊息形式可以用作記錄。

  1. Log.v (VERBOSE) 詳細訊息
  1. Log.d (DEBUG) 除錯訊息
  1. Log.i (INFO) 通知訊息
  1. Log.w (WARN) 警告訊息
  1. Log.e (ERROR) 錯誤訊息

一般較常用的是 Log.d(除錯訊息) 、Log.w (警告訊息)，和 Log.e (錯誤訊息)。範例中多使用 Log.d(除錯訊息) 。

### 標籤 ###

```
private static final String TAG = "Bmi";
....
Log.d(TAG, "find Views");
```

Log.(v,d,i,w,e) 的第一個參數，是一個自定的記錄標籤。在目前的 BMI 應用程式範例中，我們還看不太出來自定記錄標籤的意義。但是當程式的功能一擴張的時候（例如像在 AppDemos 範例那樣，包含各種不同功能），我們可以為不同的功能，給予不同的紀錄標籤。

### 訊息 ###

```
Log.d(TAG, "find Views");
```

在 Log.(v,d,i,w,e) 的第二個參數中，加入我們想要記錄的資訊。

## 實際應用 ##

在 BMI 應用程式中，我們可以在用來處理輸入錯誤的「try...catch」語句中加入「Log」訊息，好讓我們得以從記錄資料中，追蹤到輸入錯誤的情況。

```
public class Bmi extends Activity {
    private static final String TAG = "Bmi";
....
    catch(Exception err)
    {
        Log.e(TAG, "error: " + err.toString());
        Toast.makeText(Bmi.this, getString(R.string.input_error), Toast.LENGTH_SHORT).show();
    }
```

### 講解 ###

```
catch(Exception err)
    Log.e(TAG, "error: " + err.toString());
    ....
}
```

「Log.e..」敘述的意思是：根據「catch」到的例外型別的資訊(Exception err)，將資料印出到記錄中。

### 其他的記錄標籤方式 ###

我們也不是一定得為每個 TAG 事先定義好一個記錄標籤，我們可以用當前的 Activity 名稱來做為記錄標籤：

```
Log.e(this.toString(), "error: " + err.toString());
```

### 延伸運用 ###

在實作錯誤訊息提示前，我們其實可以使用 Log.e 函式，來先將錯誤訊息記錄起來，等到整個程式大致底定了，再來用 Toast 或 AlertDialog 元件，來實作輸入錯誤提示的功能。


# 在偵錯環境中查看除錯訊息 #

在程式中加上除錯訊息後，我們可以使用除錯模式 (Debug Mode) 運行模擬器，並透過開發工具來查看除錯訊息。

```
偵錯工具的正式名稱為 Dalvik Debug Monitor Service (DDMS)。
```

## 啟動模擬器 ##

使用除錯模式 (Debug Mode) 運行模擬器（選單列->Run->Debug History->BMI）。

## 切換到偵錯環境配置 ##

點選開發環境右上角的 "Open Perspective"按鈕，選擇 "Other..."選項。選擇後會彈出一個「Open Perspective」（開啟環境配置）對話框。對話框中列出了所有可用的環境配置列表，選擇 "Debug"。此時，右上角的環境配置圖示列中，會多出一個「Debug」環境配置圖示。整個開發工具的介面配置也為之一變。在右上角的環境配置圖示列中，點選「Java」環境配置圖示，就會回到我們原來的介面配置。

現在先切換到「Debug」環境配置，可以看到右下角的「LogCat」視窗。其上有五個醒目的 V、D、I、W、E 圖示，分別代表著五種 Log 形式(Verbose, Debug, Info, Warn, Error)，還有一個綠色的「+」號，與一個紅色的「-」號。

模擬器運行時會產生很多的訊息記錄(Log)，一不注意就看到眼花了。這時候，我們自訂的記錄標籤（範例中自訂的標籤是「Bmi」）就派上了用場，正好可以為 LogCat 加上一個過濾器(Log Filter)，只顯示與「Bmi」標籤相關的訊息記錄。

### 加入訊息記錄過濾器(Log Filter) ###

在「LogCat」視窗右側，按下綠色的「+」號，會彈出一個「Log Filter」視窗。在「Log Filter」視窗的「by Log Tag」欄位中填入「Bmi」，並填入任意的「Filter Name」後，按下「ok」按鈕。「LogCat」視窗上會多出一個與我們填入的「Filter Name」相同的標籤。裡面的內容，即所有標示為「Bmi」的自訂訊息記錄。

# 參考資料 #

  * ddms http://code.google.com/android/reference/ddms.html
  * debug http://code.google.com/android/intro/tutorial-extra-credit.html
  * trace view http://code.google.com/android/reference/traceview.html

< [傳送資料到新 Activity](AndroidIntent.md) | [回目錄](DiveIntoAndroid.md) | [活動的生命週期](LifeCycle.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！