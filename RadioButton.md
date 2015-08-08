# XML宣告 #

```
<RadioGroup android:id="@+id/rdg1"
        android:orientation="vertical"
        android:layout_width="fill_parent"
        android:layout_height="fill_parent"
        >
        <RadioButton android:id="@+id/rdo1"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="choice 1" />
        <RadioButton android:id="@+id/rdo2"
                android:layout_width="wrap_content"
                android:layout_height="wrap_content"
                android:text="choice 2" 
                android:checked="true" 
                />
</RadioGroup>
```

「android:checked」屬性可用來設定預設狀態

# Code #

Import
```
import android.widget.RadioGroup;
```

XML Binding
```
RadioGroup rdg=(RadioGroup)findViewById(R.id.rdg1);
```

```
rdg.setOnCheckedChangeListener(new RadioGroup.OnCheckedChangeListener() {
    public void onCheckedChanged(RadioGroup group, final int checkedId) {
        switch (checkedId) {
            case R.id.rdo1:
                //do something
                break;
            case R.id.rdo2:
                //do something
                break;
            }
    });
}
```

# 參考文件 #

http://developer.android.com/reference/android/widget/RadioButton.html
http://developer.android.com/reference/android/widget/RadioGroup.html