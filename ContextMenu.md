長按畫面所彈出的選單。

# XML宣告 #

```

```


# Code #

為上下文選單加入宣告，指定長按後會顯示上下文選單的介面元件。
```
registerForContextMenu(View)
```


Import
```
import android.view.ContextMenu;
import android.view.MenuItem;
```

Reference
```
protected static final int MENU_ABOUT = Menu.FIRST;

@Override
public boolean onCreateContextMenu(Menu menu) {
    menu.add(0, MENU_ABOUT, 0, "About");
    return super.onCreateContextMenu(menu);
    }
```

ContextMenu中不能顯示圖示。

ClickEvent
```
public boolean onContextItemSelected(MenuItem item)
{
    switch(item.getItemId()){
        case MENU_ABOUT:
            //do something
            break;
        }
    return super.onContextItemSelected(item);
}
```