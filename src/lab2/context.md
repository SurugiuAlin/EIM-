### Contextul

Contexul este utilizat pentru a implementa diferite funcționalități la
nivelul întregii aplicații:

-   obținerea de referințe la resursele aplicației (șiruri de caractere,
    elemente grafice, fișiere XML);
-   accesarea preferințelor aplicației;
-   gestiunea sistemului de fișiere corespunzător aplicației;
-   lucrul cu resurse necompilate ale aplicației;
-   utilizarea serviciilor de sistem;
-   folosirea unei baza de date SQLite;
-   administrarea permisiunilor aplicației.

În clasele de tip `Activity` sau `Service`, contextul aplicației poate
fi obținut printr-un apel de forma:

``` java
Context context = getApplicationContext(); * definita in clasa Context
Context context = getApplication();        * definita in clasa Activity
```

---
**Note**

Pentru a se evita utilizarea ineficientă a memoriei (*eng.*
memory leak), în situația în care obiectele trebuie să existe pe toată
durata aplicației, se recomandă ca acestea să refere contextul
aplicației (nu al activității), astfel încât să nu fie condiționate de
diverse evenimente din ciclul de viață al acestora.

---