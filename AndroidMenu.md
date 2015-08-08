在進一步學習 Intent 與 Activity 之前，我們先來完善我們的應用程式。
在前幾章中，我們把  「openOptionsDialog」 這個用來彈出對話框的函式，放進「calcBMI」這個按鈕元件的「OnClickListener」方法中。現在，我們要把「openOptionsDialog」 移出「OnClickListener」方法，改成按下「Menu」鍵後，跳出一個選單列(Menu Bar)。當我們點擊選單列中的選項後，才彈出 「openOptionsDialog」 的對話框。

完整的程式碼如下：

```
1  protected static final int MENU_ABOUT = Menu.FIRST;
2  protected static final int MENU_Quit = Menu.FIRST+1;
3
4  @Override
5  public boolean onCreateOptionsMenu(Menu menu) {
6      super.onCreateOptionsMenu(menu);
7      menu.add(0, MENU_ABOUT, 0, "關於...");
8      menu.add(0, MENU_Quit, 0, "結束");
9      return true;
10 }
11
12 @Override
13 public boolean onOptionsItemSelected(MenuItem item)
14 {
15     super.onOptionsItemSelected(item);
16     switch(item.getItemId()){
17	    case MENU_ABOUT:
18	        openOptionsDialog();
19		break;
20         case MENU_Quit:
21	        finish();
22             break;
23	 }
24	 return true;
25 }
```

每個選單都包含兩個部分：

  1. 建立選單
  1. 處理選項動作

「onCreateOptionsMenu」函式即選單列的主體。在 Android 機器或模擬器上按下硬體的「Menu」(選單)鍵，所彈出的選單列即是靠「onCreateOptionsMenu」函式來定義。當我們在 Activity 中定義了 「onCreateOptionsMenu」 之後，按下「Menu」(選單)鍵時，就會彈出相對應的選單列。

當我們在 Android 應用程式的選單列上選擇了相應的選項後，則是依賴「onOptionsItemSelected」函式，來負責處理選單列中各選項所個別對應的動作。

在上面的程式裡，我們定義了「關於...」與「結束」兩個選單列中的選項。我們分部分講解如下：

## 建立選單 ##

在 「onCreateOptionsMenu」函式中，我們定義了兩個選單列中的選項。
分行講解如下：

```
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    super.onCreateOptionsMenu(menu);
    return true;
}
```

「onCreateOptionsMenu」這個函式是選單列的主體，它是一個「public」(公開)的函式。函式傳入一個「Menu」（選單）型別的「menu」參數。「boolean」則表示函式的返回值必須為「boolean」型別的值。因此在函式最後，我們提供函式一個返回值「true」。「@Override」表示我們要完全重寫掉已定義在「Activity」類別中的這個函式。

基於與 onCreate 函式一樣的原因，因為我們把選單列原本的動作覆載 (Override) 掉了，因此在撰寫我們自己的內容前，加上一句「super.onCreateOptionsMenu(menu)」敘述，用來呼叫「onCreateOptionsMenu」函式執行預設的動作。

```
menu.add(0, MENU_ABOUT, 0, "關於...");
menu.add(0, MENU_Quit, 0, "結束");
```

Android 每個頁面對應到一個 Activity，每個 Activity 都有一個獨立的選單列。對傳入的「menu」參數作處理就能改變選單列的內容。
> 我們看到，增加一個選單列中選項的格式如下：

```
menu.add(0, 識別符號(identifer), 0, 字串或資源識別符號);
```

最後一欄「字串或資源識別符號」就是顯示在螢幕上的敘述。
而「識別符號」的目的則是作為這個選項的標籤，以供後續處理選項動作時，更容易辨認出所對應的選項。

```
protected static final int MENU_ABOUT = Menu.FIRST;
protected static final int MENU_Quit = Menu.FIRST+1;
```

我們看到  MENU\_ABOUT 識別符號的定義，是一個固定的常數型別（static final int）。「Menu.FIRST」則代表識別選單開頭的數字，當然我們也可以把這「Menu.FIRST」代號直接用任意數字替換，看看程式會發生什麼事。


## 處理選項動作 ##

在「OptionsItemSelected」函式中，我們分行講解如下：

```
@Override
public boolean onOptionsItemSelected(MenuItem item)
{
    super.onOptionsItemSelected(item);
    return true;
}
```

「onOptionsItemSelected」這個函式是處理所有選項的主體，和「onCreateOptionsMenu」函式相同，也是一個「public」(公開)的函式。「onOptionsItemSelected」函式傳入了一個「MenuItem」（選項）型別的「item」參數。「boolean」表示函式的返回值必須為「boolean」型別的值。因此在函式最後，我們提供函式一個返回值「true」。
「super.onOptionsItemSelected(item);」表示我們要先執行已定義在「Activity」類別中原本的「onOptionsItemSelected」函式內容，後面再接著執行我們為此函式新定義的動作。

```
    switch(item.getItemId()){
```

我們可以用「item.getItemId()」函式來取得在螢幕上選取的選項所對應的識別符號代碼(identifer)。

```
    switch(識別符號代碼){
        ....
    }
```

在 swith 敘述中，我們根據從「item.getItemId()」函式取得的識別符號代碼判斷，
根據選到的識別符號代碼，作相應處理。

```
    case MENU_ABOUT:
        openOptionsDialog();
        break;
    case 
        ....
        break;
```

在「onOptionsItemSelected」函式中收到 「MENU\_ABOUT」 識別符號時，我們呼叫 「openOptionsDialog」 函式來彈出對話框。

```
    case MENU_Quit:
        finish();
        break;
```

在「onOptionsItemSelected」函式中收到 「MENU\_Quit」 識別符號時，我們呼叫 Android 內建的 「finish」函式來關閉這個 Activity。因為我們的「BMI」應用程式只由一個「Bmi」Activity 組成，所以當我們呼叫「finish」函式來關閉「Bmi」這個 Activity，就等於直接關閉了這個「BMI」應用程式。

而事實上， 在 Android 平台上，無論是開發者或是使用者，都不需要自己來關閉 Activity。 因為 Android 虛擬機(Dalvik) 接手了什麼時候 Activity 該啟動或關閉的工作。整個 Android Activity 的運作流程，將在後續章節中作講解。


< [初見 Intent](AndroidUrl.md) | [回目錄](DiveIntoAndroid.md) | [定義 Android 清單](AndroidManifest.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！