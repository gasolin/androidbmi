# 視圖(View) #

軟體設計的過程中，常常會遇到需要頻繁修改使用者介面的情境。改著改著程式設計師們就累積起了一些經驗，也歸納出了許多應對之道。如著名的 MVC（Model-View-Controller） 模式。Google Android 為我們考慮了介面修改問題。Android 為了單純化介面修改方式，採用了目前比較流行的解決方案--即將介面描述部份的程式碼，抽取到程式外部的 XML 描述文件中。

我們在前面的過程裡已經學到，如何在 Android 應用程式中替換 TextView 介面元件所顯示的純文字內容。那麼...這個經驗能不能直接用到 BMI 應用程式的設計上呢？

我們先回過頭來思考， 要實現基本的BMI計算功能，在螢幕上至少需要哪些介面元件，以供使用者輸入數值和查看結果？

為了輸入 BMI 程式所需的身高體重值，大致上我們需要兩個 TextView 元件用來提示填入身高體重數字，另外也需要兩個文字輸入欄位用來填入身高體重數字。我們還需要一個按鈕來開始計算，而計算完也需要一個 TextView 元件來顯示計算結果。於是初版的 BMI 應用程式介面的樣子就浮現出來了。

# 查閱文件 #

話說回來，我們從哪得知各種可用的介面元件呢？其中一個方法是查閱文件。

Android 文件網站上找到各種可用介面元件列表。

> http://developer.android.com/guide/tutorials/views/index.html


例如我們想查看 EditText 的內容，我們可以點進 EditText 連結查看其內容。
http://developer.android.com/reference/android/widget/EditText.html

你會看到一個詳細地驚人的網頁。

這邊舉其中常用到的 EditText 介面元件為例。EditText 介面元件的作用就是提供一個文字輸入欄位。EditText 繼承自另一個叫 TextView 的介面元件，TextView 介面元件的作用是提供文字顯示，所以 EditText 介面元件也擁有所有 TextView 介面元件的特性。
此外，文件中你也可以查找到 EditText 欄位的一些特殊屬性，如 「android:numeric="integer"」(僅允許輸入整數數字)、「android:phoneNumber="true"」(僅允許輸入電話號碼)，或「android:autoLink="all"」(自動將文字轉成超連結)。
例如要限制 EditText 中只允許輸入數字的話，我們可以在 XML 描述檔中，透過將 EditText 的參數「android:numeric」 指定為 「true」，以限制使用者只能在 EditText 文字欄位中輸入數字。

# 離線文件 #

當你處於沒有網路連接的情況下時，也可以找到 Android 文件參考。
在下載了 android-sdk 後，將之解壓縮，你可以在「android-sdk/docs」 目錄中 (android\_sdk/docs/reference/view-gallery.html) ，找到一份與線上文件相同的文件參考。

## 開始設計 ##

我們從實例來開始，定義一個基本 BMI 程式所需的身高(Height)輸入欄位，就會用到 EditText，與 TextView 介面元件，其描述如下：
```
1  <TextView
2     android:layout_width="fill_parent"
3     android:layout_height="wrap_content"
4     android:text="身高 (cm)"
5     />
6  <EditText android:id="@+id/height"
7     android:layout_width="fill_parent"
8     android:layout_height="wrap_content"
9     android:numeric="integer"
10    android:text=""
11    />
```

可以看到 EditText 介面元件描述的基本的組成與 TextView 介面元件相似，都用到了「android:layout\_width」與「android:layout\_height」屬性。
另外，指定的另外兩個屬性「android:numeric」、「android:text」則是 EditText 介面元件的特別屬性。「android:text」屬性是繼承自 TextView 介面元件的屬性。

```
    android:numeric="integer"
    android:text=""
```
將 「android:numeric」 指定為 「integer」，可以限制使用者只能在 EditText 文字欄位中輸入整數數字。「android:text」屬性則是指定 EditText 介面元件預設顯示的文字(數字)。

我們再來看看 Button (按鈕)介面元件

```
         <Button android:id="@+id/submit"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:text="計算 BMI 值"
            />
```

Button 介面元件同樣有 「android:layout\_width」與「android:layout\_height」屬性，另外一個「android:text」屬性則用來顯示按鈕上的文字。

# 整合 #

我們這就從文件中挑出我們需要的 TextView(文字檢視)、EditText(編輯文字)、Button(按鈕) 三種介面元件，照前面的設計擺進 LinearLayout (線性版面配置)元件中。

完整的「main.xml」介面描述檔如下：
```
    <?xml version="1.0" encoding="utf-8"?>
    <LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
        android:orientation="vertical"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        >
        <TextView
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:text="身高 (cm)"
            />
        <EditText android:id="@+id/height"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:numeric="integer"
            android:text=""
            />
        <TextView
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:text="體重 (kg)"
            />
         <EditText android:id="@+id/weight"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:numeric="integer"
            android:text=""
            />
         <Button android:id="@+id/submit"
            android:layout_width="fill_parent"
            android:layout_height="wrap_content"
            android:text="計算 BMI 值"
            />
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
    </LinearLayout>
```

我們可以啟動模擬器檢視執行結果。或是在頁面標籤下選擇「Layout」標籤，來預覽頁面配置。

啟動模擬器之後，模擬器畫面上出現了兩個輸入欄位。欄位上方分別標示著「身高 (cm)」、「體重 (kg)」。在兩個輸入欄位下方，是一個標示著「計算 BMI 值」的按鈕。
當你在欄位中試著輸入文字或數字(你可以直接用電腦鍵盤輸入，或按著模擬器上的虛擬鍵盤輸入)時，你也會發現，正 XML 描述檔的描述中對兩個 EditText 欄位所規定的，欄位中只能輸入數字。

我們在上面XML描述檔中定義的最後兩個 TextView 介面元件，由於並未替這兩個介面元件指定「android:text」屬性，所以在螢幕上並未顯示。這兩個介面元件在後面章節中會派上用場。



# 革命的路還長 #

高興了沒多久，你發現按下"計算 BMI 值" 按鈕後，應用程式完全沒反應。

這是正常的，因為我們還沒處理從介面輸入取得身高體重、將數值導入 BMI 計算方式、將結果輸出到螢幕上...等等 BMI 應用程式的關鍵內容。
不過在進入了解程式流程之前，我們還有一個「android:id」屬性尚未解釋哩。
接著我們將透過講解「android:id」屬性，來進一步了解 Android UI。

# 視覺化的介面開發工具 #

目前的 ADT 版本提供了預覽介面的功能，但尚未提供方便地視覺化拖拉介面元件的開發工具。以後也許 ADT 會加入完整的 GUI 拖拉設計工具。

但在 ADT 加入完整的 GUI 拖拉設計工具之前，已經有人寫出來了對應 Android 的 GUI 拖拉設計工具，可供使用。

DroidDraw - Android GUI 拖拉設計工具
http://code.google.com/p/droiddraw/

< [描述使用者介面](AndroidUI.md) | [回目錄](DiveIntoAndroid.md) | [存取識別符號](XmlR.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！