# Utilizarea clasei IntentService

Recursul la clasa
[IntentService](http://developer.android.com/reference/android/app/IntentService.html)
este adecvată în situația în care se dorește implementarea unor servicii
care rulează în fundal, **pe un fir de execuție dedicat** realizând un
set de operații la un moment dat de timp, atunci când sunt solicitate.
În situația în care serviciul este accesat simultan de mai multe
componente ale unei (unor) aplicații Android, procesarea acestora va fi
realizată secvențial.

Un obiect de acest tip este lansat în execuție prin pornirea unui
serviciu și transmiterea unui obiect de tip `Intent` care conține toți
parametrii necesari pentru realizarea sarcinii respective. Toate
operațiile solicitate sunt înregistrate într-o coadă de așteptare și
executate succesiv, prin invocarea automată a metodei
[onHandleIntent()](http://developer.android.com/reference/android/app/IntentService.html#onHandleIntent(android.content.Intent)).
După ce procesarea a fost finalizată, procesul se oprește singur (nu
este necesar să se apeleze metodele `stopSelf()` sau `stopService()`
explicit).


> Clasa `IntentService` oferă o implementare implicită a
metodelor `onStartCommand()` care plasează intenția către coada de
așteptare și invocă metoda `onHandleIntent()` precum și a metodei
`onBind()` care întoarce valoarea `null`.\

Prin urmare, o implementare presupune definirea unei clase derivată din
`IntentService` care suprascrie metoda `onHandleIntent()`, ce primește
ca parametru intenția conținând parametrii ce se doresc a fi procesați,
execuția sa fiind realizată (în mod transparent) pe un fir de execuție
ce rulează în fundal. De asemenea, trebuie furnizat și un constructor
implicit.

``` java
import android.app.IntentService;
import android.content.Intent;

public class SomeStartedService extends IntentService {

  private final String name = "SomeStartedService";

  public SomeIntentService() {
    super(name);
    * ...
  }

  @Override
  protected void onHandleIntent(Intent intent) {
    * ...
  }
}
```

În situația în care este necesar să se suprascrie metodele `onCreate()`,
`onDestroy()` sau `onStartCommand()`, este recomandat să se apeleze și
metodele din clasa părinte, astfel încât ciclul de viață al firului de
execuție pe care sunt realizate procesările să fie actualizat
corespunzător.

``` java
@Override
public int onStartCommand(Intent intent, int flags, int startId) {
  * ...
  return super.onStartCommand(intent, flags, startId);
}
```
