# XML宣告 #

```
<EditText  android:id="@+id/edt1"
    android:layout_width="fill_parent" 
    android:layout_height="wrap_content" 
    android:text="string"
    />
```


# Code #

Import
```
import android.widget.EditText;
```

Xml Binding
```
EditText edt = (EditText)findViewById(R.id.edt1);
```

## 文字 ##
get text
```
edt.getText().toString();
```

set text
```
edt.setText("any string");
```

# 參考文件 #

http://developer.android.com/reference/android/widget/EditText.html