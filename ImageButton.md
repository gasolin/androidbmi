# XML宣告 #
```
<ImageButton android:id="@+id/imgbtn1" 
	android:layout_width="wrap_content" 
	android:layout_height="wrap_content"
        android:src="@drawable/icon"/>
```

# Code #

Import
```
import android.widget.ImageButton;
```


Reference
```
ImageButton imgbtn = (ImageButton)findViewById(R.id.imgbtn1);
```

set Drawable

```
imgbtn1.setImageDrawable(R.drawable.icon);
```

# 不同狀態 #

定義一個 selector 資源, 包含按鈕的各種狀態：
  * 預設狀態 default
  * 選取狀態 focused
  * 按壓狀態 pressed

```
<?xml version="1.0" encoding="utf-8"?>
 <selector xmlns:android="http://schemas.android.com/apk/res/android">
     <item android:state_pressed="true"
           android:drawable="@drawable/button_pressed" /> 
     <item android:state_focused="true"
           android:drawable="@drawable/button_focused" />
     <item android:drawable="@drawable/button_normal" />
 </selector>
```

# 參考文件 #

http://developer.android.com/reference/android/widget/ImageButton.html