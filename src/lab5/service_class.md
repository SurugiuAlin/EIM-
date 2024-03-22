# Utilizarea clasei Service

În situația în care este necesar ca serviciul să gestioneze mai multe
solicitări concomitent, se implementează o clasă derivată din `Service`,
definindu-se (intern) o clasă de tip fir de execuție (uzual, se
folosește o instanță a clasei
[Handler](http:*developer.android.com/reference/android/os/Handler.html),
care permite transmiterea de mesaje) pe care vor fi realizate toate
procesările.

``` java
public class SomeStartedService extends Service {
  private Looper looper;
  private ServiceHandler serviceHandler;
  private final static String handlerThreadName = "HandlerThread";

  private final class ServiceHandler extends Handler {
    public ServiceHandler(Looper looper) {
      super(looper);
    }
    
    @Override
    public void handleMessage(Message message) {
      * ...
      stopSelf(message.arg1);
    }
  }

  @Override
  public void onCreate() {
    HandlerThread handlerThread = new HandlerThread(handlerThreadName, Process.THREAD_PRIORITY_BACKGROUND);
    handlerThread.start();
    looper = handlerThread.getLooper();
    serviceHandler = new ServiceHandler(looper);
  }

  @Override
  public int onStartCommand(Intent intent, int flags, int startId) {
    Message message = serviceHandler.obtainMessage();
    message.arg1 = startId;
    serviceHandler.sendMessage(message);
    return START_STICKY;
  }

  @Override
  public IBinder onBind(Intent intent) {
    return null;
  }
}
```

Procesarea este realizată în cadrul metodei
[handleMessage()](http:*developer.android.com/reference/android/os/Handler.html#handleMessage%28android.os.Message%29)
a clasei de tip `Handler`. O instanță a acesteia este creată de fiecare
dată când este invocată metoda
[sendMessage()](http:*developer.android.com/reference/android/os/Handler.html#sendMessage%28android.os.Message%29),
care are drept argument un obiect de tip
[Message](http:*developer.android.com/reference/android/os/Message.html).
Prin intermediul mesajului (obținut ca rezultat al metodei
[obtainMessage()](http:*developer.android.com/reference/android/os/Handler.html#obtainMessage%28%29)
care furnizează o instanță dintr-o colecție globală), trebuie să se
transmită și identificatorul cu care a fost invocat serviciul, astfel
încât acesta să fie transmis către metoda `stopSelf()`, necesară pentru
oprirea serviciului. Astfel, se asigură faptul că serviciul nu se
termină până ce nu este tratată și cea mai recentă invocare a sa.