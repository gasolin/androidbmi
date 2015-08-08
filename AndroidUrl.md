# 開啟網頁 #

我們已經對 Android 應用程式的寫法有了概觀的認識。可是我們還沒有觸及 Android 平台的特別之處：整合網路的應用。

在上一章中，我們學到如何使用對話框，與如何在對話框下添加按鈕，以回到原畫面。在這一章裡，我們來為我們的應用程式添加一個簡單的網路功能：在上一章實做的「openOptionsDialog」對話框函式中，新添一個「連線到首頁」的按鈕。

我們先把「openOptionsDialog」函式中使用到的字串增加到「res/values/string.xml」裡。因此完整的「res/values/string.xml」檔案如下：

```
1  <?xml version="1.0" encoding="utf-8"?>
2  <resources>
3      <string name="app_name">BMI</string>
4      <string name="height">身高 (cm)</string>
5      <string name="weight">體重 (kg)</string>
6      <string name="bmi_btn">計算 BMI 值</string>
7      <string name="bmi_result">你的 BMI 值是 </string>
8   
9      <string name="about_title">關於 Android BMI</string>
10     <string name="about_msg">Android BMI Calc 0.6\n
11         作者 gasolin\n
12         gasolin+android [at] gmail.com</string>
13     <string name="ok_label">確認</string>
14     <string name="homepage_label">首頁</string>
15 </resources>
```

增加了「連線到首頁」按鈕，完整「openOptionsDialog」函式的新版程式碼如下：
```
1  private void openOptionsDialog() {
2      new AlertDialog.Builder(Bmi.this)
3	    .setTitle(R.string.about_title)
4	    .setMessage(R.string.about_msg)
5	    .setPositiveButton(R.string.ok_label,
6	        new DialogInterface.OnClickListener(){
7		    public void onClick(
8		         DialogInterface dialoginterface, int i){
9		    }
10		})
11	    .setNegativeButton(R.string.homepage_label,
12		new DialogInterface.OnClickListener(){
13			public void onClick(
14			    DialogInterface dialoginterface, int i){
15			    //go to url
16			    Uri uri = Uri.parse("http://androidbmi.googlecode.com/");
17			    Intent intent = new Intent(Intent.ACTION_VIEW, uri);
18			    startActivity(intent);
19			}
20		})
21	    .show();
22    }
```


# 講解 #

在上一章「openOptionsDialog」函式的基礎上，我們在函式中添加了一個「setNegativeButton」方法，以提供另一個「NegativeButton」按鈕。

```
.setNegativeButton(R.string.homepage_label,
    new DialogInterface.OnClickListener(){
         public void onClick(
             DialogInterface dialoginterface, int i){
                 .....
             }
})
```

與上一章我們將 DialogInterface 中的內容空白不同的是，我們為這個按鈕添加了連線到特定網址(首頁)的「動作」，當使用者按下「首頁」按鈕後，程式會開啟瀏覽器，並連線到本專案的首頁「http://androidbmi.googlecode.com/」。

要完成整個連線的「動作」只需要三行程式碼：

```
//go to url 這是註解
Uri uri = Uri.parse("http://androidbmi.googlecode.com/");
Intent intent = new Intent(Intent.ACTION_VIEW, uri);
startActivity(intent);
```

以下是分行詳細的講解：

```
Uri uri = Uri.parse("http://androidbmi.googlecode.com/");
```
建立一個 Uri 實體，裡面包含我們要連到的網址「http://androidbmi.googlecode.com/」。

在我們第一次在程式碼中加入「Uri」時敘述時，「Uri」下方會出現紅色的線，表示「Uri」可能是個需要由外部導入（import）的函式或類別。在「Eclispe」開發環境中，我們可以使用「ctrl-shift-O」（Windows）或「cmd-shift-O」（Mac）來自動在程式開頭的地方導入「android.net.Uri」函式庫。

```
startActivity(intent);
```

透過「startActivity」 函式，Android 系統即根據收到不同 「意圖」(Intent) 的動作和內容，開啟對應的新頁面或新程式。

在 Android 平台上，各個 Activity 之間的呼叫與交流都要透過「startActivity」 一類的函式來互動。「startActivity」 一類的函式中，最重要需傳入的內容就是「意圖」(Intent) 。因此我們在後面會進一步闡述「Intent」與「Activity」之間的關係。

```
Intent intent = new Intent(Intent.ACTION_VIEW, uri);
```

在這行中，我們建立一個「意圖」(Intent) 實體，並傳入這個意圖的「動作」與「內容」。

Intent 的格式如下：

```
Intent intent = new Intent(動作, 內容);
```

我們所建立「意圖」(Intent) 中，所傳入的「動作」是「Intent.ACTION\_VIEW」。「Intent.ACTION\_VIEW」是 Android 內建的「動作」之一。在 Eclipse 編輯畫面中輸入「Intent.」時，Eclipse 編輯器會彈出可輸入的建議動作選單，我們可以透過這個選單，了解可使用的各種 Intent 內建動作。

「Intent.ACTION\_VIEW」這個動作的意義為：依所提供內容的不同，開啟對應的程式以檢視內容資料。我們可以把這個動作想成在一般桌面系統上，開啟一個已知的檔案類型檔案(比如說一張照片)，作業系統會用你預設的應用程式(比如說某看圖軟體)開啟這個檔案。本例中提供了「Uri」網址類型的內容給「Intent.ACTION\_VIEW」這個動作，所得到的結果，就是開啟瀏覽器並前往「http://androidbmi.googlecode.com/」 頁面。

## 再做好一點 ##

前面我們看到 Uri 實體的定義方法：

```
Uri uri = Uri.parse("http://androidbmi.googlecode.com/");
```

看到 Uri.parse() 中，有一個固定的網址，你應該也會想把它抽取出來，丟到 Resource 中統一管理。那麼我們把程式改寫，首先把網址抽取出來，放到「res/values/string.xml」檔案中。

「res/values/string.xml」檔案更新如下：

```
...
<string name="homepage_label">首頁</string>
<string name="homepage_uri">http://androidbmi.googlecode.com/</string>
```

我們把 Uri.parse() 函式修改，傳入資源識別符號.

```
Uri uri = Uri.parse(R.string.homepage_uri);
```

糟了，Eclipse 上出現了紅線，表示在我們的程式碼裡，有什麼地方弄錯了。
因為我們只修改了 Uri.parse 傳入的內容，我們可以很確定是我們傳入的內容錯了。
我們重新輸入「Uri.」，利用 Eclipse 的自動提示功能，看看 parse 函式到底接受那些類別的參數。

原來，Uri.parse() 函式並不接受資源識別符號型態的輸入。
這麼一來，我們就得自行根據資源識別符號，來取得資源識別符號所代表的文字敘述內容。

真正能執行的程式碼如下：

```
Uri uri = Uri.parse(getString(R.string.homepage_uri));
```

在程式中，我們可以使用「android.content.Context」類別中的「getString」 函式(或是getText)，來取得資源識別符號對應的文字。


<  [加入對話框](AndroidDialog.md) | [回目錄](DiveIntoAndroid.md) | [加入選單](AndroidMenu.md)  >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！