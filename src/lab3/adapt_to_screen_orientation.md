## Adaptarea interfeței grafice în funcție de orientarea ecranului

Dispozitivele Android suportă două moduri de orientare a ecranului:
`portrait` și `landscape`. În momentul în care se produce o modificare a
orientării dispozitivului de afișare, activitatea care rulează în mod
curent este distrusă și apoi recreată. Aplicațiile trebuie să gestioneze
astfel de situații, adaptând interfața grafică în funcție de suprafața
de care dispun.

\<spoiler> În acest scop, poate fi adoptată una din următoarele
abordări:

1.  **ancorarea** elementelor grafice (de regulă, de cele patru colțuri
    ale ecranului), folosind o dispunere de tip `RelativeLayout`
    împreună cu o combinație a proprietăților `layout_alignParentTop`,
    `layout_alignParentBottom`, `layout_alignParentLeft`,
    `layout_alignParentRight`, `layout_centerHorizontal`,
    `layout_centerVertical`
2.  **redimensionarea și repoziționarea**
    1.  creând un fișier XML corespunzător fiecărei activități pentru
        fiecare orientare a ecranului, plasate în `/res/layout`,
        respectiv în `/res/layout-land`
    2.  programatic, detectând modificarea dimensiunilor dispozitivului
        de afișare în metoda `onCreate()` `@Override
        public void onCreate(Bundle state) {
          super.onCreate(state);
          WindowManager windowManager = getWindowManager();
          Display display = windowManager.getDefaultDisplay();
          if (display.getWidth() <= display.getHeight()) {
            * create graphic user interface for portrait mode
          }
          else {
            * create graphic user interface for landscape mode
          }
        }
        `

De asemenea, o activitate poate fi forțată să afișeze conținutul
folosind un singur tip de orientare, indiferent de poziția în care se
află dispozitivul mobil:

1.  în fișierul AndroidManifest.xml, în elementul `<activity>`
    corespunzător, se specifică proprietatea `android:screenOrientation`
    cu valorile `portrait`, respectiv `landscape`;
2.  programatic, în metoda `onCreate()`, se apelează
    `setRequestedOrientation()` cu unul din parametrii
    `ActivityInfo.SCREEN_ORIENTATION_PORTRAIT` sau
    `ActivityInfo.SCREEN_ORIENTATION_LANDSCAPE`.

Deși în cadrul unui ecran pot fi utilizate combinații între mai multe
mecanisme de dispunere a conținutului, se recomandă ca o astfel de
abordare să fie evitată întrucât se poate ajunge la situația în care
interfața grafică nu scalează pe mai multe dispozitive de afișare cu
rezoluții diferite sau prezintă probleme de performanță.

În situația în care se dorește spațierea controalelor grafice, poate fi
utilizat un obiect de tip `android.widget.Space`.

Dacă se folosesc elemente grafice definite de utilizator, se poate
recurge la etichetele `<merge>` sau `<include>` pentru a le reutiliza
(în loc de a le duplica). De asemenea, un obiect de tip
[ViewStub](http:*developer.android.com/reference/android/view/ViewStub.html)
poate fi încărcat în mod dinamic la rulare (numai atunci când este
nevoie), în loc de a fi definit static în cadrul interfeței XML.

Pentru optimizarea unei interfețe grafice pot fi utilizate și alte
utilitare cum ar fi *Hierarchy View* sau
[Lint](http:*developer.android.com/tools/debugging/improving-w-lint.html).
\</spoiler>
