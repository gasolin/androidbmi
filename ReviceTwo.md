# 改版規劃 #

因應 Android 重大改版（1.5）的發佈，Android 開發環境的操作方式出現了一些改變，也新增了許多新的特性。

本書第二版將 以目前的章節為基礎修訂、增加新的章節內容，對各主題作更深入的探討，並維持一貫易於閱讀的風格。相容 Android SDK 1.5，訂正前版本的錯誤，加入索引、圖例以易於檢閱與理解。


# 目錄 #

本書的目錄如下

### 入門 ###
安裝並熟悉「Android」開發環境，學會如何新建/開啟「Android」專案並操作「Android」模擬器。使用範例：AppDemos。

  1. [初探 Android](IntroAndroid.md)
  1. [安裝 Android 開發工具](InstallAndroid.md)
  1. [開啟現有專案](OpenProject.md)
  1. [操作 Android 模擬器(Emulator)](PlayEmulator.md)
  1. [建立一個 Android 程式](ReadSource.md)

### 基礎 ###
熟悉「Android」應用程式專案的基本架構。能讀懂「Android」程式碼與 XML 介面描述檔，並學會使用基本介面元件來撰寫「Android」應用程式。使用範例：BMI。

  1. [描述使用者介面](AndroidUI.md)
  1. [設計使用者介面](BmiUI.md)
  1. [存取識別符號](XmlR.md)
  1. [解讀程式流程](AndroidLogic.md)
  1. [完成 BMI 程式](BmiLogic.md)

### 中階 ###
進一步熟悉「Android」應用程式設計的主要技術內容。使用範例：BMI。

  1. [重構程式](BmiRefactor.md)
  1. [加入對話框(Dialog)](AndroidDialog.md)
  1. [查看線上內容 (Uri)](AndroidUrl.md)
  1. [加入選單(Menu)](AndroidMenu.md)
  1. [定義 Android 清單](AndroidManifest.md)
  1. [加入新 Activity](AndroidActivity.md)
  1. [傳送資料到新 Activity](AndroidIntent.md)
  1. 訊息提醒 (Notification)
  1. [記錄與偵錯 (Log)](AndroidDebug.md)
  1. [活動的生命週期](LifeCycle.md)
  1. [儲存資訊(Preference)](AndroidPreference.md)
  1. [開發不息](NeverEnd.md)

### 融會貫通 ###
應用前面章節中使用到的觀念與技術，加深印象的同時也學習一些實用的新技巧。使用範例：aBMI。

  1. 顯性設計
  1. 支援多國語言
  1. 針對特性配置 (Orientation)
  1. 使用接口 (Adapter)
  1. 加入下拉選單元件 (Spinner)
  1. 簽發應用程式金鑰 (keytools)
  1. [發佈到 Android 市場(Market)](AndroidMarket.md)

### 資料庫應用 ###
學習 SQLite 資料庫與「Android」平台相關實用技能，並能使用 Android 上的資料庫完成增刪改查操作。使用範例：DummyNote。

  1. 加入列表活動 (ListActivity)
  1. 使用資料庫 (SQLite)
  1. 存取資料表 (SQLiteOpenHelper)
  1. 加入增刪改查操作(CRUD)
  1. 加入相依的活動 (ActivityForResult)
  1. 加入長按選單 (ContextMenu)

### 地圖與定位應用 ###
使用 Android 極富特色的地圖與定位功能，學習控制地圖元件、地圖定位、在地圖中設置地標等等與地圖/定位應用程式設計相關的技術。使用範例：twTrainStation、MyLocation。

  1. 申請 Google 地圖服務（API Key）
  1. 使用地圖（MapView）
  1. 加入按鍵控制 (KeyEvent)
  1. 取得現在位置（GPS/基地台三角定位）
  1. 結合地圖與定位功能（MyLocationOverlay）
  1. 為地圖標上地標（ItemizedOverlay）


### 附錄 ###

  1. 後記
  1. [取得原始碼](GetSource.md)

#### 資源 ####
  1. [Android 相關資源](AndroidResource.md) (相關資源)

# 當前版本 #

  * 1.3

# 歷程記錄 #

  * 1.3 2009/5/30 初稿完成
  * 1.2 2009/5/13 相容 1.5 版