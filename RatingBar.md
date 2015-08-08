# XML宣告 #

```
<RatingBar android:id="@+id/rtbar1"
    android:layout_width="wrap_content" 
    android:layout_height="wrap_content" 
    android:rating = "3.5"
    android:numStars="5"
    android:stepSize = "0.5"
    />
```

「android:rating」屬性設定預設數目（可用浮點數）。
「android:numStars」屬性設定星星個數。
「android:stepSize」屬性設定每次點選增加的數目（可用浮點數）。

# Code #

Import
```
import android.widget.RatingBar;
```

Xml Binding
```
final RatingBar rtbar = (RatingBar) findViewById(R.id.rtbar1);
```

設定星星數目

```
rtbar.setNumStars(5);
```

監看選取狀態
```
rtbar.setOnRatingBarChangeListener(new OnRatingBarChangeListener() {
    public void onRatingChanged(RatingBar ratingBar, float rating, boolean fromUser) {
        Log.d("rtbar", "New Rating: " + rating);
    }
});
```

# 參考文件 #

http://developer.android.com/reference/android/widget/RatingBar.html