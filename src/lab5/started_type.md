# Servicii de tip Started

În momentul în care este pornit (printr-un apel al metodei
`startService()` din cadrul altei componente), un serviciu apelează în
mod automat metoda `onStartCommand()`. În cadrul acestei metode trebuie
realizată procesarea pe care o presupune serviciul respectiv. Pentru
serviciile de tip started, este necesar ca **serviciul să fie oprit
explicit**, fie din propriul său context, printr-un apel al metodei
`stopSelf()`, fie de către o componentă (aceeași sau alta decât cea care
l-a invocat), prin intermediul metodei `stopService()`.

``` java
@Override
public int onStartCommand(Intent intent, int flags, int startId) {
  processInBackground(intent, startId);
  return startMode;
}
```

Metoda `onStartCommand()` este apelată în mod automat în momentul în
care serviciul este pornit prin intermediul metodei `startService()` și
primește ca parametrii:

-   intenția care a invocat serviciul (argumentul transmis la apelul
    metodei `startService()`); **acesta poate fi `null`** în situația în
    care serviciul este repornit după ce procesul din care făcea parte a
    fost distrus;
-   anumite valori prin care poate fi semnalat modul în care a fost
    pornit:
    -   [START_FLAG_REDELIVERY](http:*developer.android.com/reference/android/app/Service.html#START_FLAG_REDELIVERY) -
        serviciul a fost repornit ca urmare a distrugerii sale de către
        sistemul de operare înainte de se fi terminat corespunzător;
    -   [START_FLAG_RETRY](http:*developer.android.com/reference/android/app/Service.html#START_FLAG_RETRY) -
        serviciul a fost repornit după o execuție anormală;
-   un identificator unic prin care se poate face distincția între
    apeluri diferite ale aceluiași serviciu.

Având în vedere faptul că această metodă poate fi apelată de mai multe
ori pe parcursul ciclului de viață al unui serviciu, tot aici trebuie
implementat și comportamentul în cazul în care acesta este repornit.

Comportamentul serviciului în situația în care este repornit poate fi
controlată prin intermediul valorii întregi care este furnizată ca
valoare întoarsă:

-   [Service.START_STICKY](http:*developer.android.com/reference/android/app/Service.html#START_STICKY) -
    mecanism standard, folosit de serviciile care își gestionează
    propriile stări și care sunt pornite și oprite în funcție de
    necesități (prin intermediul metodelor `startService()` și
    `stopService()`); prin aceasta, se indică faptul că metoda
    `onStartCommand()` va fi invocată de fiecare dată când serviciul
    este (re)pornit după ce a fost distrus de sistemul de operare
    Android (situație în care parametrul de tip `Intent` va avea
    valoarea `null`, dacă între timp serviciul nu a mai fost invocat);
-   [Service.START_NOT_STICKY](http:*developer.android.com/reference/android/app/Service.html#START_NOT_STICKY) -
    mecanism folosit de serviciile utilizate pentru a procesa anumite
    comenzi, care se opresc singure (printr-un apel al metodei
    `stopSelf()`) atunci când operațiile pe care trebuiau să le
    realizeze s-au terminat; serviciul este (re)pornit după ce a fost
    distrus de sistemul de operare Android numai în situația în care
    între timp au mai fost realizate apeluri ale metodei
    `startService()`, altfel nu este recreat; un astfel de comportament
    este adecvat pentru procese care sunt realizate periodic;
-   [Service.START_REDELIVER_INTENT](http:*developer.android.com/reference/android/app/Service.html#START_REDELIVER_INTENT) -
    mecanism utilizat atunci când se dorește să se asigure faptul că
    procesările asociate serviciului sunt terminate; în situația în care
    serviciul a fost distrus de sistemul de operare Android, este
    (re)pornit apelând metoda `onStartCommand()` folosind ca parametru
    intenția originală, a cărei procesare nu a fost terminată
    corespunzător.

În toate aceste cazuri, oprirea serviciului trebuie realizată explicit,
prin apelul metodelor:

-   `stopService()` din contextul componentei care l-a pornit;
-   `stopSelf()` din contextul serviciului.
