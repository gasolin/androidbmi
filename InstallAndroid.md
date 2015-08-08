Android 提供免費而且跨平台的整合開發環境，只要電腦能連接上網路，我們隨時都能下載相關工具下來，並開始開發 Android 應用程式。
有了輕鬆易用的開發工具，我們可以把心力專注於如何將想法實現到應用程式上。

# 系統需求 #

撰寫 Android 的應用程式，需要一套個人電腦系統。至於作業系統的部份，幾個主流作業系統都有支援。

支援的作業系統如下：

  * Windows XP 或之後版本
  * Mac OS X 10.5.8 或之後版本
  * Linux (官方是在 Ubuntu 上測試)

我們需要安裝一些 Android 開發環境所需的程式工具，這些工具都是可以免費上網取得的：

  * JDK 6以上
    * 只安裝 Java 運行環境(JRE) 是不夠的，你需要安裝的是Java開發環境 (JDK)。
    * 各平台的 JDK 可以前往   http://www.oracle.com/technetwork/java/index.html 網站，選擇「Previous Releases」連結，找到Java標準版(Java SE)連結後下載對應平台的Java SE版本。
Mac OS X 作業系統則已內建 JDK，可以通過「應用程式/工具程式/Java偏好設定」來調整預設的Java版本。

  * 可以在命令行上輸入 「java -version」 來查看目前系統上已安裝的 java 版本(java 版本需為 1.6)。
  * 要注意的是 Android 與 Java Gnu 編譯器 (gcj) 還不相容。
  * Eclipse IDE，一個多用途的開發工具平台。
> > 你可以下載安裝 Eclipse 3.6 (代號 Helios) 以上版本。
> > 請注意你選擇的版本需包含 Eclipse Java 開發工具擴充套件(Java Development Tool Plugin, JDT)。
> > 大多數 Eclipse IDE 包中都已含有 JDT 擴充套件。若對 Eclipse 平台不熟悉的話，建議直接選擇 「for Java Developers」版本來下載。
  * ADT，基於 Eclipse 的 Android 開發工具擴充套件 (Android Development Tools plugin)。
  * Android SDK，Android 程式開發套件，包含 Android 手機模擬器(Emulator)。
  * 其他開發環境工具（非必要安裝）
> > o 各平台上需要自動編譯的話可以自行安裝 Apache Ant 1.8 或之後版本。
> > o NetBeans、IDEA 等開發平台亦有推出自己的 Android 開發工具，但本書中還是以討論官方基於 Eclipse 平台的開發工具為準，其他平台不予涉及。

# 安裝流程 #

假設讀者已先安裝了 JDK 6。

現在可前往 http://developer.android.com/sdk/index.html 下載包含 Eclipse，ADT擴充套件，Android SDK的開發套件包。解壓縮後點選「Eclipse」圖示，即可開始使用。若開啟成功即可繼續閱讀下一章。


# 手動安裝步驟 #

舊版的 Android 手動安裝流程可以分為以下五個步驟
  1. 下載 Eclipse
  1. 安裝 Eclipse
  1. 安裝 ADT 擴充套件
  1. 下載 Android SDK
  1. 設定 Android SDK

詳細的安裝流程如下：

## 1. 下載 Eclipse ##

首先我們需要下載 Android 開發時會用到的整合開發環境 Eclipse。
目前 Android 應用程式只支援使用「Java」程式語言來編寫 Android 應用程式。所以開發前必須先安裝 Java 開發套件(Java SE Development Kit, JDK)。
安裝好 JDK 後，我們可以前往 [Eclipse](http://www.eclipse.org/downloads/) 網站下載 Eclipse 這個方便的整合開發環境。
下載 Eclipse 時請選「Eclipse for Mobile Developers」版本。

下載完同樣先解壓縮到適當目錄下。


---


## 2. 安裝 Eclipse ##

Eclipse 不需要安裝，只要確認你的系統上有安裝 Java，即可直接開啟 Eclipse 資料夾，點擊 Eclipse 開始執行 Eclipse 整合開發環境。
第一次啟動 Eclipse 時會彈出視窗讓你決定預設的工作目錄。一般使用 Eclipse 預設的工作目錄即可。
進入到 Eclipse IDE 後，不必急著四處觀望。我們先來安裝 Android 開發工具擴充套件。


---


## 3. 安裝 ADT 擴充套件 ##

我們將在 Eclipse 上 安裝 Android 開發工具 (ADT)。

### Eclipse 3.6 版以上 ###

找到螢幕上方的選單列， 選擇 「Help->Install New Softare」 選項，這選項會帶出一個新視窗。
選擇「Available Software」標籤，選擇右方的 「Add...」 (新增網站)按鈕，會彈出一個輸入框。

在輸入框中的"Location"欄位中輸入擴充套件的名稱(Name) 「ADT」 跟網址(URL) 「http://dl-ssl.google.com/android/eclipse/site.xml 」，按下 "OK" 按鈕離開。Eclipse 會花一點時間尋找合適的版本。

在視窗中全選「 https://dl-ssl.google.com/android/eclipse/site.xml 」項目「Developer Tools」中的的選項後，按下右方的「Install」按鈕。

按下 「Next」 (下一步)鍵。照著步驟就安裝完成。安裝完會提示需重新啟動 Eclipse，按下 「Yes」 重新啟動。

### 離線安裝 ###

已經安裝成功的讀者可以跳過這段。有些讀者因為網路環境的關係，無法順利地直接線上安裝 Android 開發工具。這時我們可以先前往 http://developer.android.com/sdk/installing/installing-adt.html，手動下載最新的開發工具版本來離線安裝。

下載完最新的 ADT 擴充套件後，打開 Eclipse 開發環境，找到螢幕上方的選單列， 選擇 「Help->Software Updates」 選項，這選項會帶出一個新視窗。選擇「Available Software」標籤，選擇右方的 「Add Site...」 (新增網站)按鈕，會彈出一個輸入框。

選擇右上角的「Local...」按鈕，並選取剛下載的 Android 最新開發工具檔案，選到之後按下 "OK" 按鈕離開。
在視窗中全選新出現項目的所有選項後，按下右方的「Install」按鈕。Eclipse 會花一點時間開始安裝 ADT 擴充套件。


---


## 4. 下載 Android SDK ##

接著我們要從 [http://developer.android.com/ Android 官方網站](.md)下載 「Android 軟體開發套件」 (Software Development Kit, SDK)。
下載下來的 SDK 檔案需要先解壓縮。Windows 平台需要先另行安裝解壓縮程式，如免費的 [7-zip](http://www.7-zip.org/zh-tw/) 解壓縮工具。
解壓縮後會出現一個資料夾。為了之後描述方便，我們將解壓縮後的 Android SDK 檔案夾命名為「android\_sdk」。


---


## 5. 設定 Android SDK ##

打開偏好設定頁面(Preference)，選擇 Android 標籤(請確認您已安裝好 ADT 擴充套件，Android 標籤才會出現在偏好設定頁面中)，在 SDK Location 欄位按下 " Browse..."鍵，選擇剛剛解壓縮完的「android\_sdk」檔案夾所在地，然後按下視窗右下角的套用(Apply) 按鈕。
這樣一來，Android SDK 就算是設定好啦。


> 註解：若您安裝過 SDK 1.5 版之前的版本，請先移除後再重新安裝一次 ADT 擴充套件，才能順利設定新版的 Android SDK。 方法是在螢幕上方的選單列，選擇「Help > Software Updates」選項，在彈出的視窗上方點選「Installed Software」頁籤，選擇「Android」開頭的選項，點選右側的「Uninstall..」按鈕移除這些相關的插件。


---


# 下一步 #

設定好 Android SDK 後，我們就擁有了一個完整的 Android 開發環境。
我們先來看看 Android SDK 中提供的一些範例，好了解 Android 到底能做些什麼。

## 參考資料 ##

**Eclipse 網站 http://www.eclipse.org/downloads/** 安裝擴充套件 http://developer.android.com/sdk/installing/index.html
**7-zip http://www.7-zip.org/**

< [初探 Android](IntroAndroid.md) | [回目錄](DiveIntoAndroid.md) | [管理 SDK](ManageSDK.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！