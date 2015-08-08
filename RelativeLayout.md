# XML宣告 #

```
<RelativeLayout  
    xmlns:android="http://schemas.android.com/apk/res/android"  
    android:layout_height="fill_parent"  
    android:layout_width="fill_parent">  
    <TextView  
        android:id="@+id/leftobj"  
        android:hint="left of the base"  
        android:layout_alignParentLeft="true"  
        android:layout_width="fill_parent"  
        android:layout_toLeftOf="@+id/base"  
        android:layout_height="wrap_content"></TextView>  
    <TextView 
        android:id="@+id/base" 
        android:text="obj"  
        android:layout_width="wrap_content"  
        android:layout_alignParentRight="true"  
        android:layout_height="wrap_content"></TextView>  
</RelativeLayout> 
```

# Details #

在目標左側
android:layout\_toLeftOf

在目標右側
android:layout\_toRightOf

在目標上方
android:layout\_above

在目標下方
android:layout\_below

## 程式碼宣告 ##

```
    TextView txt1 = new TextView(this);  
    RelativeLayout.LayoutParams params = new RelativeLayout.LayoutParams(LayoutParams.FILL_PARENT,  
    LayoutParams.WRAP_CONTENT);  
    params.addRule(RelativeLayout.ALIGN_PARENT_LEFT);  

    params.addRule(RelativeLayout.LEFT_OF, 1001);  
    txt1.setLayoutParams(params);

    TextView txt2 = new TextView(this);  
    RelativeLayout.LayoutParams params = new RelativeLayout.LayoutParams(LayoutParams. WRAP_CONTENT,  
    LayoutParams.WRAP_CONTENT);  
    params2.addRule(RelativeLayout.ALIGN_PARENT_RIGHT); 
    txt2.setLayoutParams(params2);  
    txt2.setText("obj");
    txt2.setId(1001);  
    
    RelativeLayout layout1 = new RelativeLayout(this);  
    layout1.setLayoutParams(new LayoutParams(LayoutParams.FILL_PARENT, LayoutParams.FILL_PARENT));  
    layout1.addView(txt1);  
    layout1.addView(txt2);  
    setContentView(layout1);
```

# 參考資料 #

  * http://developer.android.com/reference/android/widget/RelativeLayout.html
  * http://developer.android.com/reference/android/widget/RelativeLayout.LayoutParams.html