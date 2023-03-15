## Controale în Android (widget-uri)

În Android, un control (pentru care se utilizează și denumirea de
widget) este de regulă derivat din clasa `android.view.View`, unde sunt
definite câteva caracteristici de bază cu privire la dimensiuni și la
modul de dispunere:

| **ATRIBUT**           | **TIP OBIECT**       | **DESCRIERE**                                                                      |
|-----------------------|----------------------|------------------------------------------------------------------------------------|
| `layout_width`        | `View` / `ViewGroup` | lățimea obiectului                                                                 |
| `layout_height`       | `View` / `ViewGroup` | înălțimea obiectului                                                               |
| `layout_marginTop`    | `View` / `ViewGroup` | spațiu suplimentar ce trebuie alocat în partea de sus a obiectului                 |
| `layout_marginBottom` | `View` / `ViewGroup` | spațiu suplimentar ce trebuie alocat în partea de jos a obiectului                 |
| `layout_marginLeft`   | `View` / `ViewGroup` | spațiu suplimentar ce trebuie alocat în partea din stânga a obiectului             |
| `layout_marginRight`  | `View` / `ViewGroup` | spațiu suplimentar ce trebuie alocat în partea din dreapta a obiectului            |
| `layout_gravity`      | `View`               | modul de poziționare a elementelor componente în cadrul unui container             |
| `layout_weight`       | `View`               | proporția pe care o are controlul, raportată la întregul conținut al containerului |
| `layout_x`            | `View` / `ViewGroup` | poziția pe coordonata x                                                            |
| `layout_y`            | `View` / `ViewGroup` | poziția pe coordonata y                                                            |

Unele dintre aceste proprietăți pot fi specificate și pentru
containerele în care sunt cuprinse controalele, derivate din clasa
`android.view.ViewGroup`.

Valorile pe care le pot lua atributele `layout_width` și `layout_height`
sunt:

-   `match_parent` - dacă se dorește ca obiectul să ocupe tot spațiul pe
    care îl pune la dispoziție containerul său;

---
**Note**

Deși există și posibilitatea de a indica valoarea
`fill_parent` pentru lățimea și înălțimea unui control, aceasta trebuie
evitată, întrucât a fost înlocuită începând cu nivelul de API 8.\

---

-   `wrap_content` - dacă se dorește ca obiectul să fie restrâns la
    dimensiunile conținutului său.

În situația în care nu se specifică cel puțin valorile
`layout_width` și `layout_height` pentru un anumit control, se va genera
o excepție întrucât interfața grafică nu poate fi încărcată
corespunzător.\

---

De asemenea, pot fi specificate valori absolute, exprimate în una din
unitățile de măsură:

-   `dp` - **pixel independent de rezoluție**

---
**Note**

Se recomandă să se utilizeze această unitate de măsură în
momentul în care se specifică dimensiunea unui control în cadrul unui
container. Se asigură astfel faptul că se utilizează o proporție
adecvată pentru un control, indiferent de rezoluția ecranului, Android
scalându-i dimensiunea automat.\

---

-   `sp` - **pixel independent de scală**, echivalent cu `dp`

---
**Note**

Se recomandă să se utilizeze această unitate de măsură în
momentul în care se specifică dimensiunea unui set de caractere, cu care
va fi afișat un text.\

---

-   `pt` - **punct**, echivalent cu 1/72 inchi, bazat pe dimensiunile
    ecranului
-   `px` - **pixel**, corespunzător unui pixel al dispozitivului mobil

---
**Note**

Utilizarea acestei unități de măsură nu este recomandată,
întrucât interfața grafică definită în acești termeni nu se va afișa
corect pe dispozitive mobile cu altă rezoluție a ecranului.\

---

Specificarea dimensiunii ecranului unui dispozitiv mobil se face prin
indicarea numărului de pixeli pe orizontală și pe verticală. Pentru a
obține densitatea (rezoluția) dispozitivului respectiv, se împarte
dimensiunea exprimată în pixeli la dimensiunea exprimată în inchi. Se va
compara valoarea obținută cu una dintre valorile standard definite
pentru încadrarea dispozitivului mobil într-o anumită categorie de
rezoluție:

-   120 dpi - ldpi (Low Density)
-   160 dpi - mdpi (Medium Density)
-   240 dpi - hdpi (High Density)
-   320 dpi - xhdpi (Extra High Density)
-   480 dpi - xxhdpi (Extra Extra High Density)

Formula de conversie între pixeli (`px`) și pixeli independenți de
rezoluție (`dp`) este:

px = dp \* (resolution_category) / 160

Se observă că 1 `px` este echivalent cu 1 `dp` pe un ecran cu
rezoluția 160 dpi, considerată drept referință în Android.

---

Dimensiunea (exprimată în pixeli) a unui control poate fi obținută
apelând metodele `getWidth()`, respectiv `getHeight()`.
