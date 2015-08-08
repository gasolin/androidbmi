# XML宣告 #

由上而下的版面配置
```
<LinearLayout
    android:orientation="vertical"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    >
    <!-- contained widgets -->
</LinearLayout>
```


由左而右的版面配置
```
<LinearLayout
    android:orientation="horizontal"
    android:layout_width="fill_parent"
    android:layout_height="fill_parent"
    >
    <!-- contained widgets -->
</LinearLayout>
```

# 程式碼宣告 #
```
LinearLayout layout = new LinearLayout(this);
layout.setLayoutParams(new LayoutParams(LayoutParams.FILL_PARENT,
                                         LayoutParams.FILL_PARENT));
layout.setOrientation(LinearLayout.VERTICAL);
    
TextView txt1 = new TextView(this);     
txt1.setText("hello");		
layout.addView(txt1);
```

# 參考資料 #

  * http://developer.android.com/reference/android/widget/LinearLayout.html
  * http://developer.android.com/reference/android/widget/LinearLayout.LayoutParams.html