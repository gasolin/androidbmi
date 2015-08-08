# XML宣告 #

```

```


# Code #

Import
```
import android.view.Menu;
import android.view.MenuItem;
```

Reference
```
protected static final int MENU_ABOUT = Menu.FIRST;

@Override
public boolean onCreateOptionsMenu(Menu menu) {
    menu.add(0, MENU_ABOUT, 0, "About").setIcon(android.R.drawable.ic_menu_info_details);
    return super.onCreateOptionsMenu(menu);
    }
```

也可以照著產生「onPrepareOptionsMenu」
```
protected static final int MENU_ABOUT = Menu.FIRST;

@Override
public boolean onPrepareOptionsMenu(Menu menu) {
    menu.clear();
    menu.add(0, MENU_ABOUT, 0, "About").setIcon(android.R.drawable.ic_menu_info_details);
    return super.onPrepareOptionsMenu(menu);
    }
```

「onCreateOptionsMenu」和「onPrepareOptionsMenu」的差別，是「onCreateOptionsMenu」只在讀入Activity時執行一次，而「onPrepareOptionsMenu」則是每次開啟選單時都執行一次。加入「menu.clear」函式可以在每次執行時先清空選單。

ClickEvent
```
public boolean onOptionsItemSelected(MenuItem item)
{
    switch(item.getItemId()){
        case MENU_ABOUT:
            //do something
            break;
        }
    return super.onOptionsItemSelected(item);
}
```