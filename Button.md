# XML宣告 #

```
<Button  android:id="@+id/btn1"
    android:layout_width="fill_parent" 
    android:layout_height="wrap_content" 
    android:text="button"
    />
```


# Code #

Import
```
import android.widget.Button;
import android.view.View;
```

Xml Binding
```
Button btn = (Button)findViewById(R.id.btn1);
```

## 文字 ##
get text
```
btn.getText().toString();
```

set text
```
btn.setText("any string");
```

## Call back ##
in onCreate
```
btn.setOnClickListener(callBack);
```

Callback function
```
private Button.OnClickListener callBack = new Button.OnClickListener() {
    @Override
    public void onClick(View v)
    {
        //actions
    }
};
```


# 參考文件 #

http://developer.android.com/reference/android/widget/Button.html