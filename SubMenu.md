子選單可以用在選單和上下文選單

# XML宣告 #

```

```


# Code #

```
import android.view.OptionMenu;
import android.view.MenuItem;
```

Reference
```
protected static final int MENU_ABOUT = Menu.FIRST;

@Override
public boolean onCreateOptionMenu(Menu menu) {
    
    SubMenu about_menu = menu.addSubMenu(0, 0, MENU_ABOUT, 0, "About...");
    menu.add("Web");
    menu.add("Blog");
    return super.onCreateContextMenu(menu);
    }
```