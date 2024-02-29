# Logcat

Pentru a putea depana o aplicatie si a vedea eventualele mesaje de debug Android foloseste **LogCat**. Aveasta nevoie apare de la faptul ca o aplicatie android nu poate scrie la `stdout` sau `stderr` intr-un mod conventional.

Pentru a scrie un mesaj la log vom folosi functia `Log`:

```java
public class MainActivity extends AppCompatActivity {
   @Override
   protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_main);
      Log.w("SOME_TAG_TO_FILTER_IN_LOGCAT", "A pornit aplicatia cu bine!");
   }
```

Pentru a vedea mesajele de log pentru aplicația ta, urmează pașii următori.

1. În Android Studio, construiește și rulează aplicația ta pe un dispozitiv fizic sau pe un emulator.
2. Selectează **View > Tool Windows > Logcat** din bara de meniu.

Implicit, Logcat derulează până la final. Făcând click în fereastra Logcat sau derulând în sus folosind roata mouse-ului dezactivează această caracteristică. Pentru a o reactiva, fă click pe iconița Scroll to the End din bara de unelte. De asemenea, poți folosi bara de unelte pentru a goli, pauza sau reporni Logcat.

<img src="https://developer.android.com/static/studio/images/debug/logcat-window.png" alt=""/>


#### Cum citim log-urile?

Fiecare log conține o dată, marcaj temporal, ID de proces și thread, tag, numele pachetului, prioritate și mesaj asociat cu acesta. Tag-urile diferite au culori unice care ajută la identificarea tipului de log. Fiecare înregistrare în log are o prioritate care poate fi FATAL, ERROR, WARNING, INFO, DEBUG sau VERBOSE.

De exemplu, următorul mesaj de log are o prioritate de DEBUG și un tag de ProfileInstaller:

> 2022-12-29 04:00:18.823 30249-30321 ProfileInstaller        com.google.samples.apps.sunflower    D  Installing profile for com.google.samples.apps.sunflower

