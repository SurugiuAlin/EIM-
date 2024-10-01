# Activity Lifecycle

O schimbare majora adusa sistemului de baza Linux de catre Android a fost un nou **ciclu de viata al proceselor**. Pentru a economisii energie, procesele nu ruleaza decat atunci cand sunt folosite de catre utilizator. Regasim acest lucru in **lifecycle-ul activitatilor**.


Din momentul în care activitatea este creată și până la momentul în care
este distrusă, ea trece printr-o serie de etape, cunoscute sub denumirea
de **ciclul de viață al activității**:

![](images/ciclul_de_viata_al_unei_activitati_1.png)


-   **în execuție** (*eng.* running) - activitatea se află în prim plan
    și este vizibilă, astfel încât utilizatorul poate interacționa cu
    aceasta prin intermediul interfeței grafice pe care o oferă;
-   **întreruptă temporar** (*eng.* paused) - activitatea se află în
    fundal și este (parțial) vizibilă; o astfel de situație este
    întâlnită în momentul în care o altă activitate a fost pornită, însă
    interfața sa grafică este transparentă sau nu ocupă întreaga
    suprafață a dispozitivului de afișare; în acest caz, activitatea
    este încă activă în sensul că obiectul de tip `Activity` este stocat
    în memorie, fiind atașată în continuare procesului responsabil cu
    gestiunea ferestrelor și menținându-se starea tuturor componentelor
    sale; totuși, ea poate fi distrusă de sistemul de operare dacă
    necesarul de memorie disponibilă nu poate fi întrunit din cauza sa;
-   **oprită** (*eng.* stopped) - activitatea se află în fundal și este
    complet ascunsă; o astfel de situație este întâlnită în momentul în
    care o altă activitate a fost pornită, iar interfața sa grafică
    ocupă întreaga suprafață a dispozitivului de afișare; și în acest
    caz, activitatea este activă în sensul că obiectul de tip `Activity`
    fiind stocat în memorie, menținându-se starea tuturor componentelor
    sale, dar detașându-se de procesul responsabil cu gestiunea
    ferestrelor; ea poate fi distrusă de sistemul de operare dacă
    necesarul de memorie disponibilă nu poate fi întrunit din cauza sa;
-   **inexistentă** - activitatea a fost terminată sau distrusă de
    sistemul de operare, rularea sa impunând crearea tuturor
    componentelor sale ca și când ar fi accesată inițial.


Tranziția unei activități dintr-o stare în alta este notificată prin
intermediul unor **callbacks**, care pot fi suprascrise
pentru a realiza diferite operații necesare pentru gestiunea memoriei,
asigurarea persistenței informațiilor și a consistenței aplicației
Android în situația producerii de diferite evenimente:


``` java
public class LifecycleMonitorActivity extends Activity {

  /* Apelată în momentul în care activitatea este
     creată; această metodă va fi folosită pentru
     inițializări statice: */
  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    * ...
  }
  /* apelată înainte ca activitatea să apară pe ecran; */
  @Override
  protected void onStart() {
    super.onStart();
    * ...
  }

  /* apelată înainte ca activitatea să interacționeze cu
    utilizatorul; această metodă va fi folosită pentru a     
    porni servicii sau cod care trebuie să ruleze atâta timp 
    cât aplicația este afișată pe ecran; este urmată 
    întotdeauna de metoda `onPause()`; */
  @Override
  protected void onResume() {
    super.onResume();
    * ...
  }
  
  /* apelată înainte ca activitatea să fie întreruptă
    temporar, iar o altă activitate să fie reluată; această 
    metodă va fi utilizată pentru a opri servicii sau cod 
    care nu trebuie să ruleze atâta timp cât activitatea se 
    află în fundal (întrucât consumă timp de procesor) și 
    pentru a salva starea diferitelor componente în
    vederea asigurării persistenței și a consistenței 
    aplicației înainte
    și după evenimentul care a produs suspendarea sa */
  @Override
  protected void onPause() {
    super.onPause();
    * ...
  }
   
  /*  apelată în momentul în care activitatea este ascunsă,
    fie din cauză că urmează să fie distrusă, fie din cauză 
    că o altă activitate, a cărei interfață grafică ocupă 
    întreaga suprafață a dispozitivului de afișare, urmează 
    să devină vizibilă;
  */
  @Override
  protected void onStop() {
    super.onStop();
    * ...
  }

  /* apelată înainte ca activitatea să se termine sau să
    fie distrusă de către sistemul de operare (fie manual, 
    fie automat) din lipsă de memorie; această metodă va fi 
    utilizată pentru a elibera resursele ocupate.
  */ 
  @Override
  protected void onDestroy() {
    super.onDestroy();
    * ...
  }
 
  /* apelată atunci când activitatea a fost oprită și
     ulterior repornită; este urmată întotdeauna de metoda
     `onStart()`; */
  @Override
  protected void onRestart() {
    super.onRestart();
    * ...
  }
  
}
```

``` kotlin
kotlin
#public override fun onCreate(savedInstanceState: Bundle?) {
#        super.onCreate(savedInstanceState)
#        ...
#}        

#public override fun onRestart() {
#        super.onRestart()
#        ...
#}

```
