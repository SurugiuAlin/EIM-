#### Primirea unui intenții cu difuzare

Pentru a putea primi o intenție cu difuzare, o componentă
trebuie să fie înregistrată în acest sens, definind un filtru de
intenții pentru a specifica ce tipuri de acțiuni și ce tipuri de date
asociate intenției poate procesa.

Acesta poate fi precizat:

-   în fișierul `AndroidManifest.xml` (caz în care nu este necesar ca
    aplicația să ruleze la momentul în care se produce evenimentul cu
    difuzare pentru a-l putea procesa); elementul `<receiver>` trebuie
    să conțină în mod obligatoriu filtrul de intenții prin care se
    indică acțiunea care poate fi procesată: 
    ```xml
    <manifest ... >
      <application ... >
        <receiver
          android:name=".SomeEventBroadcastReceiver">
          <intent-filter>
            <action android:name="ro.pub.cs.systems.eim.lab04.SomeAction.SOME_ACTION" />
          </intent-filter> 
        </receiver>
      </application>
    </manifest>
    ```
-   programatic, în codul sursă (caz în care aplicația trebuie să fie în
    execuție la momentul în care se produce evenimentul cu difuzare
    pentru a-l putea procesa); o astfel de abordare este utilă când
    procesarea intenției cu difuzare implică actualizarea unor
    componente din cadrul interfeței grafice asociate activității:
    `private SomeEventBroadcastReceiver someEventBroadcastReceiver = new SomeEventBroadcastReceiver();
    private IntentFilter intentFilter = new IntentFilter(SOME_ACTION);

    ```java
    @Override
    protected void onResume() {
      super.onResume();
      
      registerReceiver(someEventBroadcastReceiver, intentFilter);
    }

    @Override
    protected void onPause() {
      super.onPause();
      
      unregisterReceiver(someEventBroadcastReceiver);
    }
    ```

---

O clasă capabilă să proceseze intenții cu difuzare este derivată din
`android.content.BroadcastReceiver`, implementând metoda `onReceive()`
pe care realizează rutina de tratare propriu-zisă:

``` java
import android.content.BroadcastReceiver;
import android.content.Context;
import android.content.Intent;

public class SomeEventBroadcastReceiver extends BroadcastReceiver {
  @Override
  public void onReceive(Context context, Intent intent) {
    * ...
  }
}
```

Metoda `onReceive()` va fi invocată în mod automat în momentul în care
este primită o intenție cu difuzare, fiind executată pe firul de
execuție principal al aplicației. De regulă, în cadrul acestei metode
utilizatorul este anunțat asupra producerii evenimentului prin
intermediul serviciului de notificare (*Notification Manager*), este
lansat în execuție un serviciu sau sunt actualizate componente din
cadrul interfeței grafice.