# Threads

Când o aplicație este lansată, sistemul creează un thread de execuție pentru
aplicație, numit **thread principal**. Acest thread este foarte important,
deoarece este responsabil cu dispecerizarea evenimentelor către widget-urile
corespunzătoare ale interfeței utilizator, inclusiv evenimentele de desenare.
De asemenea, este aproape întotdeauna thread-ul în care aplicația ta
interacționează cu componentele din pachetele android.widget și android.view
ale kit-ului UI Android. Din acest motiv, thread-ul principal este numit uneori
thread-ul UI. Totuși, în circumstanțe speciale, thread-ul principal al unei
aplicații ar putea să nu fie thread-ul său UI.

Din cauza acestui model cu un singur thread, este vital pentru receptivitatea
interfeței utilizator a aplicației tale să nu blochezi thread-ul UI. Dacă ai
operații de efectuat care nu sunt instantanee, asigură-te că le faci în
thread-uri background sau worker separate. Doar ține minte că nu poți actualiza
interfața utilizator din niciun alt thread în afară de thread-ul UI sau
thread-ul principal.

Acesta este un exemplu simplu de cum putem folosi declara un thread.
```java
public class ProcessingThread extends Thread {
  // we can pass data to the thread through the constructor
  public ProcessingThread() {
  }

  @Override
  public void run() {
    while(true){ 
        // we perform some work on the thread
    }
  }
}
```

Pentru a il folosi dintr-un serviciu vom face astfel:

```java
@Override
public int onStartCommand(Intent intent, int flags, int startId) {
    Log.d(Constants.TAG, "onStartCommand() method was invoked");
    ProcessingThread processingThread = new ProcessingThread();
    processingThread.start();
}
```
