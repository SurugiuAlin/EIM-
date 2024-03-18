## Intenții

Aplicațiile pe Android sunt izolate, și comunicația între aplicație
și sistem se face prin Inter-Process Communication (IPC). În
Android, pentru a porni alte activități sau aplicații vom folosi
forma de IPC numită  **Intents**.

Conceptul de intenție în Android este destul de complex (și unic),
putând fi definit ca o acțiune având asociată o serie de informații,
transmisă sistemului de operare Android pentru a fi executată sub forma
unui mesaj asincron. În acest fel, intenția asigură interacțiunea între
toate aplicațiile instalate pe dispozitivul mobil, chiar dacă fiecare în
parte are o existență autonomă. Din această perspectivă, sistemul de
operare Android poate fi privit ca o colecție de componente funcționale,
independente și interconectate.

De regulă, o intenție poate fi utilizată pentru:

-   a invoca activități din cadrul aceleiași aplicații Android;
-   a invoca alte activități, existente în contextul altor aplicații
    Android;
-   a transmite mesaje cu difuzare (*eng.* broadcast messages), care
    sunt propagate la nivelul întregului sistem de operare Android și pe
    care unele aplicații Android le pot prelucra, prin definirea unor
    clase ascultător specifice; un astfel de comportament este util
    pentru a implementa aplicații bazate pe evenimente.

![](images/intent-filters_2x.png)

O intenție reprezintă o instanță a clasei `android.content.Intent`.
Aceasta este transmisă ca parametru unor metode (de tipul
`startActivity()` sau `startService()`, definite în clasa abstractă
`android.content.Context`), pentru a invoca anumite componente
(activități sau servicii). Un astfel de obiect poate încapsula anumite
date (împachetate sub forma unui `android.os.Bundle`), care pot fi
utilizate de componenta ce se dorește a fi executată prin intermediul
intenției.
