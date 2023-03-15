#### ImageView

Controlul de tip `ImageView` este utilizat pentru afișarea unei imagini,
aceasta putând proveni:

-   dintr-o resursă a aplicației Android, ce poate fi specificată
    -   în fișierul XML prin proprietatea `android:src=@drawable/...`
        (se poate indica și codul unei culori în formatul `#RRGGBB`)
    -   programatic, folosind una din metodele
        -   `setImageResource()`, care primește ca parametru
            identificatorul resursei din clasa `R.drawable`
        -   `setImageBitmap()`, ce primește un parametru de tip `Bitmap`
            încărcat din resursa respectivă, ulterior putând fi
            realizate și unele modificări

``` java
ImageView someImageView = (ImageView)findViewById(R.id.some_image_view);
Bitmap someBitmap = BitmapFactory.decodeResource(this.getResources(), R.drawable.some_image);

* realizeaza modificari asupra obiectului Bitmap

someImageView.setImageBitmap(someBitmap);
```

---
**Note**

Clasa `BitmapFactory` pune la dispoziția programatorilor și
alte metode pentru crearea unui obiect de tip `Bitmap`, folosind un
vector de octeți sau un obiect de tip `InputStream` (mai ales pentru
încărcarea unor resurse de pe un server).\

---

-   dintr-un fișier local, apelând pentru obiectul de tip `ImageView`
    una dintre metodele:
    -   `setImageDrawable()` ce primește ca parametru rezultatul întors
        de metoda statică `createFromPath()` a clasei `Drawable` pentru
        indicarea locației la care se găsește fișierul ce conține
        imaginea
    -   `setImageURI()`, transmițându-se un URI care să indice locația
        la care se găsește fișierul ce conține imaginea; în acest caz,
        va putea fi utilizat doar protocolul `file`
-   de la un furnizor de conținut

Pentru un astfel de obiect pot fi precizate parametrii precum lățimea și
înălțimea maximă (`maxWidth`, respectiv `maxHeight`), precum și
mecanismul folosit pentru scalarea conținutului în situația în care
suprafața pe care se realizează afișarea este diferită de dimensiunile
reale ale resursei (`scaleType`).
