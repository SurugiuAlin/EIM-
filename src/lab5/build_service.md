# Gestiunea unui Serviciu


Pentru a putea fi utilizat, orice serviciu trebuie să fie declarat în
cadrul fișierului `AndroidManifest.xml`, prin intermediul etichetei
[\<service>](http:*developer.android.com/guide/topics/manifest/service-element.html)
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

Alte atribute ale elementului `<service>` sunt: `android:icon`,
`android:isolatedProcess`, `android:label`, `android:process`.

Un serviciu este o clasă derivată din `android.app.Service` (sau din
subclasele sale), implementând o serie de metode din ciclul de viață al
serviciului. Mai jos avem doua exemple de cod pentru doua tipuri de servicii:

``` java
import android.app.Service;
import android.content.Intent;
import android.os.IBinder;

public class SomeStartedService extends Service {

  private int startMode;

  @Override
  public void onCreate() {
    super.onCreate();
    * ...
  }

  @Override
  public int onStartCommand(Intent intent, 
                            int flags,
                            int startId) {
    * ...
    return startMode;
  }

  @Override
  public IBinder onBind(Intent intent) {
    * ...
    return null;
  }
  
  @Override
  public void onDestroy() {
    super.onDestroy();
    * ...
  }
}
```


``` java
import android.app.Service;
import android.content.Intent;
import android.os.IBinder;

public class SomeBoundedService extends Service {
  
  private IBinder iBinder;
  private boolean allowRebind;

  @Override
  public void onCreate() {
    super.onCreate();
    * ...
  }

  @Override
  public IBinder onBind(Intent intent) {
    * ...
    return iBinder;
  }
  
  @Override
  public boolean onUnbind(Intent intent) {
    * ...
    return allowRebind;
  }
  
  @Override
  public void onRebind(Intent intent) {
    * ...
  }
  
  @Override
  public void onDestroy() {
    super.onDestroy();
    * ...
  }
}
```

Metode din ciclul de viață al serviciului sunt urmatoarele:

-   [onCreate()](http://developer.android.com/reference/android/app/Service.html#onCreate%28%29) -
    realizând operațiile (unice) asociate construirii serviciului
    respectiv (legate de configurarea sa); această metodă este invocată
    doar atunci când este realizată o nouă instanță a serviciului; în
    situația în care serviciul este invocat, însă acesta există deja în
    memorie, metoda nu va mai fi apelată;
-   [onStartCommand()](http://developer.android.com/reference/android/app/Service.html#onStartCommand%28android.content.Intent,%20int,%20int%29) -
    apelată în mod automat, **numai pentru serviciile de tip started**,
    în momentul în care serviciul este invocat printr-un apel al metodei
    `startService()`; serviciul va fi executat imediat după această
    metodă; **este responsabilitatea programatorului să oprească
    serviciul printr-un apel al uneiea dintre metodele `stopSelf()`,
    respectiv `stopService()`**, altfel serviciul va rula pentru o
    perioadă de timp nedefinită; nu este necesar ca metoda să fie
    implementată, dacă serviciul este de tip bounded;
-   [onBind()](http://developer.android.com/reference/android/app/Service.html#onBind%28android.content.Intent%29) -
    apelată în mod automat, **numai pentru serviciile de tip bounded**,
    în momentul în care o componentă a fost atașată unui serviciu
    printr-un apel al metodei `bindService()`; implementarea acestei
    metode trebuie să furnizeze un obiect ce implementează interfața
    [ΙBinder](http:*developer.android.com/reference/android/os/IBinder.html),
    prin intermediul căruia serviciul să poată interacționa cu
    componenta care l-a invocat, punând la dispoziție o anumită
    funcționalitate, descrisă de metode publice; **toate tipurile de
    serviciu trebuie să implementeze această metodă**, însă pentru
    serviciile de tip started, valoarea întoarsă va fi `null`;
-   [onUnbind()](http://developer.android.com/reference/android/app/Service.html#onUnbind%28android.content.Intent%29) -
    apelată în mod automat, **numai pentru serviciile de tip bounded**,
    în momentul în care toate componentele au fost detașate unui
    serviciu;
-   [onRebind()](http://developer.android.com/reference/android/app/Service.html#onRebind%28android.content.Intent%29) -
    apelată în mod automat, **numai pentru serviciile de tip bounded**,
    în momentul în care o componentă a fost atașată unui serviciu după
    ce acesta a fost notificat anterior că toate componentele care îi
    erau asociate au fost detașate (s-a apelat metoda `οnUnbind()`); o
    astfel de metodă va fi invocată numai dacă rezultatul întors de
    metoda `οnUnbind()` este `true`;
-   [onDestroy()](http://developer.android.com/reference/android/app/Service.html#onDestroy%28%29) -
    realizând operațiile asociate distrugerii serviciului respectiv,
    atunci când acesta nu mai este utilizat (a fost oprit sau sistemul
    de operare Android solicită memoria pe care o folosește); în cadrul
    acestei metode sunt eliberate resursele utilizate de serviciu (fire
    de execuție, obiecte, fluxuri de intrare / ieșire).
