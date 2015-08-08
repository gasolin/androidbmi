# XML宣告 #

```
<TextView  android:id="@+id/txt1"
    android:layout_width="fill_parent" 
    android:layout_height="wrap_content" 
    android:text="string"
    />
```


# Code #

Import
```
import android.widget.TextView;
```

Xml Binding
```
TextView txt = (TextView)findViewById(R.id.txt1);
```

## 文字 ##
get text
```
txt.getText().toString();
```

set text
```
txt.setText("any string");
```


## 更多文字類型 ##

```
<TextView  android:id="@+id/txt1"
    android:layout_width="fill_parent" 
    android:layout_height="wrap_content" 
    android:text="string"
    android:textSize="24dp"
    android:textStyle="italic"
    />
```

# 參考文件 #

http://developer.android.com/reference/android/widget/TextView.html