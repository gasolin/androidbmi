
```
維護一個 Activity 的生命週期非常重要，因為 Activity 隨時會被系統回收掉。
```

## 生命週期 ##

作者在初級章節中一直努力地傳達給讀者：編寫 Android 平台的基本應用程式，跟編寫桌面應用程式的難度，兩者並沒什麼不同。甚至因為 Android 平台擁有免費、跨平台的開發工具，使得 Android 平台應用程式的開發更為單純。

但是請別忘了，Android 平台也是個手機作業系統。撇掉其他功能不談，手機的特性，就是應該能隨時在未完成目前動作的時候，離開正在使用的功能，切換到接電話、接收簡訊模式...而且在接完電話回來應用程式時，還希望能看到一樣的內容。

現在使用者使用智慧型手機，大多已習慣使用多工(Multi-Task)的作業系統(如 Windows Mobile)，可以在用手機聽音樂的同時，也執行其他多個程式。同時執行多個程式有它的明顯好處，但是也有它的嚴重的缺點。每多執行一個應用程式，就會多耗費一些系統記憶體。而手機裡的記憶體是相當有限的。當同時執行的程式過多，或是關閉的程式沒有正確釋放掉記憶體，執行系統時就會覺得越來越慢，甚至不穩定。

為了解決這個問題， Android 引入了一個新的機制 -- 生命週期 (Life Cycle)。

### 行程 ###

應用程式（一個個 Activity）執行的狀態稱為行程(process)。在 Android 作業系統中，每個應用程式都是一個行程。Android 系統平台(準確的說是 Dalvik 虛擬機)會維護一個唯一的 Activity 歷史記錄堆疊，並從旁觀察每個應用程式行程。系統平台會依照系統的記憶體狀況，與 Activity 的使用狀態，來管理記憶體的使用。

Activity 類別除了負責運行程式流程，與操作介面元件之外，最重要的，就是它提供了開發者控制行程生命週期的函式。我們已經相當習慣在 OnCreate (建立行程時的行為)函式中，加入我們對這個 Activity 執行流程的控制。在前面遇到的範例中，我們並不需要對除了 OnCreate 之外的行為做出改變。不過理解行程的生命週期，將為我們繼續深入 Android 開發打下基礎。

### 為什麼要了解生命週期 ###

Android 應用程式的生命週期是由 Android 框架進行管理，而不是由應用程式直接控制。

通常，每一個應用程式（入口一般會是一個 Activity 的 onCreate 方法），都會佔據一個行程(Process)。當系統記憶體即將不足的時候，會依照優先級自動進行行程(process)的回收。不管是使用者或開發者，都無法確定的應用程式何時會被回收。

一個 Activity 類別除了 OnCreate 函式之外，還預先定義了 OnPause(暫停行程時的行為)、OnResume(繼續行程時的行為)等等的基本行為，當從一個 Activity 切換到另一個 Activity 的時候，原本的 Activity 將經過一連串的狀態改變。開發者可以在程式中添加一些各狀態相對應的流程，每次 Activity 改變狀態時，就會執行相對應的流程。

要讓使用者有好的使用經驗，Activity 需要在各個週期點上負責保管狀態、恢復狀態、傳送資料等工作。

## Activity 的狀態 ##

Android 的虛擬機(VM)執行Activity時主要有四種狀態：

  * Active (活動)
  * Paused (暫停)
  * Stopped (停止)
  * Dead (已回收或未啟動)

### Active (活動) ###

「Active」狀態是使用者啟動應用程式或 Activity 後，Activity 運行中的狀態。

在 Android 平台上，同一個時刻只會有一個 Activity 處於活動(Active)或運行(Running)狀態。其他的 Activity 都處於未啟動(Dead)、停止(Stopped)、或是暫停(Pause)的狀態。

### Paused (暫停) ###

「Paused」狀態是當 Activity 暫時暗下來，退到背景畫面的狀態。

當我們使用Toast、AlertDialog、或是電話來了時，都會讓原本運行的 Activity 退到背景畫面。新出現的Toast、AlertDialog等介面元件蓋住了原來的 Activity 畫面。Activity 處在「Paused」狀態時，使用者無法與原 Activity 互動。

### Stopped (停止) ###

「Stopped」狀態是有其他 Activity 正在執行，而這個 Activity 已經離開螢幕，不再動作的狀態。

透過長按「Home」鈕，可以叫出所有處於「Stopped」狀態的應用程式列表。

在「Stopped」狀態的 Activity，還可以透過「Notification」來喚醒。「Notification」會在後面章節中解說。

### Dead (已回收或未啟動) ###

「Dead」狀態是 Activity 尚未被啟動、已經被手動終止，或已經被系統回收的狀態。

要手動終止 Activity，可以在程式中呼叫「finish」函式。我們在[加入選單](AndroidMenu.md)一章中已經提到過了。

如果是被系統回收，可能是因為記憶體不足了，所以系統根據記憶體不足時的回收規則，將處於「Stopped」狀態的 Activity 所佔用的記憶體回收。

## 記憶體不足時的行為 ##

記憶體不足時，Dalvik 虛擬機會根據其記憶體回收規則來回收記憶體：

  1. 先回收與其他 Activity 或 Service/Intent Receiver 無關的行程(即優先回收獨立的Activity)
  1. 再回收處於「Stopped」狀態的其他類型 Activity（在背景等待的Activity）。最久沒有使用的 Activity 優先回收（比較官方的說法是 "根據 LRU 演算法..."）
  1. 還不夠？回收 Service 行程
  1. 快不行啦，關掉可見的 Activity/行程
  1. 關閉當前的 Activity

當系統缺記憶體缺到開始「4. 關掉可見的 Activity/行程」時，大概我們換機子的時機也早該到啦！

## 觀察 Activity 運作流程 ##

講了這麼多虛的，我們可以寫一些程式來直觀查看 Activity 的運作流程嗎？

當然可以。在上一章[記錄與偵錯 (Log)](AndroidDebug.md)中，我們學到的「Log」工具，正好可以在查看 Activity 的運作流程時派上用場。

打開「src/com/demo/android/bmi/Bmi.java」，在程式中加入一些「Log」記錄點：

```
public class Bmi extends Activity {
	private static final String TAG = "Bmi";

    public void onCreate()
    {
        super.onCreate(...);
        Log.v(TAG,"onCreate");
    }
    
    public void onStart()
    {
        super.onStart();
        Log.v(TAG,"onStart");
    }
    
    public void onResume()
    {
        super.onResume();
        Log.v(TAG,"onResume");
    }
    
    public void onPause()
    {
        super.onPause();
        Log.v(TAG,"onPause");
    }
    
    public void onStop()
    {
        super.onStop();
        Log.v(TAG,"onStop");
    }    
    
    public void onRestart()
    {
        super.onRestart();
        Log.v(TAG,"onReStart");
    }

    public void onDestroy()
    {
        super.onDestroy();
        Log.v(TAG,"onDestroy");
    }
    
}
```

### 講解 ###

我們為 Activity 的各個狀態加入了「Log」記錄訊息。當模擬器運行時，我們可以透過 「LogCat」工具來查看 Activity 所處在的狀態。

上面的七個狀態又可以歸納成三組：

1. 資源分配 (Create/Destroy)

完整的 Activity 生命週期由「Create」狀態開始，由「Destroy」狀態結束。
建立(Create)時分配資源，銷毀(Destroy)時釋放資源。

2. 可見與不可見(Start/ReStart/Stop)

當 Activity 運行到「Start」狀態時，就可以在螢幕上看到這個 Activity。相反地，當Activity 運行到「Stop」狀態時，這個 Activity 就會從螢幕上消失。

當使用者按下 Back 按鈕回到上一個 Activity 時，會先到 Restart 狀態，再到一般的 Start 狀態。

3. 使用者能否直接存取螢幕（Resume/Pause）

當有個 Toast、AlertDialog、簡訊、電話等訊息亂入時，原來的 Activity 會進入「Pause」狀態，暫時放棄直接存取螢幕的能力，被中斷到背景去，將前景交給優先級高的事件。當這些優先級高的事件處理完後，Activity 就改進入「Resume」狀態，此時又直接存取螢幕。

## Activity 運作流程 ##

由實際運行的記錄來看，我們可以歸納出所有 Android 應用程式都遵循的動作流程：

### 一般啟動 ###
```
onCreate -> onStart -> onResume
```

啟動一個 Activity 的基本流程是：分配資源給這個 Activity（Create 狀態），然後將 Activity 內容顯示到螢幕上（Start 狀態）。在一切就緒後，取得螢幕的控制權（Resume 狀態），使用者可以開始使用這個程式。

### 呼叫另一個 Activity ###
```
onPause(1) -> onCreate(2) -> onStart(2) - onResume(2) -> onStop(1)
```
這是個先凍結原本的 Activity，再交出直接存取螢幕能力（Pause 狀態）的過程。
直到 Activity 2 完成一般啟動流程後，Activity 1 才會被停止。

### 回原 Activity ###
```
onPause(2) -> onRestart(1) -> onStart(1) -> onResume(1) -> onStop(2) -> onDestroy(2)
```

點 Back 按鈕可以回到原本的 Activity。

### 退出結束 ###
```
onPause -> onStop -> onDestroy
```

如果程式中有直接呼叫「finish」函式來關閉 Activity的話，系統假設我們很確定我們在做什麼，因此會直接跳過先凍結(Freeze)的階段，暫停(Pause)，停止(Stop)，然後銷毀(Destroy)。

### 回收後再啟動 ###

```
    onCreate -> onStart -> onResume
```

被回收掉的 Activity 一旦又重新被呼叫時，會像一般啟動一樣再次呼叫 Activity 的 onCreate 函式。

當我們使用「Android」手機一陣子，在手機上已經執行過多個應用程式。只要按下「Back」（返回）鍵，「Android」就會開啟最近一次開啟過的 Activity。

這時我們要是按下多次「Back」（返回）鍵，理論上遲早會返回到某個已經銷毀（Destroy）的 Activity。這時會發生什麼事呢？

如果應該開啟的 Activity 已經被回收了，那麼這個 Activity 會再次被建立（Create）出來。再次被建立出來的 Activity，當然會跟原本我們開啟過的 Activity 不一樣啦。

所以如果要讓再次被建立出來的 Activity 看起來跟原本開啟過的一樣，那麼在 Activity 之間切換時，我們就要留意保留資料：最好在每次 Activity 運行到「onPause」或「onStop」狀態時先保存資料，然後在「onCreate」時將資料讀出來。

我們可以使用下章介紹到的「Preference」（偏好設定）等方法來記錄之前運作時的資料或設定。

# 參考資料 #

  * Activity Cycle ![http://code.google.com/android/images/activity_lifecycle.png](http://code.google.com/android/images/activity_lifecycle.png)
  * Activity 的生命週期 http://blog.csdn.net/sharetop/archive/2007/12/16/1941935.aspx

< [記錄與偵錯 (Log)](AndroidDebug.md)  | [回目錄](DiveIntoAndroid.md) | [儲存資訊](AndroidPreference.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！