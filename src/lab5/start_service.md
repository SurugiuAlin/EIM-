# Pornirea unui Serviciu

Un serviciu este pornit printr-un apel al metodei `startService()`.
Aceasta primește ca parametru un obiect de tip `Intent` care poate fi
creat:

-   explicit, pe baza denumirii clasei care implementează serviciul
    respectiv; 
    ```java
    Intent intent = new Intent(this, SomeService.class);
    startService(intent);
    ```
-   implicit, indicând componenta care gestionează serviciul respectiv
    (se va indica atât denumirea pachetului cât și denumirea clasei ca
    argument al metodei `setComponent()` asociat intenției respective):
    ```java
    Intent intent = new Intent();
    intent.setComponent(new ComponentName("SomePackage", "SomeService"));
    startService(intent);
    ```

Transmiterea de informații suplimentare către serviciu poate fi
realizată prin intermediul metodelor `putExtras(Bundle)`,
`putExtra(String, Parcelable)` sau `put<type>Extra(String, <type>)`.

Metoda `startService()` presupune livarea unui mesaj asincron la nivelul
sistemului de operare Android, astfel încât aceasta se execută
instantaneu. Fiecare apel al acestei metode invocarea, în mod automat,
al metodei `onStartCommand()`.

De regulă, comunicația dintre o componentă și un serviciu este
unidirecțională, dintre componenta care invocă către serviciul invocat,
prin intermediul datelor încapsulate în intenție. În situația în care se
dorește ca serviciul să transmită date către componentă, se utilizează
un obiect de tip
[PendingIntent](http:*developer.android.com/reference/android/app/PendingIntent.html),
prin intermediul căruia pot fi transmise mesaje cu difuzare.
