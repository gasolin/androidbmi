# XML宣告 #

```
<ToggleButton android:id="@+id/tglbtn1"
    android:layout_width="wrap_content" 
    android:layout_height="wrap_content" 
    android:textOn="On"
    android:textOff="Off"
    />
```

# Code #

Import
```
import android.widget.ToggleButton;
```

Xml Binding
```
ToggleButton tglbtn=(ToggleButton)findViewById(R.id.tglbtn1);
```

設定勾選狀態
```
tglbtn.setChecked(true);
```
或
```
tglbtn.toggle()
```

是否已勾選?

tglbtn.isChecked()

```
tglbtn.setOnCheckedChangeListener(new ToggleButton.OnCheckedChangeListener() { 
    public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
        if (isChecked) {
            Log.d("tglbtn", "This checkbox is: checked");
        } else {
            Log.d("tglbtn", "This checkbox is: unchecked");
        }
    })
}
```

# 參考文件 #

http://developer.android.com/reference/android/widget/ToggleButton.html