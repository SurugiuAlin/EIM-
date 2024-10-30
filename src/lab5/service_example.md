# Exemplu de serviciu

Un serviciu started este unul pe care o altă componentă îl pornește prin
apelarea `startService()`, care rezultă într-o apelare a metodei
`onStartCommand()` a serviciului.

Când un serviciu este pornit, acesta are un ciclu de viață independent de
componenta care l-a pornit. Serviciul poate rula în background pe termen
nedefinit, chiar dacă componenta care l-a pornit este distrusă. Ca atare,
serviciul ar trebui să se oprească singur când sarcina sa este completă prin
apelarea `stopSelf()`, sau o altă componentă îl poate opri prin apelarea
`stopService()`.

O componentă a aplicației, cum ar fi o activitate, poate porni serviciul prin
apelarea `startService()` și transmiterea unui `Intent` care specifică
serviciul și include orice date pe care serviciul să le folosească. Serviciul
primește acest Intent în metoda `onStartCommand()`.

De exemplu, să presupunem că o activitate trebuie să salveze niște date într-o
bază de date online. Activitatea poate porni un serviciu însoțitor și să-i
livreze datele de salvat prin transmiterea unui intent către `startService()`.
Serviciul primește intent-ul în `onStartCommand()`, se conectează la Internet
și efectuează tranzacția în baza de date. Când tranzacția este completă,
serviciul se oprește singur și este distrus.


```java
public class HelloService extends Service {
  private Looper serviceLooper;
  private ServiceHandler serviceHandler;

  // A handler is a cool class that we can use to send and receive
  // messages between objects. For example, this is a 
  // Handler that receives messages from the thread
  // Combined with a Looper it's a easy way to run some work on a thread and
  // get the results back via the handler.
  private final class ServiceHandler extends Handler {
      public ServiceHandler(Looper looper) {
          super(looper);
      }
      @Override
      public void handleMessage(Message msg) {
          // Normally we would do some work here, like download a file.
          // For our sample, we just sleep for 5 seconds.
          try {
              Thread.sleep(5000);
          } catch (InterruptedException e) {
              // Restore interrupt status.
              Thread.currentThread().interrupt();
          }
          // Stop the service using the startId, so that we don't stop
          // the service in the middle of handling another job
          stopSelf(msg.arg1);
      }
  }

  @Override
  public void onCreate() {
    // Start up the thread running the service. Note that we create a
    // separate thread because the service normally runs in the process's
    // main thread, which we don't want to block. We also make it
    // background priority so CPU-intensive work doesn't disrupt our UI.
    HandlerThread thread = new HandlerThread("ServiceStartArguments",
            Process.THREAD_PRIORITY_BACKGROUND);
    thread.start();

    // Get the HandlerThread's Looper and use it for our Handler
    // The looper is basically the "code" that loops for the thread,
    serviceLooper = thread.getLooper();
    serviceHandler = new ServiceHandler(serviceLooper);
  }

  @Override
  public int onStartCommand(Intent intent, int flags, int startId) {
      Toast.makeText(this, "service starting", Toast.LENGTH_SHORT).show();

      // For each start request, send a message to start a job and deliver the
      // start ID so we know which request we're stopping when we finish the job
      Message msg = serviceHandler.obtainMessage();
      msg.arg1 = startId;
      serviceHandler.sendMessage(msg);

      // If we get killed, after returning from here, restart
      return START_STICKY;
  }

  @Override
  public IBinder onBind(Intent intent) {
      // We don't provide binding, so return null
      return null;
  }

  @Override
  public void onDestroy() {
    Toast.makeText(this, "service done", Toast.LENGTH_SHORT).show();
  }
}
```
