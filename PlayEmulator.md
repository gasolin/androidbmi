# 使用 Android 虛擬機器 #

我們已經透過「Eclipse」開發環境，開啟了「ApiDemos」專案。本章將講解如何設定和操作 Android 虛擬機器。

## 設定 Android 虛擬機器 ##

現在我們還不忙著開始寫程式，先花點時間，來看看怎麼在開發環境中，透過「Android 虛擬機器」來執行應用程式吧。

由於在剛開始開發時，我們手邊並不一定已擁有 Android 設備。因此 Android 開發工具亦提供了相當強大的模擬器，能讓我們自由配置，模擬各種硬體規格的設備。在 Android 中一律把 Android 模擬器稱作「Android 虛擬機器」（Android Virtual Device），簡寫為「AVD」。

「Android 開發工具」（ADT）提供了支援不同版本虛擬機器的功能。在使用虛擬機器之前，必須先建立一個虛擬機器，然後才可在 Eclipse 開發環境中使用。

我們可以在Eclipse中選擇「Window->AVD Manager」來開啟AVD管理工具。

在Android虛擬機器管理工具中，我們可以建立新的虛擬機器或刪除現有的虛擬機器。點選右側的「New...」按鈕，會彈出「Create New Android Virtual Device (AVD)」（建立新Android虛擬機器）視窗。

只要在視窗中的「Name」欄位中填入虛擬機器名稱，選擇適當的目標版本（Target），按下「Create AVD」按鍵，即可建立新的虛擬機器。

虛擬機器建立成功後，在管理工具畫面中選取虛擬機器，按下「Start...」鍵，在彈出的視窗中點選「Launch」按鈕，即可啟動虛擬機器。

## 設定環境參數 ##

要執行 ApiDemos 程式前，我們得在開發環境中，事先設定好一些用來執行 ApiDemos 程式的環境參數。
以後使用其他程式專案時，我們也能用同樣的方式，讓這些程式在我們的開發環境中運行。

首先，我們透過選單列上的「Run」(執行)選單，選擇「開啟執行參數設定」(Run-> Debug Configurations...) 進入運行環境參數設定畫面。

進入設定畫面後，在視窗左側會有一整排 Eclipse 支援的運行設定，我們從中找到 "Android Application"(Android 應用程式)項目，按下滑鼠右鍵，點選 "New"(新增)選項。

選擇 「New」 選項後，在「Android Application」項目下方會多出一筆執行項目。

我們可以在 Name 欄位上輸入一個代表這個環境參數的名稱，在此我們輸入與專案名稱相同的「ApiDemos」。

在「Project」欄位右方，點選「Browse...」按鈕，開啟「專案選擇」（Project Selection）視窗，選擇「ApiDemos」專案並點選「OK」按鈕，以選擇要執行的專案。

在 「Launch Action」 選單中，確認預設選擇的是「Launch Default Activity」。

至此我們就完成了模擬器環境參數的設定。 點選右下角的「Debug」按鈕，Eclipse 就會啟動 Android 虛擬機器。

小技巧:
> 在選單列中，也可以選擇設定「Run Configuration...」選項。這時我們得到的是一個幾乎完全相同的環境參數設定畫面，只是右下角的「Debug」按鈕變成了「Run」按鈕。「Debug」與「Run」模式的環境參數設定可以共用，差別在於「Debug」模式下可以使用在之後章節中會介紹的 logd，來顯示一些開發時所需的額外訊息。

## 再次啟動 Android 虛擬機器 ##

當我們設定好之後，以後碰到要再次啟動虛擬機器的情況時，只要在螢幕左上角的「Debug」或「Run」圖示右側小箭頭上按一下，從彈出的選單中選擇剛剛設定的環境參數名稱，虛擬機器即開始執行，並安裝好我們所指定的專案應用程式。

# 操作虛擬機器 #

## 改變虛擬機器外觀 ##

在建立虛擬機器的時候，我們可以透過「skin」欄位來選擇預設的虛擬機器外觀。「skin」欄位中會列出目標（Target）版本支援的所有外觀。「HVGA」（解析度 480x320）、「QVGA」（解析度 320x240）等分別代表著各種不同畫面的解析度

## 切換螢幕方向 ##

在 Windows 作業系統上按下 「Ctrl」和「F12」鍵 ，或是在 Mac OS X 作業系統上同時按下「fn」 、「Control」和「F12」鍵，螢幕就會從預設的直式顯示改成橫式顯示，再按一次則切換回原來的直式顯示。

閱讀參考

  * 虛擬機器操作細節 http://developer.android.com/tools/devices/emulator.html

< [開啟現有專案](OpenProject.md) | [回目錄](DiveIntoAndroid.md) | [建立一個 Android 程式](ReadSource.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！