## Structura unei aplicatii android

O aplicație Android poate conține mai multe componente:

1.  [contextul](http:*developer.android.com/reference/android/content/Context.html)
    reprezintă punctul central al unei aplicații Android, oferind acces
    către mai multe funcționalități ale acesteia (inclusiv la resursele
    dizpozitivului mobil, serviciile sistemului de operare, diferite
    fișiere de configurare); este instanțiat sub forma unui obiect de
    tip `android.app.Application`;
2.  [activitatea](http:*developer.android.com/reference/android/app/Activity.html)
    realizează sarcini a căror execuție nu influențează timpul de
    răspuns al aplicației Android, astfel încât să nu aibă un impact
    asupra experienței utilizatorului; de aceea, este asociată unei
    ferestre (interfețe grafice), o aplicație Android fiind formată din
    una sau mai multe activități;
3.  [fragmentul](http:*developer.android.com/reference/android/app/Fragment.html)
    conține interfața grafică și logica aplicației corespunzătoare unei
    părți din cadrul unei activități; motivul pentru care se recurge la
    modularizarea unei activități prin intermediul a mai multor
    fragmente este asigurarea consistenței și flexibilității aplicației
    Android pe mai multe echipamente mobile, cu dispozitive de afișare
    de dimensiuni și rezoluții diferite;
4.  [serviciul](http:*developer.android.com/reference/android/app/Service.html)
    încapsulează procese mai complexe, executate în fundal (și posibil
    la intervale de timp regulate) a căror rulare durează o perioadă de
    timp semnificativă, astfel încât să nu poată fi plasate în cadrul
    aceluiași fir de execuție ca și interfața grafică prin care se
    asigură interacțiunea cu utilizatorul;
5.  [intenția](http:*developer.android.com/reference/android/content/Intent.html)
    este mecanismul de comunicare între elementele unei aplicații
    Android (activități și servicii); prin intermediul unui sistem de
    mesagerie (asincronă), sistemul de operare Android mapează o
    solicitare (împachetată sub forma unei intenții) către componenta
    adecvată.

![](images/structura_unei_aplicatii_Android.png)