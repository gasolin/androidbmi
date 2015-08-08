# XML宣告 #
```
<ImageView android:id="@+id/img1" 
	android:layout_width="wrap_content" 
	android:layout_height="wrap_content"
        android:src="@drawable/icon"/>
```

# Code #

Import
```
import android.widget.ImageView;
```


Reference
```
ImageView img = (ImageView)findViewById(R.id.img1);
```

set Drawable
```
Drawable imgPic = new Drawable.createFromPath(pathName);
img1.setImageDrawable(imgPic);
```


# 參考文件 #

http://developer.android.com/reference/android/widget/ImageView.html