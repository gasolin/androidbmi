# Android Market #

要釋出程式讓所有使用者使用有三種方式：

  1. 發佈到 Android Market
  1. 自己提供程式線上下載
  1. 發佈到第三方 Android 應用程式下載網站

「Android Market (市集)」是一個「Android」官方(Google)提供的「Android」應用程式下載網站，同時也內建於所有的「Android」手機中。透過手機上的「Market」程式，使用者可以直接在「Android」手機上瀏覽「Android Market」網站，查看各種可供使用的應用程式。看到喜歡的程式可以直接下載安裝。也可以透過「Android Market」為這些軟體打分、或是交換對這些軟體的意見。

我們也可以將寫好的應用程式放在自己的網站上提供下載，或是透過其他的「Android」應用程式下載網站發佈。但是，還有哪個地方會比官方的「Android Market」更容易吸引使用者造訪呢？所以我們將主要介紹如何將應用程式發佈到官方「Android Market」上。

# Android Market 的運作方式 #

「Android Market」的運作方式如下

  * 開發者可以將自己寫好的軟體上傳到 Android Market 中。
  * 開發者透過 Android Market 販賣軟體的 30% 收入，得分給電信商跟電子收費商(如手機月費帳單或 Google Checkout 等)，所以開發者可以拿到應用程式定價的 70%。
  * 註冊為「Android Market Developer」要收美金 25元的「入場費」。推測可能是種為了保證「Android Market」上應用程式的質量，也為了促使開發者寫一點收費軟體，好讓電信商有得分成的策略。


## 註冊 Android Market ##

前往 http://www.android.com/market/ ，畫面右上角有一段「Interested in having your application in Android Market?」敘述，按下其下方的「learn more」按鈕，即可開始註冊成為「Android」開發者。

開發者用的網址是 http://market.android.com/publish

開發者可以透過「Android Market」發佈「Android」應用程式。首先，開發者得註冊一個 Google 帳號。然後使用(Google Checkout)以信用卡付出 $25 美元的註冊費用。
最後得同意「Android Market」的使用授權協議。

註冊一個 Google 帳號不難，相信大部分讀者都已經擁有一個 Google 帳號。

在申請「Android Market」時要填入加上國碼的手機號碼。台灣加上國碼的手機號碼為「+8869xxxxxxxx」。「886」是國碼，加上一個「0」之後，「09xxxxxxxx」是你的手機號碼。「+」則是「加上國碼的手機號碼」表示方式。

接著按下「Google Checkout」圖示，如果沒有「Google Checkout」的話，也需作先設定。一切完成後在「Google Checkout」中勾選「I agree and I am willing to associate my credit card and account registration above with the Android Market Developer Distribution Agreement.」。畫面會出現「等待信用卡認證的訊息」，並有 「Google Checkout」的確認函寄到我們設定的電子信箱中。接著想要繼續登錄開發者網頁時，會發現這個網頁似乎壞掉了。其實是等待信用卡認證完成，需要一點時間（一兩個鐘頭），等認證好，完成付款程序後，網頁就能再次開啟。

開啟後會出現「Your Registration to the Android Market is approved!You can now upload and publish software to the Android Market.」(已經註冊完成)訊息。以後點擊「Android Market」網頁右上角的按鈕時，就會進入開發者面板（Developer Console）頁面。

在開發者面板畫面的左上角是開發者的暱稱。暱稱旁邊可以選擇「Edit profile » 」（編輯個人資料）來編輯之前填入的「Android Market Developer」資訊。

## 上傳應用程式到 Android Market ##

選擇右下角的「Upload Application」（上傳應用程式）按鈕，出現應用程式上傳畫面。各個欄位的作用都寫的很明白，也可以為應用程式自行定價。

「Android Market」上所有的程式可分為「應用程式」與「遊戲」兩大類。選擇好大分類後，其下會出現各自可選的子分類。

在「Upload assets」區塊中，點選「Application .apk file」旁的「瀏覽...」按鈕，就可以上傳已經簽署好金鑰的「.apk」程式。（本書還未提及怎麼釋出簽署金鑰的應用程式）

直接選擇「BMI/bin/」目錄中的「BMI.apk」的話，會出現

```
    Market does not accept apks signed with the debug certificate. Create a new certificate that is valid for at least 50 years.
    Market requires that the certificate used to sign the apk be valid until at least October 22, 2033. Create a new certificate.
```

這段警告訊息。意思是說我們要上傳的「apk」檔用的是「debug」的授權金鑰，這樣是不能用做發佈的，我們得要自行簽署金鑰才成。

如果改選擇透過「AndroidManifest.xml」的「Overview」頁籤中「Exporting the unsigned .apk」連結，會出現訊息

```
    The apk is not properly signed.
```

如果驗證成功，該欄位上會直接出現該應用程式圖標（icon），與所需的存取權限(permissions)數目。

最後按下左下方的「Publish」按鈕，即可將應用程式發佈到「Android Market」上。

## 檢視成果 - 查看管理介面 ##

「Android Market」的開發者面板（Developer Console）頁面上，列出了開發者當前已發佈與未發佈的應用程式名稱與圖標。應用程式名稱右側有明顯的星號，表示目前的使用者評價。星號旁邊的括號表示當前已給予評價的人數。星號的右方是該程式的定價。最右側則是應用程式狀態，已發佈的應用程式狀態是「Published」。還未發佈的應用程式狀態是「Saved Draft」。

目前只有透過「Android」手機，才能查看關於應用程式的評論。

線上查看評論可以透過 [cyket](http://www.cyrket.com)查看。

程式熱門程度排名可以透過 [aTrackDog](http://atrackdog.a0soft.com/) 和 [AndroidStats ](http://www.androidstats.com) 等網站查看。


# 自行提供程式線上下載 #

要自行提供程式線上下載的話，需要指定下載檔案的 MIME 類型。可以在「Apache」網頁伺服器的「.htaccess」設定中加入:

```
    AddType application/vnd.android.package-archive apk
```

一行，如此一來使用者在瀏覽器中點選到「.apk」檔的連結時，瀏覽器能自動辨識該檔案為「Android」應用程式類型。


# 發佈到第三方 Android 應用程式下載網站 #

請自行參考「參考資料」中的「其他的 Android 應用程式下載網站」。


# 針對使用者作設計 #

針對使用者作設計，有沒有意義呢？每個人都有自己的一套道理，不如就用數據來說話吧。

在「Android Market」開放給開發者上傳應用程式的第一天（美國時間10/27），作者即將本書中的兩個範例程式「aBMI」(英制)（本章的範例）、「gBMI」(公制)（基礎、中階的範例）上傳到「Android Market」上。考慮到當時使用者(美國)主要集中在使用英制的國家，因此預期「aBMI」應用程式會得到比較好的評價。

果然，在第一天結束之後，「aBMI」(英制)得到 732 次下載，目前「active installs」(仍安裝在機器上)的人數為 452 人（比率 61%）。共有 25 個人平均給予 3 顆星的評價。就一個運作相當簡單的應用程式而言，比起其他書籍範例的完成度，3 顆星的評價還是算相當可接受的。

至於「gBMI」(公制)則因為不是針對目標使用者設計，得到 602 次下載，「active installs」的人數為 193 人(比率 32%)。只有 11 個人平均給 2 顆星的評價。

因此可以明顯看到，「gBMI」不論是下載的人數、安裝後繼續使用的比率，或是整體評價都要比「aBMI」差一個檔次。當 Android 手機在使用「公制」的國家開賣後，相信比例或評價會再次變化。

我們在設計兩個應用程式時，同樣需花上差不多的時間，但是卻得到有相當明顯差別的結果。由此可以看出，手機應用程式需針對使用者特性來設計的重要性。


# 參考資料 #

  * Android Market http://www.android.com/market/
  * Signing and Publishing Your Applications http://code.google.com/android/devel/sign-publish.html
  * http://docs.sun.com/app/docs/doc/820-4607/ablqz?l=zh_TW&a=view
  * http://www.anddev.org/viewtopic.php?p=12252
  * http://keytool.sourceforge.net/

其他的 Android 應用程式集散地

  * AndAppStore http://andappstore.com/
  * MobiHand OnlyAndroid http://onlyandroid.mobihand.com/
  * SlideMe http://www.slideme.org/
  * [各種 Android 市集一覽表](ShanzaiMarket.md)


<  [儲存資訊(Preference)](AndroidPreference.md) | [回目錄](DiveIntoAndroid.md) | [開發不息](NeverEnd.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！