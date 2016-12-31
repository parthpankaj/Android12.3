# Android12.3
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical" >
    <Button
        android:id="@+id/button1"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="@string/notify"
        android:onClick="sendNotification"/>


</LinearLayout>
--------------------------
package com.example.pankaj.animation123;

import android.app.Activity;
import android.app.NotificationManager;
import android.app.PendingIntent;
import android.content.Intent;
import android.os.Bundle;
import android.support.v4.app.NotificationCompat;
import android.view.View;


public class MainActivity extends Activity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);


    }

    public void sendNotification(View view){
        //Creating Notification Builders
        NotificationCompat.Builder myNotificationBuilder = new NotificationCompat.Builder(this);

        //Setting Notification properties
        myNotificationBuilder.setSmallIcon(R.drawable.ic_launcher);
        myNotificationBuilder.setContentTitle("First Notification");
        myNotificationBuilder.setContentText("This is a test notification");
        int notificationid = 3452;

        // Creates an explicit intent for an Activity in your app
        Intent myIntent = new Intent(this, ResultActivity.class);
        myIntent.putExtra("myNotificationId", notificationid);
        myIntent.putExtra("AnyValue", 12345);
        //myIntent.setFlags(Intent.FLAG_ACTIVITY_NEW_TASK | Intent.FLAG_ACTIVITY_CLEAR_TOP);

        PendingIntent myPendingIntent = PendingIntent.getActivity(this, 0, myIntent, PendingIntent.FLAG_UPDATE_CURRENT);

        // start the activity when the user clicks the notification text
        myNotificationBuilder.setContentIntent(myPendingIntent);

        //Issue the Notification
        NotificationManager myManager = (NotificationManager) getSystemService(NOTIFICATION_SERVICE);
        myManager.notify(notificationid, myNotificationBuilder.build());
    }
}
---------------
package com.example.pankaj.animation123;

import android.os.Bundle;
import android.widget.TextView;
import android.app.Activity;
import android.app.NotificationManager;
import android.content.Intent;

public class ResultActivity extends Activity {
    public void onCreate(Bundle savedInstanceState){
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        TextView output = (TextView)findViewById(R.id.textView1);
        Intent myIntent = getIntent();
        int myNotificationId = myIntent.getIntExtra("myNotificationId",-1);

        //Removing notification from top after tap on notification
        if (myNotificationId != -1)
        {
            NotificationManager myManager = (NotificationManager)getSystemService(NOTIFICATION_SERVICE);
            myManager.cancel(myNotificationId);
        }
        output.setText("Data sent by first activity: "+myIntent.getIntExtra("AnyValue", -1));
    }
}
--------------
<resources>
    <string name="app_name">Animation12.3</string>
    <string name="notify">Notify</string>
</resources>
