# 從頭建立編譯環境 #

官方文件可在 http://source.android.com/source/initializing.html 找到

## 系統需求 ##

  * 一套 Unix 相容作業系統，如 Ubuntu、Mac OS X（檔案格式要選擇日誌式/區分大小寫）
  * 至少 10G 的硬碟空間
  * RAM 必須超過 1.5G
  * 可連上網路

## 編譯前需知 ##

Android 原始碼相關資源可在 http://source.android.com/ 官方網站找到。

最好選擇 32 位元主機或模擬環境來編譯 Android。本教學以 Ubuntu 9.10 32位元版為例。

因為編譯整個 Android 系統是極度耗系統資源的工作。請讀者不要浪費時間嘗試在 Windows 上編譯 Android 的方法。 在電腦上留下 10 多 G 硬碟空間裝個 Ubuntu Linux 環境然後照著官方教學走，比在 Windows 下裝 Cygwin 並自行摸索簡單多了。


  * 可透過網路更新編譯 Android 必需的套件

```
sudo apt-get update
sudo apt-get install git-core gnupg flex bison gperf libsdl-dev libesd0-dev libwxgtk2.6-dev build-essential zip curl libncurses5-dev zlib1g-dev
```

注意系統上一定得裝 Java 5 的 JDK，因為 Android 尚不支援 java 6 的 JDK。

由於 Sun 已經正式宣布不再支援 Java 5（End of Life），所以 Ubuntu 9.10 等新的發佈套件不再支援 java 5。

在新系統上要安裝 Java 5 的 JDK 最容易的方法是打開 /etc/apt/source.list，將裡面的「karmic」（或任何後續版本代號）改為「jaunty」（9.04），然後執行：

```
sudo apt-get update
```

接著執行 Java 5 SDK 安裝命令，即可順利安裝

```
sudo apt-get install sun-java5-jdk 
```

安裝完可以用以下命令確認安裝是否成功

```
java -version
```

## 下載 Android 原始碼版本管理工具 ##
```
mkdir bin
curl http://android.git.kernel.org/repo >~/bin/repo
chmod a+x ~/bin/repo
```

## 準備映像站目錄 ##

```
mkdir android-mirror
cd android-mirror
~/bin/repo init --mirror -u https://android.googlesource.com/mirror/manifest
~/bin/repo sync
```

## 配置抓取不同版本 ##

同樣命令後面加上分支版本(branch)代號，如要配置成抓取 android-4.0.1\_r1 分支，可用以下命令

```
mkdir mydroid
cd mydroid
~/bin/repo init -u {path}/android-mirror/platform/manifest.git -b android-4.0.1_r1
```

## 下載原始碼 ##

```
~/bin/repo sync
```

## 編譯(預設值) ##

參考 http://source.android.com/source/building.html

```
make
```

以 1.6G 雙核的 CPU 來說，從頭編譯 Android 大概需要 5 小時以上時間。直接打「make」命令編譯好的 ROM 只適合模擬器使用。要編譯能在實機上使用的 ROM 需要另外加上其他參數。

## 啟動模擬器 ##

  * 下載 Android SDK 並解壓縮，並將目錄更名為 android\_sdk

```
cd ~/mydroid/out/target/product/generic
~/android_sdk/tools/emulator -system system.img -data userdata.img -ramdisk ramdisk.img
```


待續...

## 發佈 ##

  * pack/repack bootimage http://android-dls.com/wiki/index.php?title=HOWTO:_Unpack%2C_Edit%2C_and_Re-Pack_Boot_Images
  * skinning how-to http://www.modmygphone.com/forums/showpost.php?p=42091&postcount=1

## Porting ##

  * http://www.kandroid.org/android_pdk/bring_up.html
  * beagle board http://labs.embinux.org/index.php/Android_Porting_Guide_to_Beagle_Board
  * 

## 參考資料 ##

  * Android 自製 ROM 列表 http://db.androidspin.com/android_build_summary.asp
  * 編譯android原始碼到模擬器上執行 http://www.dotblogs.com.tw/neil/archive/2009/04/03/7838.aspx
  * 編譯到機器上執行 http://source.android.com/documentation/building-for-dream
  * Recovery http://forum.xda-developers.com/showthread.php?t=523558
  * Using repo http://source.android.com/download/using-repo
  * JF build environment http://jf.andblogs.net/2009/05/24/jfv151-images-are-out/#more-88
  * http://www.johandekoning.nl/index.php/2009/06/07/building-android-15-build-environment/
  * 訂製 ROM http://www.androidin.net/bbs/thread-36391-1-1.html
  * 相關名詞解釋 http://www.hiapk.com/bbs/thread-126604-1-1.html
  * 刷機原理 http://www.hiapk.com/bbs/thread-53732-1-1.html


---


# 更新 #

# 待整理資料 #

長按 斷話鍵（紅） 關閉機器。

同時按 斷話鍵/Home 鍵 啟動 Recovery

或下命令

$ adb shell reboot recovery

（早期）在 recovery 畫面按 alt+s 來開始 update，按 Home + Back 鍵重啟系統。

（現在）畫面上選擇 reboot system


**http://blog.csdn.net/dong_miao/archive/2009/04/13/4068701.aspx** http://haykuro.theiphoneproject.org/?page_id=35
**Recovery 更新系統 http://android.cool3c.com/article/2482** Nexus One 刷機流程 http://www.mobile01.com/topicdetail.php?f=423&t=1435633&last=17699129

**adp & fastboot http://www.htc.com/www/support/android/adp.html**

**SPL http://code.google.com/p/android-roms/wiki/SPL**

**Partition SD Card http://geeks.pirillo.com/profiles/blogs/how-to-partition-an-sd-card**

**http://forum.xda-developers.com/showthread.php?t=522076**

