在[初見 Intent](IntroAndroid.md)一章中，我們已嘗試過使用 「startActivity」函式，傳入適當的「Intent」，來呼叫瀏覽器的 Activity。

到目前為止，我們可以由學習 Android 應用程式的經驗中歸納得出：所有 Android 程式的運作流程，都定義在 Activity 中。

Android 系統與其他系統很不一樣的地方是：它的應用程式並不直接與底層系統緊密結合，而是跑在 Android 框架中。這意思是設計 Android 應用程式時，我們並不需要關心實際上運作的機器是哪一牌的手機或是哪一種嵌入式系統，或使用哪一種架構(ARM、x86、MIPS)。我們要關心的只有Android 框架提供了那些功能，好讓我們能操作這台設備。具體來說就是我們只要知道這台機器的螢幕大小、有沒有鍵盤，有沒有支援 GPS 等等訊息，就知道我們寫的應用程式是否能在這台機器上順暢地運作。Android 框架與底層系統的整合的問題完全可以留給軔體工程師來操心。

在執行「startActivity」函式時，應用程式並不是直接呼叫另一個 Activity，而是將「Intent」(意圖)傳進 Android 框架中。 Android 框架會查看 「startActivity」 呼叫所傳入的動作與 Intent 內容是否在註冊表中，如果符合，就啟動對應的服務或 Activity。

Android 系統中的每一個應用程式，在安裝的過程裡，都得事先在 Android 框架中註冊、登記這個應用程式所建立的 Activity，並事先註明會使用到的服務。譬如當我們在 Android 上安裝我們撰寫的 BMI 應用程式時，BMI 應用程式就會向 Android 框架登記相關資訊：BMI 應用程式將會用到 「Bmi」這個 Activity。

這份訊息存在於每個 Android 應用程式專案根目錄下的「AndroidManifest.xml」檔案中。如果我們在程式裡，要用到其他應用程式或服務所提供的功能，也需一併在此列出。

在安裝應用程式的時候，Android 框架會根據應用程式提供的這份清單，將資訊註冊於 Android 框架的註冊表中。


備註:
> 這麼說其實是不太精確的。Android 應用程式的運作流程，存在於四種載體中：

  1. Activity (活動)
  1. Broadcast Intent Receiver
  1. Service
  1. Content Provider

> 各種載體的相關內容會在後續章節提到時作解說。

## 預設的 Activity 清單 ##

我們使用 eclipse Android 開發工具打開「BMI/AndroidManifest.xml」檔案。切換到「AndroidManifest.xml」分頁標籤，查看預設的 「BMI/AndroidManifest.xml」檔案原始碼：

```
1  <?xml version="1.0" encoding="utf-8"?>
2  <manifest xmlns:android="http://schemas.android.com/apk/res/android"
3      package="com.demo.android.bmi"
4      android:versionCode="1"
5      android:versionName="1.0">
6      <application android:icon="@drawable/icon">
7          <activity android:name=".Bmi" android:label="@string/app_name">
8              <intent-filter>
9                  <action android:name="android.intent.action.MAIN" />
10                 <category android:name="android.intent.category.LAUNCHER" />
11            </intent-filter>
12          </activity>
13     </application>
14     <uses-sdk android:minSdkVersion="X" />
15 </manifest>
```

我們分行講解如下：
```
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
    ....>
    ....
</manifest>
```

「AndroidManifest.xml」這個檔案也是以 XML 格式描述，每個 Android 應用程式都需要一個「AndroidManifest.xml」檔案，每份「AndroidManifest.xml」檔案的開頭都會出現這段敘述。而整個「AndroidManifest.xml」檔案的敘述，都包含在「manifest」(清單)這個主要標籤中。

```
package="com.demo.android.bmi"
```

「package」 是「manifest」(清單)標籤的一個特別屬性，範例中的內容可用來標明，這個應用程式的進入點存在於「com.demo.android.bmi」這個名稱空間/路徑中。

```
android:versionCode="1"
android:versionName="1.0"
```

「android:versionCode」和「android:versionName」是應用程式版本號。
這兩個屬性是可選的(非必要)。
「android:versionName」是給使用者看的版本號，如「1.0」、「2.0」。「android:versionCode」則是開發者用的內部版本號，一般使用流水號。

```
<application android:icon="@drawable/icon" android:label="@string/app_name">
...
</application>
```

「manifest」標籤中主要包含一個「application」標籤(備註1)。「application」標籤裡面，定義了所有這個應用程式用到的 Activity、服務等資訊。「application」標籤中的「android:icon」屬性，定義了這個應用程式將顯示在 Android 主畫面中的應用程式圖示。「android:icon="@drawable/icon"」表示應用程式圖示的資源檔存在於 「res/drawable/icon」 中。圖示的大小必須超過 64x64 像素（Pixel）。「application」標籤中的「android:label」屬性可用來指定應用程式將顯示在 Home 主畫面上的名稱。也就是預設剛開好機時，可以從桌面下方拉出的應用程式列表。

```
<activity android:name=".Bmi" android:label="@string/app_name">
...
</activity>
```
「application」標籤中所有用到的 Activity ，都要包含在一個個「activity」標籤中(備註2)。
Activity 是 Android 應用程式與使用者互動的主要元素，當使用者開啟一個應用程式，第一個看到的畫面就是一個 Activity。若是一個應用程式中包含多個畫面時，會定義多個不同的 Activity，我們也必須在「application」標籤中，使用多個「activity」標籤，為不同的 Activity 添加描述。如果我們已經在程式碼中定義好了 Activity ，卻忘了在「AndroidManifest.xml」檔案中加入對應的「activity」標籤，那麼在執行中呼叫到這個 Activity 的時候，將無法開啟這個 Activity。

「activity」標籤的「android:name」屬性，指出了這個 Activity 所對應的類別(class)。「activity」標籤中的「android:label」屬性可用來指定應用程式將顯示在 Activity 畫面上方的名稱。也可以在程式碼中透過「setTitle(“名稱”)」來動態修改。

因為在上一層「Manifest」標籤屬性中已經定義了「package="com.demo.android.bmi"」，因此在「activity」標籤的 「android:name」屬性中，「.Bmi」代表著「com.demo.android.bmi.Bmi」的簡寫。也可以寫成「Bmi」，一樣是代表「com.demo.android.bmi.Bmi」這個類別。

```
<intent-filter>
    <action android:name="android.intent.action.MAIN" />
    <category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
```

「intent-filter」標籤定義了這個「activity」的性質。
「intent-filter」中主要包含了兩個標籤：「action」跟「category」標籤。
「action」標籤中的「android:name」屬性，其內容「android.intent.action.MAIN」表示：這個 Activity 是此應用程式的進入點（就像程式中常見的 main 主程式），開啟這個應用程式時，應先執行這個 Activity。
。常見的還有「android.intent.action.EDIT」等標籤，會在之後章節用上的時候講解。「category」標籤中的「android:name」屬性，其內容「android.intent.category.LAUNCHER」表示：這個 Activity 將顯示在 Launcher 的應用程式列表中。

我們把整個檔案合到一起看，可以總結出這個檔案所傳達的訊息：在「com.demo.android.bmi」路徑下的「Bmi.java」這個檔案中，已定義了一個主要的 Activity; 當我們打開 Android 的時候，顯示的是位於「res/drawable/icon」的圖示。一旦我們按下圖示來啟動這個應用程式，Android 應用程式框架會去尋找到定義了「android.intent.action.MAIN」內容的 「.Bmi」activity，並呼叫執行。

```
<uses-sdk android:minSdkVersion="X" />
```

Android SDK 1.1 版之後引入了這條敘述，「X」代表了目標版本代號。透過指定這個參數，系統可以依此辨別應用程式是否使用相容的 SDK 版本，好決定能否在這台機器上安裝執行。這也是一個可選填的選項。但如果我們的應用程式要發佈出去，一些強勢的通路如 Google Android Market 已規定所有新發佈的應用程式必須指定「android:minSdkVersion」這個參數。

各目標版本與代號對應表如下:

| 目標版本 | 代號 |
|:-----|:---|
| 3.0          | 11 |
| 2.3.3       | 10 |
| 2.3          | 9  |
| 2.2          | 8  |
| 2.1          | 7  |
| 2.0.1       | 6  |
| 2.0          | 5  |
| 1.6          | 4  |
| 1.5          | 3  |
| 1.1          | 2  |
| 1.0          | 1  |

目前各版本佔有率可以參考官方的版本佔有率圖表：
http://developer.android.com/resources/dashboard/platform-versions.html

這個圖表是根據最近 2 周間連上 Android Market 設備的比率來繪製。

備註1
> 除了「application」標籤外，還有「uses-permission」(例如允不允許存取SMS、能否存取聯絡簿、相機功能)、「permission」、「instrumentation」等主要標籤。相關的內容在後續章節用到時再一併解說。

備註2
> 除了「activity」標籤外，對應於 Android 應用程式的運作流程，還有「service」、「receiver」、「provider」等主要元件。相關內容會在後續章節提到時作解說。

參考資料

  * Android manifest http://developer.android.com/reference/android/R.styleable.html#AndroidManifest
  * Intent Action http://developer.android.com/reference/android/content/Intent.html

< [加入選單](AndroidMenu.md) | [回目錄](DiveIntoAndroid.md) | [加入新 Activity](AndroidActivity.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！