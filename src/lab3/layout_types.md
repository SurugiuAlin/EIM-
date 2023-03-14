### Mecanisme pentru dispunerea controalelor (layout) 

Controalele Android fac parte din cadrul unui grup (obiect de tip
`android.view.ViewGroup`) care definește și modul în care acestea sunt
dispuse în cadrul interfeței grafice precum și dimensiunile pe care le
pot lua, motiv pentru care o astfel de componentă este referită și sub
denumirea de layout. Acest element nu vizează însă tratarea
evenimentelor legate de interacțiunea cu utilizatorul.

\<note>În Android, denumirea de layout este utilizată și pentru
fișierele de resurse care definesc interfața grafică corespunzătoare
unei activități, a unui fragment sau a unui alt element din interfața
grafică, plasate în `/res/layout` (respectiv în `/res/layout-land`).
Acestea nu trebuie însă confundate cu tipurile de controale care
gestionează mecanismul de dispunere a diferitelor elemente grafice în
cadrul interfeței.\

---

Cele mai utilizate tipuri de grupuri de componente vizuale sunt
`LinearLayout`, `AbsoluteLayout`, `RelativeLayout`, `FrameLayout`,
`TableLayout` și `GridLayout`.

>Există și alte tipuri de controale derivate din pachetul
`android.view.ViewGroup`, care au rolul de containere pentru anumite
colecții de informații, cu care utilizatorul poate interacționa în mod
direct: `ListView`, `GridView`, `ScrollView`, `ImageSwitcher`.

Elementele de tip layout pot fi imbricate (conținute) unele într-altele,
astfel încât se pot proiecta interfețe grafice în care modul de
dispunere al controalelor să fie foarte complex, prin combinarea
funcționalităților pe care le oferă fiecare dintre componentele de tip
`ViewGroup`. Restricția care trebuie respectată în acest caz este ca
spațiile de nume indicate prin proprietatea `xmlns` să fie precizate
doar o singură dată, de obiectul layout rădăcină.

Dezvoltarea unei interfețe grafice se poate realiza atât în fișierul XML
corespunzător activiții cât și programatic. În ambele cazuri, va trebui
precizat inițial obiectul de tip `ViewGroup` la care se va preciza
componența, prin specificarea elementelor de tip `View` pe care le
conțin.

Fiecare clasă de tip layout are și o clasă internă `LayoutParams` în
care proprietățile referitoare la dimensiuni și margini sunt reținute în
obiecte de tip `layout_...`. Ele vor fi aplicate tuturor controalelor
grafice conținute.Cele mai frecvent utilizate atribute sunt:

-   `layout_height`, `layout_width` - definesc lățimea și înălțimea
    componentei, putând avea valorile:

<!-- -->

        * ''match_parent'' - va ocupa tot spațiul pus la dispoziție de componenta în care este conținută (fără padding);
        * ''wrap_content'' - va ocupa doar spațiul solicitat de componentele pe care le conține (cu padding);
        * o valoare indicată explicit împreună cu unitatea de măsură.
    * ''layout_weight'' - proporția pe care o ocupă în raport cu alte componente;

\<note> Presupunând cazul unei interfețe cu trei componente:

-   dacă una are proprietatea `layout_weight` egală cu 1 (iar restul au
    specificată valoarea 0), aceasta va ocupa tot spațiul rămas liber
-   dacă valorile asociate proprietății `layout_weight` au valori egale
    cu 1, 2, respectiv 3, acestea vor ocupa 16% (1/6), 33% (2/6),
    respectiv 50% (3/6) din spațiul pe care îl pune la dispoziție
    componenta în care sunt incluse

\

---

-   `weightSum` - suma proporțiilor tuturor controalelor grafice
    conținute; valoarea implicită este 1;
-   `layout_gravity` - modul în care componenta este aliniată în cadrul
    grupului din care face parte (valorile posibile pe care le poate lua
    această proprietate sunt: `top`, `botttom`, `left`, `right`,
    `center_vertical`, `center_horizontal`, `center` (centrare pe ambele
    direcții), `fill_vertical`, `fill_horizontal`, `fill` (ocuparea
    spațiului pe ambele direcții), `clip_vertical`, `clip_horizontal`;
    aceste valori pot fi combinate prin intermediul operatorului `|` (pe
    biți);

---
**Note**

Această proprietate nu trebuie confundată cu `gravity`,
care controlează modul în care sunt dispuse elementele conținute în
cadrul componentei.\

---

-   marginile sunt precizate de proprietățile `layout_marginTop`,
    `layout_marginBottom`, `layout_marginLeft`, `layout_marginRight`,
    valorile precizate trebuind să aibă asociată și unitatea de măsură
    folosită; în situația în care se dorește să se folosească aceeași
    valoare pentru toate direcțiile, se va folosi atributul
    `layout_margin`;

---
**Note**

Pentru această proprietate este permisă și precizarea de
valori negative.

---

-   spațiul de umplere (cu spații) este specificat prin `paddingTop`,
    `paddingBottom`, `paddingLeft`, `paddingRight`;
-   `background` poate specifica o culoare sau o imagine care vor fi
    afișate pe fundal;
-   `textColor` indică culoarea textului în format `#rrggbb` (sau
    `#aarrggbb`), putând fi referită și o culoare definită anterior
    într-un fișier `colors.xml` (sau cu orice altă denumire) din
    directorul `/res/values` în care elementul rădăcină este
    `<resources>` (elementele de aici fiind referite prin `@color/...`).

