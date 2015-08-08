
```
偉大的創意少之又少，多數時候只是一些小改進。小的改進也是好的。
```

# 什麼是重構 #

可以運作的程式跟可以維護的程式之間，還有一道難以言說的鴻溝。

一個程式設計之初，是用來解決特定問題。就像在前面章節的學習中，我們也已經寫好了一個可以運作的 BMI 程式。但是對程式設計來說，當我們寫越多程式，我們會希望可以從這些程式之中，找到一個更廣泛適用的法則，讓每個程式都清晰易讀，從而變得更好修改與維護。

讓程式清晰易讀有什麼好處呢？當一段程式被寫出來，之後我們所要做的事，就是修改它與維護它。一旦程式越長越複雜，混亂到無法維護的境界時，就只好砍掉重練。
所以若我們能透過某些方式，例如重新組織或部分改寫程式碼，好讓程式容易維護，那麼我們就可以為自己省下許多時間，以從容迎接新的挑戰。

我們回過頭來看看前面所寫的 Android 程式。Android 平台的開發者已經先依照 MVC 模式，為我們將顯示介面所用的 XML 描述檔、顯示資源所用的 XML 描述檔從程式碼中區隔開來。將與程式流程無關的部份分開來組織，讓程式流程更清楚，相對易於維護。

而在主要程式碼(Bmi.java)方面，雖然程式碼量很少，還算好讀，但整體上並不那麼令人滿意。例如，假使我們要在這段程式碼中再多加上按鍵、適用於多種螢幕顯示模式、或是再加入選單等等內容，很快地程式碼就開始變得複雜，變得不容易閱讀，也開始越來越不容易維護。

因此，在繼續新的主題之前，我們先來重構這個 BMI 應用程式。在重構的過程中，也許我們能學到的東西，比學任何新主題還重要哩。


# MVC #

我們打算重構 BMI 程式的部份 java 程式碼。既然我們已經照著 Android 平台的作法，套用 MVC 模式在我們的程式組織上，那麼，我們不妨也試著套用同樣的 MVC 模式在 Bmi.java 程式碼上。

如何套用 MVC 模式到Bmi.java 程式碼上哩？

原來的程式片段是這樣的

```
1  @Override
2  public void onCreate(Bundle savedInstanceState) {
3      super.onCreate(savedInstanceState);
4      setContentView(R.layout.main);
5           
6      //Listen for button clicks
7      Button button = (Button) findViewById(R.id.submit);
8      button.setOnClickListener(calcBMI);
9  }
```

上面的程式片段中，包含了所有 Android 程式共用的標準內容，
整個程式的大致架構在前面章節中已經講解過，現在我們從中取出我們感興趣的部分來討論：

```
Button button = (Button) findViewById(R.id.submit);
button.setOnClickListener(calcBMI);
```

在第7行我們看到一段程式碼來宣告按鈕物件，與針對該按鈕物件作動作的程式碼。
button.setOnClickListener 程式碼的意義是指定一個函式，來負責處理"按下"這個"按鈕"後的動作。

我們可以想像，在同一個畫面中，多加入一些按鈕與欄位後，"onCreate" 這段程式將變得壅腫，我們來試著先對此稍作修改：

首先，我們可以套用 MVC 模式，將宣告介面元件(按鈕、數字欄位)、指定負責函式等動作抽取出來，將 onCreate 函式改寫如下

```
@Override
public void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.main);
    findViews();
    setListeners(); 
}
```

接著我們將宣告介面元件的部份寫成一個獨立的「findViews」函式：

```
private Button calcbutton;
private EditText fieldheight;
private EditText fieldweight;

private void findViews()
{
    calcbutton = (Button) findViewById(R.id.submit);
    fieldheight = (EditText) findViewById(R.id.height);
    fieldweight = (EditText) findViewById(R.id.weight);
}
```

順便將原本很沒個性的按鈕識別參數「button」改名成「calcbutton」，以後在程式中一看到「calcbutton」，就知道是一個按下後將開始處理計算工作的按鈕。

同樣地，我們也將指定特定動作(按按鈕)的負責函式獨立出來：

```
//Listen for button clicks
private void setListeners() {
    calcbutton.setOnClickListener(calcBMI);
}
```

如此一來，我們就將程式邏輯與介面元件的宣告分離開來，達成我們重構的目的。

完整程式如下：
```
package com.demo.android.bmi;

import java.text.DecimalFormat;

import android.app.Activity;
import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.EditText;
import android.widget.TextView;

public class Bmi extends Activity {
    /** Called when the activity is first created. */
    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.main);
        findViews();
        setListeners();
    }

    private Button button_calc;
    private EditText field_height;
    private EditText field_weight;
    private TextView view_result;
    private TextView view_suggest;

    private void findViews()
    {
    	button_calc = (Button) findViewById(R.id.submit);
    	field_height = (EditText) findViewById(R.id.height);
    	field_weight = (EditText) findViewById(R.id.weight);
    	view_result = (TextView) findViewById(R.id.result);
    	view_suggest = (TextView) findViewById(R.id.suggest);
    }

    //Listen for button clicks
    private void setListeners() {
    	button_calc.setOnClickListener(calcBMI);
    }

    private Button.OnClickListener calcBMI = new Button.OnClickListener()
    {
        public void onClick(View v)
        {
            DecimalFormat nf = new DecimalFormat("0.0");
            double height = Double.parseDouble(field_height.getText().toString())/100;
            double weight = Double.parseDouble(field_weight.getText().toString());
            double BMI = weight / (height * height);
            
            //Present result 
            view_result.setText(getText(R.string.bmi_result) + nf.format(BMI));
 
            //Give health advice 
            if(BMI>25){
                view_suggest.setText(R.string.advice_heavy);
            }else if(BMI<20){
                view_suggest.setText(R.string.advice_light);
            }else{
                view_suggest.setText(R.string.advice_average);
            }
        }
    };
}
```

同樣是「calcBMI」 函式，在完整程式中，改將「calcBMI」 函式從原本的「OnClickListener」宣告成 「Button.OnClickListener」。這個改變有什麼差別呢？

閱讀原本的程式碼，在匯入(import)的部分可以看到，「OnClickListener」是來自於「android.view.View.OnClickListener」函式：
```
    import android.view.View.OnClickListener;
```

改成 「Button.OnClickListener」後，「Button.OnClickListener」就變成來自於「android.widget.Button」中的「OnClickListener」函式，在查閱程式時，整個「Button」與「OnClickListener」之間的關係變得更清晰。

另外，我們偷偷將「OnClickListener」中其他會存取到的介面元件識別參數，也補進 findViews 宣告中：
```
private void findViews()
{
    button_calc = (Button) findViewById(R.id.submit);
    field_height = (EditText) findViewById(R.id.height);
    field_weight = (EditText) findViewById(R.id.weight);
    view_result = (TextView) findViewById(R.id.result);
    view_suggest = (TextView) findViewById(R.id.suggest);
}
```

同時，我們也把識別參數的命名方法做了統一：按鈕的識別參數前加上 「button_」前綴，可輸入欄位的識別參數前加上 「field_」前綴，用作顯示的識別參數前則加上「view_」前綴。將變數名稱的命名方法統一有什麼好處呢？
好處在於以後不管是在命名新變數，或是閱讀程式碼時，都能以更快速度命名或理解變數的意義，讓程式變得更好讀。_

我們也把原本在程式中直接寫進的字串

```
TextView result = (TextView) findViewById(R.id.result);
result.setText("Your BMI is "+nf.format(BMI));
```

改寫成

```
//Present result
view_result.setText(getText(R.string.bmi_result) + nf.format(BMI));
```

並將「TextView view\_result」宣告改放到 findViews 中一次處理好。

現在，整個程式流程是不是清爽了許多呢？


< [完成 BMI 程式](BmiLogic.md) | [回目錄](DiveIntoAndroid.md) | [加入對話框](AndroidDialog.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！