SDK 中也提供了一個「android」命令行工具（在 android-sdk/tools 中），可以用來建立新專案或是管理虛擬機器。在此我們使用「android」命令行工具來新建立一個虛擬機器。

### 列出虛擬機器類型 ###

首先，把「android-sdk/tools 」目錄加入系統路徑，我們以後就可以在任何地方使用「android-sdk/tools 」目錄下的各種命令。

在 Windows 2000、XP、2003、Windows 7 這些作業系統裡，點選「控制台 > 系統 > 進階 > 環境變數」。在「系統變數(S)」欄中，選取「PATH」變數名稱後，再點選「編輯(I)」按鈕。

再此假設您安裝 Android SDK 的路徑是「C:\android-sdk\tools」，接著在彈出的視窗中將「;C:\android-sdk\tools」（注意要以分號隔開）這字串添在原本的字串之後，按下確定後重新啟動作業系統。

重開系統後選擇「開始 > 執行」，在彈出的輸入框中輸入「cmd」，即可開啟命令行工具並繼續以下的動作。

或是您也可以直接打開命令行，進入「android-sdk/tools 」目錄，輸入以下命令：
```
$ android list targets
```

在沒有將 Android SDK 加入路徑的情況下，在 Linux 或 Mac 環境中要輸入
```
$ ./android list targets
```

螢幕上會列出所有支援的虛擬機器類型

```
$ android list targets
Available Android targets:
id: 1 or "android-5"
     Name: Android 2.0
     Type: Platform
     API level: 5
     Revision: 1
     Skins: HVGA (default), QVGA, WQVGA400, WQVGA432, WVGA800, WVGA854
id: 2 or "Google Inc.:Google APIs:5"
     Name: Google APIs
     Type: Add-On
     Vendor: Google Inc.
     Revision: 1
     Description: Android + Google APIs
     Based on Android 2.0 (API level 5)
     Libraries:
      * com.google.android.maps (maps.jar)
          API for Google Maps
     Skins: WVGA854, WQVGA400, HVGA (default), WQVGA432, WVGA800, QVGA
```

在這邊列出了三種虛擬機器類型。分別是編號(id)為 1 的 Android 2.0 虛擬機器，與編號(id)為 2 的「Google APIs」，Google 把自己提供的應用程式（如 Google Map）放在「Google APIs」這個虛擬機器類型中，因此要開發 Google Map 等 Google 專屬應用程式時，就必須先建立「Google APIs」這類型的虛擬機器，稍後才能在適當的虛擬機器上作驗證。

### 建立虛擬機器 ###

我們現在來建立一個基本的 Android SDK 2.0 虛擬機器。

在命令行中輸入以下命令：

```
$ android create avd --target 1 --name eclair
```

這段命令的意思是：使用「android create avd」命令來建立一個新的虛擬機器，「 --target 1」參數的意思是這個虛擬機器使用 id 為 1 的 SDK 套件（Android 1.5），「--name eclair」參數的意思是將這個建立的虛擬機器命名為「eclair」。

產生的結果如下

```
$ android create avd --target 1 --name eclair
Android 2.0 is a basic Android platform.
Do you wish to create a custom hardware profile [no]
Created AVD 'eclair' based on Android 2.0
```

### 列出已建立的虛擬機器 ###

我們可以使用 「Android」命令行工具提供的「list avd」命令，來列出所有我們已經建立的模擬器。

在命令行中輸入以下命令：
```
$ android list avd
```
產生的結果如下：
```
$ android list avd
Available Android Virtual Devices:
    Name: eclair
    Path: /Users/mac/.android/avd/cupcake.avd
    Target: Android 2.0 (API level 5)
    Skin: HVGA
```

使用「 android list avd」命令看到有輸出，即表示已成功建立虛擬機器，可以回到 Eclipse 環境來，設定執行應用程式專案所需的環境參數了。


## 移除程式 ##

我們已經順利地啟動了虛擬機器，那麼，該怎麼移除安裝到虛擬機器上的程式哩?

Android SDK 中提供一個 adb (Android Debugger) 命令行工具 (在 android-sdk/tools 中)，我們可以用裡面的 shell 工具連上虛擬機器來移除應用程式。在某些平台上，這些動作可能需要擁有 root 權限才能執行。

首先打開命令列，啟動 adb shell
```
    $ adb shell
```
接著切換到 data/app 目錄中
```
    $ cd data/app/
```
使用 ls 命令(等同 windows 上命令行的 dir 命令)來檢視檔案列表
```
    # ls
    com.example.android.apis.apk
```

接著使用 rm 命令來刪除 ApiDemos 應用程式
```
    # rm com.example.android.apis.apk
    # ls
```

## 移除虛擬機器 ##

我們可以使用「android list avd」命令來列出所有的虛擬機器

```
$ android list avd
Available Android Virtual Devices:
    Name: eclair
    Path: /Users/mac/.android/avd/cupcake.avd
  Target: Android 2.0 (API level 5)
    Skin: HVGA
```

表示現在系統中有一個名為 eclair 的虛擬機器。
我們可以使用「android delete avd --name eclair」命令來刪除名稱為「eclair」的虛擬機器。
```
$ android delete avd --name eclair
AVD 'eclair' deleted.
```
刪除後再次執行「android list avd」命令，得到的結果為
```
$ android list avd
Available Android Virtual Devices:
```

表示系統中已經不存在任何模擬器，我們真的已經將虛擬機器刪除了。