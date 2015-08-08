我們都知道，一般人身高的變化程度，比起體重的變化程度小的多。

因此就設計一款 BMI 計算程式來說，如果能在使用者第一次輸入身高體重值後，程式能幫我們預先記住上次輸入過的身高，那麼等到下次啟動程式時，便只需要輸入體重。這麼一來，減少了使用者重複輸入的麻煩，在使用上就更方便了。使用者應該會喜歡這個便利的功能吧。

# 使用偏好設定 #

打開「src/com/demo/android/bmi/Bmi.java」，在「onCreate」和「onPause」中加入「Preference」(偏好設定)相關的程式碼。完整的程式碼如下：

```
public class Bmi extends Activity {
	private static final String TAG = "Bmi";
        public static final String PREF = "BMI_PREF";
	public static final String PREF_HEIGHT = "BMI_Height";
	
    /** Called when the activity is first created. */
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        findViews();
        restorePrefs();
        setListensers();
    }

    // Restore preferences
    private void restorePrefs()
    {
    	SharedPreferences settings = getSharedPreferences(PREF, 0);
    	String pref_height = settings.getString(PREF_HEIGHT, "");
    	if(! "".equals(pref_height))
    	{
    		field_height.setText(pref_height);
    		field_weight.requestFocus();
    	}
    }

......

	@Override
	protected void onPause(){
		super.onPause();
		// Save user preferences. use Editor object to make changes.
		SharedPreferences settings = getSharedPreferences(PREF, 0);
		settings.edit()
		  .putString(PREF_HEIGHT, field_height.getText().toString())
		  .commit();
	}
```

## 講解 ##

### 取得偏好設定 ###


```
    // Restore preferences
    private void restorePrefs()
    {
    	SharedPreferences settings = getSharedPreferences(PREF, 0);
    	String pref_height = settings.getString(PREF_HEIGHT, "");
    	if(! "".equals(pref_height))
    	{
    		field_height.setText(pref_height);
    		field_weight.requestFocus();
        }
    }
```

我們在「onCreate」函式中，加入一行 「restorePrefs」呼叫。並在「onCreate」函式外，再定義一個「restorePrefs」函式如上。

```
SharedPreferences settings = getSharedPreferences(PREF, 0);
```

我們宣告了一個偏好設定（SharedPreferences）型別「settings」，並使用「getSharedPreferences」函式，來尋找系統中有無符合以「BMI\_PREF」字串（PREF 參數）作為檔名的偏好設定檔。如果有符合條件的偏好設定檔存在的話，就將這個偏好設定指定使用「settings」作為代號來操作。如果沒有的話，「getSharedPreferences」函式會回傳空值給「settings」。

```
    String pref_height = settings.getString(PREF_HEIGHT, "");
```

我們可以透過「getXXX」函式，來從偏好設定(SharedPreferences)讀取不同型別的內容。例如本例中使用「getString」來讀取文字類型的資訊。當「PREF\_HEIGHT」偏好設定參數存在時，字串「pref\_height」就會得到偏好設定參數的內容。如果不存在「PREF\_HEIGHT」這個偏好設定參數時，字串「pref\_height」則會得到一個空字串。

```
if(! "".equals(pref_height))
    	{
    		field_height.setText(pref_height);
            ...
        }
```

當「pref\_height」字串存在時，我們將 field\_height 欄位內容設定成偏好設定參數中取出的值。

```
field_weight.requestFocus();
```

同時，因為身高欄位已經預先填好了，使用者只需要再填入體重值即可開始計算自己的 BMI 值。但是當程式一執行，預設的焦點欄位（游標）還是停在「身高」欄位上。因此我們可以在「field\_weight」欄位識別符號上，使用「requestFocus」函式，來手動將焦點欄位改到「體重」欄位上。這樣當使用者要輸入時，如果之前已經輸入過「身高」，那麼程式就會自動幫忙填好上次輸入的身高，並把焦點欄位設置到「體重」欄位上，使用者只需直接輸入體重數字就可以了。

如果只加入了「取得偏好設定」這段的程式碼，就運行模擬器來看看結果，會發現我們寫在「restorePrefs」函式中的程式碼，目前都還沒有發生作用。這是因為我們尚未在程式中儲存任何偏好設定。接著，我們將在程式中加入儲存偏好設定的程式碼，好能在開啟 Activity 時讀到偏好設定。


### 儲存偏好設定 ###

```
    	@Override
	protected void onPause(){
		super.onPause();
		// Save user preferences. use Editor object to make changes.
		SharedPreferences settings = getSharedPreferences(PREF, 0);
		settings.edit()
		  .putString(PREF_HEIGHT, field_height.getText().toString())
		  .commit();
	}
```

當我們使用「Home」、「Back」按鈕或其他方式離開當前的 Activity 時，我們才把身高的值儲存到偏好設定中。根據上一章[活動的生命週期](LifeCycle.md)，我們知道停止當前螢幕動作的狀態是「onPause」狀態。因此我們覆載(Override)了「onPause」函式，在其中加入儲存身高偏好設定的程式碼。「super.onPause」的作用是先將原本的「onPause」函式執行一遍。

```
SharedPreferences settings = getSharedPreferences(PREF, 0);
```

我們宣告了一個偏好設定（SharedPreferences）型別「settings」，並使用「getSharedPreferences」函式，來尋找系統中有無符合以「BMI\_PREF」字串（PREF 參數）作為檔名的偏好設定檔。如果有符合條件的偏好設定檔存在的話，就將這個偏好設定指定使用「settings」作為代號來操作。如果沒有的話，「getSharedPreferences」函式會回傳 0 給「settings」。

```
    settings.edit()
		  .putString(PREF_HEIGHT, field_height.getText().toString())
		  .commit();
```

在此我們串接了三個 settings 擁有的函式：「edit」、「putString」，和「commit」。
要改變偏好設定(SharedPreferences)型別的內容，需要透過「edit」函式來編輯。編輯結束後，要透過「commit」函式來將改變寫到系統中。我們可以透過「putXXX」函式來為偏好設定(SharedPreferences)填入不同型別的內容。例如本例中使用「putString」來寫入文字類型的資訊（讀者也可以試試用 putInt 或 putFloat 函式來直接將身高值儲存成整數或浮點數）。

本例中「putString」函式所執行的動作，是透過「field\_height」介面元件識別符號來取得身高的字串後，將字串儲存到「PREF\_HEIGHT」所代表的偏好設定參數中。


# 參考資料 #

  * http://code.google.com/android/devel/data/preferences.html
  * http://developer.android.com/guide/topics/data/data-storage.html

< [活動的生命週期](LifeCycle.md)  | [回目錄](DiveIntoAndroid.md) | [發佈到 Android 市場(Market)](AndroidMarket.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！