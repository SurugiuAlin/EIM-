#### TextView

Controlul de tip `TextView` este utilizat pentru afișarea unui text
către utilizator, fără ca acesta să aibă posibilitatea de a-l modifica.

Conținutul pe care îl afișează un obiect `TextView` este indicat de
proprietatea `text`. De regulă, acesta referă o constantă definită în
resursa care conține șirurile de caractere utilizate în cadrul
aplicației. Gestiunea acestui atribut poate fi realizată prin metodele
getter și setter respective.

---
**Note**

Metoda `getText()` întoarce un parametru de tip
[CharSequence](http:*developer.android.com/reference/java/lang/CharSequence.html),
astfel încât trebuie realizată conversia sa la o implementare a acestei
interfețe (cel mai frecvent, `String`), înainte de a putea folosi
valoarea respectivă.\

---

Pentru un control de tip `TextView` pot fi specificate mai multe
proprietăți, printre care `minLines`, `maxLines`, `minEms`, `maxEms` și
`textcolor`.

---
**Note**

Pentru a defini lățimea și înălțimea unui control de tip
`TextView`, este de preferat să se utilizeze următoarele unități de
măsură:

-   **ems** (pentru lățime) - termen folosit în tipografie relativ la
    dimensiunea punctului unui set de caractere, oferind un control mai
    bun asupra modului în care este vizualizat textul, independent de
    dimensiunea propriu-zisă a semnelor respective;
-   **număr de linii** (pentru înălțime) - garantează afișarea
    netrunchiată a textului, indiferent de dimensiunea caracterelor;

\

---

Pentru a avertiza utilizatorul de faptul că textul nu a fost afișat
complet, se poate folosi parametrul `ellipsible`, care atașează șirul de
caractere `(...)` în finalul secvenței vizibile. În cazul în care textul
este trunchiat și totuși textul afișat are sens, fără a exista indicii
că ar mai fi urmat și altceva, utilizarea acestui atribut este foarte
utilă.

O componentă de tip `TextView` NU implementează doar funcționalitatea
unei etichete, ea putând fi utilizată și pentru a realiza anumite
acțiuni, în cazul în care conținutul pe care îl afișează are un format
cunoscut:

-   `android:autoLink="none"` - dezactivează orice tip de acțiune care
    poate fi atașată unui text;
-   `android:autoLink="web"` - pentru pagini Internet care vor fi
    accesate prin intermediul unui navigator;
-   `android:autoLink="email"` - pentru adrese de poștă electronică la
    care se vor trimite mesaje prin intermediul unei aplicații dedicate;
-   `android:autoLink="phone"` - pentru numere de telefon care se doresc
    a fi formate;
-   `android:autoLink="map"` - pentru coordonate GPS care se doresc a fi
    vizualizate pe hartă;
-   `android:autoLink="all"` - activează orice tip de acțiune care poate
    fi atașată unui text.

---
**Note**

Se pot folosi și combinații ale acestor tipuri de legături,
agregate folosind operatorul `|` (pe biți).\

---

Nu întotdeauna este detectat tipul corect de informație și în
unele cazuri se poate realiza transferul către un alt tip de activitate
sau cu informații eronate.

---

Programatic, comportamentul unui obiect de acest tip poate fi stabilit
prin intermediul metodei `setAutoLinkMask()`, care va primi ca parametru
o constantă a clasei `Linkify`.

---
**Note**

Alternativ, poate fi utilizată metoda statică `addLinks()`
din clasa `Linkify`, apelată cu un parametru de tip `TextView` și un
parametru care indică tipul de conținut. \

---

În situația în care se dorește ca informația să fie afișată într-un mod
care să o evidențieze, însă fără a permite utilizatorului să lanseze în
execuție o altă activitate prin intermediul ei, se poate utiliza
atributul `linksClickable` (având valoarea `false`).

