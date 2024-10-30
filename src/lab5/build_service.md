# Gestiunea unui Serviciu

Pentru a crea un serviciu, trebuie să creezi o subclasă a `Service` sau să folosești una dintre subclasele existente ale acesteia. În implementare, trebuie să suprascrii câteva metode callback care gestionează aspecte cheie ale ciclului de viață al serviciului și să oferi un mecanism care permite componentelor să se lege de serviciu, dacă este cazul.


``` java
import android.app.Service;
import android.content.Intent;
import android.os.IBinder;

public class SomeStartedService extends Service {

  private int startMode;

  @Override
  public void onCreate() {
    super.onCreate();
    // ...
  }

  @Override
  public int onStartCommand(Intent intent, 
                            int flags,
                            int startId) {
    // start a new thread here and run your code
    // from here you can send broadcasts to update the UI in a interface
    return startMode;
  }

  @Override
  public IBinder onBind(Intent intent) {
    // ...
    return null;
  }
  
  @Override
  public void onDestroy() {
    super.onDestroy();
    // ...
  }
}
```

Acestea sunt cele mai importante metode callback pe care ar trebui să le suprascrii:

-   [onCreate()](http://developer.android.com/reference/android/app/Service.html#onCreate%28%29) -
    Sistemul invocă această metodă pentru a efectua proceduri de configurare care au loc o singură dată când serviciul este creat inițial (înainte de a apela fie `onStartCommand()` sau `onBind()`). Dacă serviciul rulează deja, această metodă nu este apelată.

-   [onStartCommand()](http://developer.android.com/reference/android/app/Service.html#onStartCommand%28android.content.Intent,%20int,%20int%29) -
    Sistemul invocă această metodă prin apelarea `startService()` când o altă componentă (cum ar fi o activitate) solicită pornirea serviciului. Când această metodă se execută, serviciul este pornit și poate rula în background pe termen nedefinit. Dacă implementezi această metodă, este responsabilitatea ta să oprești serviciul când munca sa este completă prin apelarea `stopSelf()` sau `stopService()`. **Dacă dorești doar să oferi binding, nu trebuie să implementezi această metodă.**
    
-   [onBind()](http://developer.android.com/reference/android/app/Service.html#onBind%28android.content.Intent%29) -
    Sistemul invocă această metodă prin apelarea `bindService()` când o altă componentă dorește să se lege de serviciu (cum ar fi pentru a efectua Remote Procedure Calls (RPC)). În implementarea acestei metode, trebuie să oferi o interfață pe care clienții o folosesc pentru a comunica cu serviciul prin returnarea unui `IBinder`. Trebuie să implementezi întotdeauna această metodă; totuși, dacă nu dorești să permiți binding-ul, ar trebui să returnezi null.

-   [onDestroy()](http://developer.android.com/reference/android/app/Service.html#onDestroy%28%29) -
    Sistemul invocă această metodă când serviciul nu mai este folosit și urmează să fie distrus. Serviciul tău ar trebui să implementeze această metodă pentru a elibera orice resurse precum thread-uri, listeners înregistrați sau receivers. Aceasta este ultima apelare pe care serviciul o primește.


### Declararea unui serviciu în manifest

Pentru a putea fi utilizat, orice serviciu trebuie să fie declarat în
cadrul fișierului `AndroidManifest.xml`, prin intermediul etichetei
[\<service>](http://developer.android.com/guide/topics/manifest/service-element.html)
în cadrul elementului
[\<application>](http:*developer.android.com/guide/topics/manifest/application-element.html).
Eventual, se poate indica o permisiune necesară pentru pornirea și
oprirea serviciului, astfel încât aceste operații să poată fi realizate
numai de anumite aplicații Android.

``` xml
<manifest ...>
  <application ...>
    <service
      android:name="ro.pub.cs.systems.eim.lab05.SomeService"
      android:enabled="true"
      android:exported="true"
      android:permission="ro.pub.cs.systems.eim.lab05.SOME_SERVICE_PERMISSION" />
  </application>
</manifest>
```

Intalnim mai multe campuri de configurare posibile:

* `android:name`
este singurul **obligatoriu** în cadrul elementului `<service>`,
desemnând clasa care gestionează operațiile specifice serviciului
respectiv. Din momentul în care aplicația Android este publicată,
această valoare nu mai poate fi modificată, întrucât poate avea un efect
asupra componentelor care utilizează acest serviciu prin intermediul
unei intenții explicite folosită la pornirea serviciului sau la
asocierea componentei cu serviciul respectiv.


* `android:enabled` indică dacă serviciul poate fi instanțiat de
către sistemul de operare.

* `android:exported` specifică posibilitatea ca alte componente
(aparținând altor aplicații) să poată interacționa cu serviciul. În
situația în care serviciul nu conține filtre de intenții, acesta poate
fi invocat numai prin precizarea explicită a numelui clasei care îl
gestionează (calificată complet), valoarea sa fiind `false`, fiind
destinat invocării din contextul unor componente aparținând aceleiași
aplicații Android ca și el. În cazul în care serviciul definește cel
puțin un filtru de intenții, valoarea sa este `true`, fiind destinat
invocării din contextul altor aplicații Android.

* `android:permission` precizează denumirea unei permisiuni pe
care entitatea trebuie să o dețină pentru a putea lansa în execuție un
serviciu sau pentru a i se putea asocia. Aceasta trebuie indicată în
cadrul intențiilor transmise ca argumente metodelor utilizate pentru a
invoca serviciul respectiv (`startService()`, respectiv
`bindService()`), altfel intenția respectivă nu va fi livrată către
serviciu.
