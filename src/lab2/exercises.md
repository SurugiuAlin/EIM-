## Activitate de Laborator

**1.** În contul Github personal, să se creeze un depozit denumit
'Laborator02' in care vom pune aplicatia la care vom lucra astazi.

- Să se cloneze [scheletul laboratorului](https:*www.github.com/eim-lab/Laborator02).
- Să se încarce conținutul descărcat în cadrul depozitului `Laborator02` de pe contul Github personal.
Ne intereseaza doar folder-ul `labtasks`.

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

**3.** Să se creeze un filtru, denumit `ActivityLifecycleMonitor`,
astfel încât LogCat să afișeze doar mesajele care au eticheta
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
      - se primește un apel telefonic\\ a) pentru AVD, se poate folosi *ADM* → *Emulator Control*\\ b) pentru Genymotion se poate simula doar formarea unui număr de telefon <code>

Pe baza mesajelor, să se completeze tabelul de mai jos, indicând ordinea
în care s-au apelat metodele respective:

|                              | `onCreate()` | `onRestart()` | `onStart()` | `onResume()` | `onPause()` | `onStop()` | `onDestroy()` |
|------------------------------|--------------|---------------|-------------|--------------|-------------|------------|---------------|
| 1\) buton *Home*             |              |               | 3           | 4            | 1           | 2          |               |
| 2\) buton *Back*             |              |               |             |              |             |            |               |
| 3\) buton *OK* din aplicație |              |               |             |              |             |            |               |
| 4\) buton *lista app*        |              |               |             |              |             |            |               |
| 5\) apel telefonic           |              |               |             |              |             |            |               |
| a\) acceptare                |              |               |             |              |             |            |               |
| b\) respingere               |              |               |             |              |             |            |               |
| 6\) rotire ecran             |              |               |             |              |             |            |               |

**6.** Să se dezactiveze opțiunea de salvare a stării.

---
**Note**

În fișierul `activity_lifecycle_monitor.xml`, pentru fiecare
dintre elementele grafice pentru care se dorește să se dezactiveze
opțiunea de salvare a stării, se va completa proprietatea
`android:saveEnabled="false"`.

---

Să se observe care este comportamentul în privința informațiilor
reținute în elementele grafice de tip `EditText`, respectiv `CheckBox`,
în condițiile în care activitatea este distrusă (se apasă butonul
*Home*, astfel încât să se apeleze metodele `onPause()` și `onStop()`,
apoi se închide aplicația. Să se repornească aplicația din meniul
dispozitivului mobil.

**7.** Să se implementeze metoda `onSaveInstanceState()`, astfel încât,
**în condițiile în care este bifat elementul grafic de tip `CheckBox`**,
să se salveze informațiile din interfața cu utilizatorul.

---
**Note**

Se vor folosi metodele `putString()` și `putBoolean()` ale
clasei `Bundle`.  
  
Cheile sub care vor fi identificate valorile salvate sunt definite în
interfața `Constants` din pachetul
`ro.pub.cs.systems.eim.lab02.activitylifecyclemonitor.general`.  
  
Verificarea faptului că un element grafic de tip `CheckBox` este bifat
se face prin intermediul metodei `isChecked()`.

---

Să se observe comportamentul aplicației în condițiile producerii
evenimentului descris anterior.

**8.** Să se implementeze metoda `onRestoreInstanceState()` astfel
încât să se restaureze starea elementelor grafice. Să se observe
comportamentul aplicației în condițiile producerii evenimentului descris
anterior.

Să se transfere comportamentul de restaurare a stării pe metoda
`onCreate()` și să se identifice diferențele de implementare
([Hint](https:*developer.android.com/guide/components/activities/activity-lifecycle.html#saras)).

**9.** Să se încarce modificările realizate în cadrul depozitului
`Laborator02` de pe contul Github personal, folosind un mesaj sugestiv.