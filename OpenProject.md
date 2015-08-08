# 開啟專案 #

我們回到 Eclipse 環境來。在螢幕上方的選單列上，選擇「File > New > Project...」，會彈出精靈選擇視窗（Select a Wizard），在精靈選擇視窗中可以選擇要開啟新專案還是開啟現有專案。

在精靈選擇視窗（Select a Wizard）中，從中選擇「Android Project from Existing Code」（透過現成程式碼建立Android專案），會彈出「 Import Projects」視窗。

在「Import Projects」對話視窗中，點選「Browse...」按鈕以選擇要開啟的專案。我們在此選擇位於「android\_sdk/samples/android-x/」目錄中的 「ApiDemos」應用程式專案 (android\_sdk/samples/android-x/ ApiDemos)。 「x」代表目標版本號。

當我們選擇了現存的範例程式專案時，對話視窗中會自動找到對應的專案內容。這時我們就可以按下 「Finish」按鈕，完成從現存專案新增專案進「Eclipse」開發環境的動作。

# 刪除專案 #

開啟專案後，「 ApiDemos 」專案會產生一個資料夾圖示，並示在Eclipse環境左側的「Package Explorer」視窗中。

要移除專案，只要點選「tests」和「com.example.android.apis.ApiDemos 」專案資料夾圖示上，按右鍵選擇「Delete」選項，在彈出視窗中選擇「OK」即可移除專案。

# 修復專案 #

完成新增程式專案到 Eclipse 後，我們可以在左側的「Package Explorer」中找到我們新增的專案。

如果發現開啟後的資料夾圖示上有個小小的黃色驚嘆號，表示這個專案匯入後還有些問題，我們可以使用ADT內建的功能來試著修復專案屬性。
在「Package Explorer」的 「ApiDemos」 專案檔案夾圖示上點選右鍵，從「Android Tools」選單中選擇「修復專案屬性」(Fix Project Properties)。
(Android Tools->Fix Project Properties)

如果發現開啟後的資料夾圖示上有個小小的紅色叉號，表示這個專案開啟/匯入後遇到了無法編譯的問題。最常見的也是與無法正常生成「gen」目錄相關的問題。一般簡單的解決方式是打開專案中任一 XML 檔案（如AndroidManifest.xml 或是「res」目錄下附檔名為 .xml 的檔案），改變一下內容（如在檔案中多按一個空格）後存檔，這時開發工具會自動編譯生成「gen」目錄中新的內容。這樣無法編譯的問題往往就解決了。如何修改 XML 檔案在後面章節中會提到。

# 切換 SDK 版本 #

Android 在 SDK 1.5 版之後引入了支援多個版本 SDK 與模擬器的新特性，讓我們得以透過修改屬性設定畫面的設定，來切換用來編譯與運行這些專案的目標 SDK 版本。

在「Navigator」的「ApiDemos」專案檔案夾圖示上點選右鍵，選擇「properties」選項，會開啟專案屬性設定畫面。

在設定畫面中先選擇左方的 Android 標籤，選擇後會出現可勾選的「Project Build Target」選單。

在選單中選擇適當的目標版本，選擇好之後按下 OK 結束設定畫面，這時專案就已經切換成可使用目標版本編譯的狀態了。

## 參考資料 ##

  * 如何開啟 Hello World 程式 http://developer.android.com/training/basics/firstapp/index.html

< [管理 SDK](ManageSDK.md) | [回目錄](DiveIntoAndroid.md) | [操作虛擬機器](PlayEmulator.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！