reference
```
mgr=(NotificationManager)getSystemService(NOTIFICATION_SERVICE);
```

Notify
```
Notification note=new Notification(R.drawable.icon,
                                 "notify",
                                 System.currentTimeMillis());

//PendingIntent pi=PendingIntent.getActivity(this, 0, intent,0);
//note.setLatestEventInfo(this, "Tweet!",pi);

mgr.notify(123, note);
```