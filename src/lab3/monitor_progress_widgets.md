### Controale pentru monitorizarea progresului --facultativ

În momentul în care sunt realizate acțiuni care durează o perioadă de
timp mai mare, o practică uzuală este de a indica utilizatorului faptul
că un proces este în desfășurare și că aplicația nu s-a blocat prin
intermediu unei bare de progres. O altă situație în care se dorește să
se afișeze progresul este indicarea evoluției pe care a realizat-o un
utilizator în cadrul unei aplicații (rularea unui fișier multimedia -
timp scurs vs. timp rămas, nivelul la care s-a ajuns în cadrul unui joc)
sau chiar controlul acestei poziții.

SDK-ul de Android oferă mai multe controale care pot fi utile în
monitorizarea progresului: bară de progres (`ProgressBar`) sau bară de
căutare (`SeekBar`), precum și alte obiecte pentru a indica diferite
forme de activitate.

![](images/progress_monitoring_samples.png)

#### ProgressBar

Obiectul de tip `ProgressBar` are mai multe forme:

1.  un indicator circular animat, care nu oferă nici un fel de
    informații cu privire la procentul de completitudine al procesului
    realizat în fundal (util mai ales pentru operații a căror lungime nu
    poate fi determinată); stilurile care pot fi folosite pentru acest
    tip de bară de progress sunt `progressBarStyleLarge` și
    `progressBarStyleSmall`, animația fiind realizată în mod automat;
2.  o bară de progres orizontală care indică și măsura în care sarcina
    din fundal a fost realizată (poate fi însoțită și de o altă bară de
    progres orizontală care indică starea unui proces imbricat); stilul
    folosit în acest caz este `progressBarStyleHorizontal`, suportând
    proprietăți cum ar fi `progress` (valoarea curentă), respectiv `min`
    / `max`.

Se obișnuiește ca progresul să fie afișat direct în bara de titlu, ceea
ce poate economisi din spațiul folosit de interfața grafică, acesta
putând fi activat / dezactivat cu ușurință. Semnificația unui indicator
de progres în acest caz este aceea că trebuie așteptată încărcarea mai
multor resurse înainte ca utilizatorul să poată interacționa cu
aplicația respectivă.

\<columns 100% 50%>

``` java
@Override
protected void onCreate(Bundle savedInstanceState) {
  requestWindowFeature(Window.FEATURE_INDETERMINATE_PROGRESS);
  setContentView(R.layout.progress_bar_activity);
  setProgressBarIndeterminateVisibility(true);
}
```

\<newcolumn>

``` java
@Override
protected void onCreate(Bundle savedInstanceState) {
  requestWindowFeature(Window.FEATURE_PROGRESS);
  setContentView(R.layout.progress_bar_activity);
  setProgressBarVisibility(true);
  setProgress(0); * valoarea maxima implicita este 10000
}
```

\</columns>

De remarcat faptul că metoda `requestWindowFeature()` trebuie apelată
înainte de încărcarea propriu-zisă a interfeței grafice prin metoda
`setContentView()`. Implicit, indicatorul de progres este vizibil,
metodele `setProgressBarIndeterminateVisibility()` și
`setProgressBarVisibility()` având rolul de a-l activa, respectiv
dezactiva în funcție de parametrul care este transmis. În momentul în
care progresul atinge valoarea maximă, starea obiectului asociat trece
de la vizibil la non-vizibil, prin intermediul unei animații.

În situația în care nu se poate evalua progresul pe care îl
înregistrează un proces, se folosesc **indicatori de activitate**, care
pot avea forma unei bare de stare sau a unui cerc.

\<note>Fiecare operație care este realizată în fundal ar trebui
reprezentată în interfața grafică prin intermediul unui indicator de
activitate.\

---

Se folosesc tot obiecte de tip `ProgressBar`, pentru care se precizează
faptul că vor rula o perioadă de timp nedeterminată:

-   prin precizarea proprietății `android:indeterminate`;
-   prin invocarea metodei `setProgressBarIndeterminateVisibility()`.

#### SeekBar

În situația în care se dorește să se ofere utilizatorului posibilitatea
de a controla progresul unei anumite operații, se folosește un obiect de
tip `SeekBar`, care are în plus un selector a cărui locație poate fi
modificată manual prin interfața grafică, la orice poziție cuprinsă
între `0` și valoarea indicată de proprietatea `max`.

---
**Note**

Resursa grafică folosită pentru redarea selectorului poate fi
particularizată prin utilizarea oricărei imagini din directorul
`drawable`.\

---

Notificările cu privire la modificările operate pe un astfel de obiect
sunt primite prin intermediul unui obiect ascultător de tipul
`SeekBar.OnSeekBarChangeListener` pentru care se definește metoda
`onProgressChanged()` (aceasta primește și un parametru de tip `boolean`
care indică dacă actualizarea controlului a fost realizată în urma unei
intervenții a utilizatorului sau programatic):

``` java
SeekBar moviePlayerSeekBar = (SeekBar)findViewById(R.id.movie_player_seek_bar);
moviePlayerSeekBar.setOnSeekBarListener(new SeekBar.OnSeekBarChangeListener() {
  
  @Override
  public void onProgressChanged(SeekBar seekBar, int progress, boolean fromTouch) {
    * ...
  }
  
});
```
