## Manifest

```Java
    
    <application
        android:allowBackup="true"
        android:icon="@mipmap/ic_launcher"
        android:label="@string/app_name"
        android:roundIcon="@mipmap/ic_launcher_round"
        android:supportsRtl="true"
        android:theme="@style/Theme.BroadcastMessages">
        <receiver
            android:name=".MessageReceiver"
            android:enabled="true"
            android:exported="true">
            <intent-filter>
                <action android:name="com.example.broadcastmessages.action.ACTIONWHO" />
            </intent-filter>
```

## MainActivity

```Java
public class MainActivity extends AppCompatActivity {
    public static final String ACTION_WHO= "com.example.broadcastmessages.action.ACTIONWHO";

    public static final String MESSAGE = "Привет!";

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
    public void sendMessage(View view){
        Intent intent = new Intent();
        intent.setAction(ACTION_WHO);
        intent.putExtra("com.example.broadcastmessages.broadcast.Message", MESSAGE);
        intent.addFlags(Intent.FLAG_INCLUDE_STOPPED_PACKAGES);
        intent.setComponent(new ComponentName(this, MessageReceiver.class));
        sendBroadcast(intent);


    }
}

```

## Message

```Java

public class MessageReceiver extends BroadcastReceiver {

    @Override
    public void onReceive(Context context, Intent intent) {
        Toast.makeText(context, "Сообщение: " +
                        intent.getStringExtra("com.example.broadcastmessages.broadcast.Message"),
                Toast.LENGTH_LONG).show();
    }

}

```

## How it works

