我們的程式主功能已經完成了，現在我們要試著讓它看起來更像一個完整的應用程式。

接下來的幾章，我們要為「BMI」應用程式加上一個選單。選單裡面有一個「關於..」選項。按下「關於...」選項後，會彈出一個對話框，裡面會顯示「BMI」程式的相關訊息。

本章中將先學習如何處理對話框。

在本章中，我們要產生一個應用程式中常見的「關於」頁面。
應用程式的「關於」頁面中，通常要包含版本訊息、作者、聯絡方式、首頁等資訊。

我們的「關於」頁面將以彈出對話框的方式表現。所需要做的，是撰寫負責處理對話框的「openOptionsDialog」函式，並將之附加在原本應用程式中「calcBMI」這個按鈕元件的「OnClickListener」方法上。當我們按下「計算 BMI 值」按鈕時，即彈出對話框。

等我們學會了對話框的寫法，在接下來學習 Android 選單的章節中，我們會改將對話框函式放入選單中。

對話框中所能顯示的內容千變萬化。對 Android 來說，對話框也是一種顯示內容(View)。與一般全頁面顯示的不同之處，在於對話框會重疊顯示到原本的呼叫頁面上，而且在對話框的主要顯示內容下方，可能還會再附加上幾個按鈕，用以回到原頁面，或是用來執行其他的動作。

要在 Android 程式中呼叫一個對話框，有二個主要步驟：

  1. 定義呼叫點
  1. 實作對話框

## 定義呼叫點 ##

修改「Bmi.java」

Bmi.java
```
1  private OnClickListener calcBMI = new OnClickListener()
2  {
3      public void onClick(View v)
4      {
.           ....
6           }else{
7               view_suggest.setText(R.string.advice_average);
8           }
9           openOptionsDialog(); 
```

我們在「calcBMI」函式的尾端加入一行「openOptionsDialog();」，用以在每次計算完BMI值並顯示建議後，順便呼叫「關於」對話框。

## 實作對話框 ##

緊接著「calcBMI」這個「OnClickListener」函式之後，我們實際開始撰寫對話框函式。

```
private void openOptionsDialog() {
    AlertDialog.Builder dialog = new AlertDialog.Builder(Bmi.this)
    dialog.setTitle("關於 Android BMI")
    dialog.setMessage("Android BMI Calc")
    dialog.show();
```

我們來分析這個對話框程式。

首先，顯示一個最基本的對話框所需的程式碼如下。

```
AlertDialog.Builder dialog = new AlertDialog.Builder(Bmi.this)
```

我們建立了一個 AlertDialog 對話框類別實體，AlertDialog 呼叫 Builder 方法來預備對應的介面元件。最後使用 show() 方法來將對話框顯示在螢幕上。

在「Builder」方法中傳入的「Bmi.this」指的是我們建立的「Bmi」這個Activity的實體。也可以這麼想，因為在onCreate的過程中，我們將main.xml介面描述檔繫結到了「Bmi」這個Activity，因此「Bmi.this」指的也是目前顯示的畫面。我們透過傳入「Bmi.this」，指定這個對話框將顯示在當前的畫面上。

透過
```
dialog.setTitle("關於 Android BMI")
```
我們設定了對話框的標題。

透過
```
dialog.setMessage("Android BMI Calc")
```
我們設定了對話框的主要內容。

## 重構 ##

我們把其中用到的字串抽取出來，整理到「res/values/strings.xml」中。

res/values/strings.xml
```
<?xml version="1.0" encoding="utf-8"?>
<resources>
    ....
    <string name="about_title">關於 Android BMI</string>
    <string name="about_msg">Android BMI Calc\n
    		作者 gasolin\n\n
    		gasolin+android [at] gmail.com</string>
    ....
</resources>
```

於是 openOptionsDialog 函式變成這樣：

```
private void openOptionsDialog() {
    AlertDialog.Builder dialog = new AlertDialog.Builder(Bmi.this)
    dialog.setTitle(R.string.about_title)
    dialog.setMessage(R.string.about_msg)
    dialog.show();
```

打開模擬器，在按下按鈕後，我們看到計算出 BMI 值的同時，螢幕上也彈出了一個有標題的對話框。

### 加入按鈕 ###

目前的對話框中，並沒有提供離開對話框的方法。所以我們得按下 「Undo」按鈕來離開對話框，有點不便，所以我們來為這個對話框加入一個「確認」按鈕。

```
dialog.setPositiveButton("確認",
    new DialogInterface.OnClickListener(){
        public void onClick(
            DialogInterface dialoginterface, int i){
            }
    })
```

「setPositiveButton」、「setNegativeButton」 或  「setNeutralButton」 函式都可以用來定義按鈕，各按鈕分別預設代表正面/中立/負面的結果（下一章會用到）。

上方程式碼中定義的「setPositiveButton」裡，包含了一個沒有作用的對話框介面(DialogInterface)。
表示當我們按下按鈕時，不做任何事就直接退出對話框。

完整對話框函式的程式碼如下

```
	private void openOptionsDialog() {
		AlertDialog.Builder dialog = new AlertDialog.Builder(Bmi.this)
		dialog.setTitle(R.string.about_title)
		dialog.setMessage(R.string.about_msg)
		dialog.setPositiveButton(R.string.ok_label,
		    new DialogInterface.OnClickListener(){
			public void onClick(
				DialogInterface dialoginterface, int i){
				}
			})
		dialog.show();
	}
}
```

更詳細的對話框使用可參考官方文件
http://code.google.com/android/reference/android/app/AlertDialog.Builder.html

註: Android 本身也有預先定義了一些基本訊息，如這裡使用到的「ok」訊息，其實可以使用系統預設的「android.R.string.ok」字串來替換。

## 順道一提 -「Toast 」介面元件 ##

對話框的使用模式，限制了使用者得按下某些按鍵以跳出對話框，才能繼續使用原本程式。如果我們只是要顯示一小段提示訊息，而不想打擾使用者的注意力，有沒有更適合的方法哩？
有的，我們可以把顯示方式比較有彈性的對話框拿掉，改為使用簡單的 「Toast 」介面元件。「Toast 」介面元件的作用是彈出一個訊息框，快速在螢幕上顯示一小段訊息。

程式碼如下：
```
import android.widget.Toast;
...
private void openOptionsDialog() {
    Toast popup =  Toast.makeText(Bmi.this, "BMI 計算器", Toast.LENGTH_SHORT);
    popup.show();
    /*new AlertDialog.Builder(this) //註解掉原本的對話框
   ...
   */
}
```

打開模擬器。我們按下「計算 BMI 值」按鈕後，螢幕上不再出現一個對話框，而改成彈出一段「BMI 計算器」文字訊息，過幾秒之後即自動隱去。

整段程式值得注意的兩行是
```
Toast popup = Toast.makeText(Bmi.this, "BMI 計算器", Toast.LENGTH_SHORT)
popup.show();
```

我們對 Toast 元件指定了欲顯示文字，與Toast 元件的顯示時間長短(LENGTH\_SHORT，即短訊息)，最後與處理對話框一樣，呼叫 「show() 」方法來將 Toast 元件顯示在螢幕上。

### 重構 ###

為了更好地重用，我們繼續把字串提取到「res/values/strings.xml」中

```
....
<string name="input_error">打錯了嗎？只能輸入數字喔</string>
</resources>
```

然後在程式中使用「R.string.input\_error」來取得字串
```
Toast popup = Toast.makeText(Bmi.this, R.string.input_error, Toast.LENGTH_SHORT);
popup.show();
```

別忘了不管是 AlertDialog 或者 Toast，這些函式後都必須加上「show()」方法，這樣提醒訊息才會顯示到螢幕上。

<  [重構程式](BmiRefactor.md) | [回目錄](DiveIntoAndroid.md) | [初見 Intent](AndroidUrl.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！