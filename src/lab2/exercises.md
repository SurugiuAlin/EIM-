# Activitate de Laborator

**1.** În contul de Gitlab de la facultate, să se creeze un depozit denumit
'Laborator02' in care vom pune aplicatia la care vom lucra astazi.

- Să se cloneze [scheletul laboratorului](https://github.com/eim-lab/Laborator02).
- Să se încarce conținutul descărcat în cadrul depozitului `Laborator02` de pe contul Gitlab personal.
Ne intereseaza doar folder-ul `labtasks`.

> Daca aveti o eroare legata de `--add-exports=java.base/sun.nio.ch=ALL-UNNAMED`, va trebui sa
stergeti toate linile cu `--add-exports` din `gradle.properties`.

**2.** Să se încarce în mediul integrat de dezvoltare Android Studio
proiectul `ActivityLifecycleMonitor`, folosind opțiunea *Open an
Existing Android Studio Project*.

**3.** În clasa `LifecycleMonitorActivity` din pachetul
`ro.pub.cs.systems.eim.lab02.activitylifecyclemonitor.graphicuserinterface`,
să se suprascrie metodele care monitorizează ciclul de viață al unei
activități; fiecare dintre acestea va trebui **să apeleze metoda
părinte** și **să notifice apelarea sa prin intermediul unui mesaj**,
având prioritatea `DEBUG` și eticheta
`activitylifecyclemonitor`:`Log.d(Constants.TAG, "??? method was invoked");
`

      - onRestart()
      - onStart()
      - onResume()
      - onPause()
      - onStop()
      - onDestroy()

**3.** Daca ne uitam in Logcat cand ruleaza aplicatia, o sa vedem foarte multe mesaje. 
Vom filtra in LogCat să afișeze doar mesajele care au eticheta
`activitylifecycle`, generate de aplicația
`ro.pub.systems.eim.lab02.activitylifecyclemonitor` și au cel puțin
prioritatea `debug`.

**4.** Să se modifice mesajul din metoda `onCreate()`, astfel încât să
se indice dacă activitatea a mai fost lansată în execuție anterior sau
nu (dacă există o stare a activității care trebuie restaurată).

**5.** Să se inspecteze mesajele care sunt generate la producerea
următoarelor evenimente:

      - se apasă butonul *Home*
      - se apasă butonul *Back*
      - se apasă butonul *OK* din cadrul aplicației (indiferent dacă datele de autentificare sunt corecte sau nu)
      - se apasă butonul *lista app* 


<details>
  <summary>genymotion, Nexus 5X API 24, butoane "hardware"</summary>
  
|  |  onC rea te()  |  onR est ar t()  |  onS tar t()  |  onR esu me ()  |  onP aus e()  |  onS top ()  |  onD est roy ()  | onS ave Ins t()  | onR est ore Ins t()  |
|-|-|-|-|-|-|-|-|-|-|
| buton _Home_ |   |   |    |    |  1  |  3  |   |  2  |   |
| buton _Back_ |   |   |    |    |  1  |  2  |  3  |     |   |
| buton _OK_in app |  nici | una   | din tre   | met ode  | nu   | se  | ape lea ză  |
| buton _lista app_  |   |   |   |   |  1  |  3  |   |  2  | |  
| apel tele fonic |   | | | |  1  |  3  | |  2  | |  
| acce ptare |   |  1  |  2  |   |    |    |   |  |  | 
| resp ingere |   |   |   |   |   |   |   |
| rotire ecran |  5  |   |  6  |   |  1  |  3  |  4  |  2  |  7  |

</details>




**6.** Să se dezactiveze opțiunea de salvare a stării.


> În fișierul `activity_lifecycle_monitor.xml`, pentru fiecare
dintre elementele grafice pentru care se dorește să se dezactiveze
opțiunea de salvare a stării, se va completa proprietatea
`android:saveEnabled="false"`.


Să se observe care este comportamentul în privința informațiilor
reținute în elementele grafice de tip `EditText`, respectiv `CheckBox`,
în condițiile în care activitatea este distrusă (se apasă butonul
*Home*, astfel încât să se apeleze metodele `onPause()` și `onStop()`,
apoi se închide aplicația. Să se repornească aplicația din meniul
dispozitivului mobil.

**7.** Să se implementeze metoda `onSaveInstanceState()`, astfel încât,
**în condițiile în care este bifat elementul grafic de tip `CheckBox`**,
să se salveze informațiile din interfața cu utilizatorul.

> Să se observe comportamentul aplicației în condițiile producerii
evenimentului de rotire de ecran.

**8.** Să se implementeze metoda `onRestoreInstanceState()` astfel
încât să se restaureze starea elementelor grafice. Să se observe
comportamentul aplicației în condițiile producerii evenimentului de rotire de ecran.

Să se transfere comportamentul de restaurare a stării pe metoda
`onCreate()` și să se identifice diferențele de implementare
([Hint](https://developer.android.com/guide/components/activities/activity-lifecycle.html#saras)).

**9.** Să se încarce modificările realizate în cadrul laboratorului pe Gitlab folosint nume sugestive pentru commits.


**10.** 
Utilitarul adb (Android Debug Bridge) se află în locația unde ați instalat SDK-ul pentru studio, de exemplu '/opt/android-sdk/platform-tools/'
Să se utilizeze comanda ```adb``` pentru a rula comenzi pe telefon:
 - ```adb devices``` - vizualizează dispozitivele disponibile (telefoane sau emulatoare)
 - ```adb -s DEVICE shell ls -l /sdcard/``` - dacă e unul singur, nu mai e nevoie de -s 
 - ```adb pull /sdcard/Download .``` - pentru a descărca fișiere/directoare din device în mașina de dezvoltare
 - ```adb push fișier.local /sdcard/Download/``` - încărcare
 - ```adb shell``` obținerea unui prompt în device 
 
