# XML宣告 #

# Code #

Import
```
import android.app.AlertDialog;
import android.content.DialogInterface;

```

Open Dialog
```
new AlertDialog.Builder(this)
    .setTitle("Title")//.setView(view)
    .setMessage("About")
    .setPositiveButton("OK",
        new DialogInterface.OnClickListener(){
            public void onClick(
                DialogInterface dialoginterface, int i){
                }
            })
    .setNegativeButton("Cancel",
        new DialogInterface.OnClickListener(){
            public void onClick(
                DialogInterface dialoginterface, int i){
                }
            })
    .show();
```