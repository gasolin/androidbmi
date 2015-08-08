# XML宣告 #

```
<Checkbox android:id="@+id/chk1"
    android:layout_width="wrap_content" 
    android:layout_height="wrap_content" 
    android:text="checkbox"
    />
```


# Code #

Import
```
import android.widget.CheckBox;
```

Xml Binding
```
CheckBox chk=(CheckBox)findViewById(R.id.chk1);
```

設定勾選狀態
```
chk.setChecked(true);
chk.setChecked(false);
```

是否已勾選?
```
chk.isChecked();
```


```
chk.setOnCheckedChangeListener(new CheckBox.OnCheckedChangeListener() { 
    public void onCheckedChanged(CompoundButton buttonView, boolean isChecked) {
        if (isChecked) {
            Log.d("chk", "This checkbox is: checked");
        } else {
            Log.d("chk", "This checkbox is: unchecked");
        }
    })
}
```

# 參考文件 #

http://developer.android.com/reference/android/widget/CheckBox.html