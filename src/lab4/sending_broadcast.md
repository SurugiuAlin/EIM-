#### Trimiterea unei intenții de tip broadcast

Construirea unei intenții care urmează să fie difuzată la
nivelul sistemului de operare Android poate fi realizată prin definirea
unui obiect de tipul `Intent`, pentru care se vor specifica acțiunea,
datele și categoria, astfel încât obiectele de tip ascultător să îl
poată identifica cât mai exact. Ulterior, acesta va fi trimis tuturor
proceselor aferente aplicațiilor instalate pe dispozitivul mobil prin
intermediul metodei `sendBroadcast()`, căreia îi este atașat ca
parametru.

---
**Note**

Pot fi utilizate atât acțiuni predefinite (care vor fi
procesate atât de aplicațiile Android native cât și de eventuale
aplicații instalate din alte surse) cât și acțiuni definite de
utilizator, pentru care trebuie implementate aplicații dedicate,
responsabile cu procesarea acestora.

---

``` java
final public static String SOME_ACTION = "ro.pub.cs.systems.eim.lab04.SomeAction.SOME_ACTION";

Intent intent = new Intent(SOME_ACTION);
intent.putExtra("someKey", someValue);
sendBroadcast(intent);
```

*Kotlin*
```Kotlin
companion object {
    const val SOME_ACTION = "ro.pub.cs.systems.eim.lab04.SomeAction.SOME_ACTION"
}

val intent = Intent(SOME_ACTION).apply {
    putExtra("someKey", someValue)
}
sendBroadcast(intent)
```