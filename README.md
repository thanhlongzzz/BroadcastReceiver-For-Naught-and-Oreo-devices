# BroadcastReceiver-For-Naught-and-Oreo-devices
Broadcast Receiver for naught and oreo+ devices . getting all the actions performed by device at one place.
working on all devices get all Actions at place for :-
1.Power Connected
2.Power disconnected
3.Screen On
4.Screen off
5.Network connectivity change 

You can add other action according to your need .

Class MyReceiver
```
@BroadcastReceiverActions({
        "android.intent.action.SCREEN_ON",
        "android.intent.action.SCREEN_OFF",
        "android.intent.action.DREAMING_STARTED",
        "android.intent.action.DREAMING_STOPPED",
        "android.intent.action.ACTION_POWER_DISCONNECTED",
        "android.intent.action.ACTION_POWER_CONNECTED",
        "android.net.conn.CONNECTIVITY_CHANGE"
})
public class MyReceiver extends BroadcastReceiver {
    public MyReceiver() {
        super();
    }
    @Override
    public void onReceive(Context context, Intent intent) {
        Session.getGlobalReceiverCallBack(context, intent);
        //Log.e("dfd", "" + intent.getAction());
    }
}
```
Class AppController

```public class AppController extends Application {
    private BroadcastReceiver receiver;
    MyReceiver mR;

    @Override
    public void onCreate() {
        super.onCreate();
        mR = new MyReceiver();
        receiver = DynamicReceiver.with(mR)
                .register(this);
    }
}
```
Class MainActivity
```public class MainActivity extends AppCompatActivity implements GlobalReceiverCallBack {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        Session.setmGlobalReceiverCallback(this);

    }

    @Override
    public void onCallBackReceived(Context context, Intent intent) {

        Toast.makeText(context, "" + intent.getAction(), Toast.LENGTH_LONG).show();
    }
}
```
