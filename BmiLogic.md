至此，我們已經完成了 bmi 程式的介面設計，並且理解了了新建立的程式。剩下我們要做的，只剩下為 BMI 程式加上程式邏輯囉。

很幸運的是，BMI 程式中用到的並不是什麼神秘的演算法，你甚至可以透過搜尋引擎找到中文的範例。


完整的程式如下：
```
1  package com.demo.android.bmi;
2
3  import java.text.DecimalFormat;
4
5  import android.app.Activity;
6  import android.os.Bundle;
7  import android.view.View;
8  import android.view.View.OnClickListener;
9  import android.widget.Button;
10 import android.widget.EditText;
11 import android.widget.TextView;
12
13 public class Bmi extends Activity {
14     /** Called when the activity is first created. */
15     @Override
16     public void onCreate(Bundle savedInstanceState) {
17         super.onCreate(savedInstanceState);
18         setContentView(R.layout.main);
19
20         //Listen for button clicks
21         Button button = (Button)findViewById(R.id.submit);
22         button.setOnClickListener(calcBMI);
23     }
24
25     private OnClickListener calcBMI = new OnClickListener()
26     {
27         public void onClick(View v)
28         {
29             DecimalFormat nf = new DecimalFormat("0.00");
30             EditText fieldheight = (EditText)findViewById(R.id.height);
31             EditText fieldweight = (EditText)findViewById(R.id.weight);
32             double height = Double.parseDouble(fieldheight.getText().toString())/100;
33             double weight = Double.parseDouble(fieldweight.getText().toString());
34             double BMI = weight / (height * height);
35
36             TextView result = (TextView)findViewById(R.id.result);
37             result.setText("Your BMI is "+nf.format(BMI));
38
39             //Give health advice
40             TextView fieldsuggest = (TextView)findViewById(R.id.suggest);
41             if(BMI>25){
42                 fieldsuggest.setText(R.string.advice_heavy);
43             }else if(BMI<20){
44                 fieldsuggest.setText(R.string.advice_light);
45             }else{
46                 fieldsuggest.setText(R.string.advice_average);
47             }
48         }
49     };
50 }
```


我們會學到：導入其他用到的模組、如何取得介面元件、如何對按鈕設定動作。

從上面的完整程式中，我們看到上面介紹到的程式主體都還在，不過也增加了一些內容。這些內容即我們的主要程式邏輯。


# 講解 #

```
//Listen for button clicks
```

兩個反斜線是 java 語言所支援的另一種註解方式。

## 按鈕 ##
```
Button button = (Button)findViewById(R.id.submit);
```

宣告一個 button 實體，透過 findViewById 方法，從資源檔中取得對應的介面元件(按鈕)。這邊取出的是「R.id.submit」按鈕元件。

「R.id.submit」對應到 XML 描述檔的資源是
```
<Button id="@+id/submit"
/>
```
為了確保宣告的型別跟 XML 描述檔中描述的介面元件型別一致，好使程式運作正常，我們在 「findViewById」 方法前加上 「(Button)」修飾，強制將取得的資源型別設成 「button」型別。

```
button.setOnClickListener(calcBMI);
```

這句包含了「Button」類別中的「setOnClickListener」方法。方法中傳入了一個「calcBMI」函式。Android 系統的 UI 互動方式採用常見的事件驅動方式。也就是當使用者按下「button」按鈕的時候，Android 系統會去觸發按鈕的「setOnClickListener」方法中所指定的「calcBMI」函式。

## 觸發事件函式 ##

```
    private OnClickListener calcBMI = new OnClickListener() { 
        public void onClick(View v) {
            …
        }
    };
```

範例中所有的邏輯與運算內容，都放置在這個事件函式中。

當使用者按下按鈕時，即觸發「OnClickListener」類型的事件函式。也有人將這種函式稱為回呼（Call Back）函式，因為是當有動作做完（使用者按下了按鈕），才會呼叫（算出 BMI 值）。

onClick(View v) 是 OnClickListener 中實作的方法，代表按下按鈕時會執行的事件方法。

## 編輯欄位 ##

```
EditText fieldheight = (EditText)findViewById(R.id.height);
EditText fieldweight = (EditText)findViewById(R.id.weight);
```

與上面 button 的宣告類似，只是改成宣告 EditText 實體，透過 findViewById 方法，從資源檔中取得對應的文字欄位元件。這邊取出的是「R.id.height」和「R.id.weight」文字欄位元件。

## 運算 ##

```
double height = Double.parseDouble(fieldheight.getText().toString())/100;
double weight = Double.parseDouble(fieldweight.getText().toString());
double BMI = weight / (height * height);
```

BMI 值的算法是「體重除以身高的平方」。
用計算式來表示，就是

```
體重(weight) / 身高(height)*身高(height)
```

這麼看來，上面的程式碼就很清晰了。我們先從身高欄位(fieldheight)、體重欄位(fieldweight)中取得使用者輸入的身高體重數字，再定義一個雙倍精度浮點數(double) 型態的變數 BMI 來儲存運算的結果，因此，BMI 變數中儲存了運算出來的實際 BMI 值。

## 顯示結果 ##

我們把 BMI 值運算出來了，接著要將結果顯示回螢幕上。

```
TextView result = (TextView)findViewById(R.id.result);
```

為了將結果顯示到螢幕上，在之前 XML 定義檔中我們已經預留了一個名為「result」的 TextView 欄位。在程式碼中，我們再宣告一個 TextView 實體，透過 findViewById 方法，從資源檔中取得對應的介面元件(文字顯示)。這邊取出的就是「R.id.result」介面元件。

```
DecimalFormat nf = new DecimalFormat("0.00");
result.setText("Your BMI is "+nf.format(BMI));
```

透過 java 內建的 DecimalFormat 函式，我們可以將運算結果，以適當的格式顯示。

透過「setText」方法，我們可以將指定的字串，顯示在螢幕上文字類型的介面元件中。

## 顯示建議 ##

「顯示建議」的方式與「顯示結果」完全相同，只有多加了幾個「if」判斷式：當BMI 值大於25顯示過重，小於20顯示過輕。程式碼留給讀者自習。

```
//Give health advice
TextView fieldsuggest = (TextView)findViewById(R.id.suggest);
if(BMI>25){
    fieldsuggest.setText(R.string.advice_heavy);
}else if(BMI<20){
    fieldsuggest.setText(R.string.advice_light);
}else{
    fieldsuggest.setText(R.string.advice_average);
}
```

完整的 BMI 程式動作流程，就是使用者在身高體重欄位中輸入好身高體重後，按下「計算 BMI 值」按鈕，程式根據識別符號，從對應的身高體重欄位讀取輸入的值，並做計算，最後將計算的結果與建議顯示到螢幕上。

< [解讀程式流程](AndroidLogic.md) | [回目錄](DiveIntoAndroid.md) | [重構程式](BmiRefactor.md) >


---


對於本章，您還期望知道什麼樣的內容呢？請在下方提出建議！