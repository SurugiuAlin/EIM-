## Structura unei aplicatii android

Spre deosebire de un proces pe Linux, o aplicație Android poate conține mai multe componente:

1.  [context](http://developer.android.com/reference/android/content/Context.html)
    reprezintă punctul central al unei aplicații Android, oferind acces
    către mai multe funcționalități ale acesteia (inclusiv la resursele
    dizpozitivului mobil, serviciile sistemului de operare, diferite
    fișiere de configurare); este instanțiat sub forma unui obiect de
    tip `android.app.Application`;
2.  [activity](http://developer.android.com/reference/android/app/Activity.html)
    realizează sarcini a căror execuție nu influențează timpul de
    răspuns al aplicației Android, astfel încât să nu aibă un impact
    asupra experienței utilizatorului; de aceea, este asociată unei
    ferestre (interfețe grafice), o aplicație Android fiind formată din
    una sau mai multe activități;
3.  [serviciul](http://developer.android.com/reference/android/app/Service.html)
    încapsulează procese mai complexe, executate în fundal (și posibil
    la intervale de timp regulate) a căror rulare durează o perioadă de
    timp semnificativă, astfel încât să nu poată fi plasate în cadrul
    aceluiași fir de execuție ca și interfața grafică prin care se
    asigură interacțiunea cu utilizatorul;
4.  [intent](https://developer.android.com/reference/android/content/Intent.html)
    este mecanismul de comunicare între elementele unei aplicații
    Android (activități și servicii); prin intermediul unui sistem de
    mesagerie (asincronă), sistemul de operare Android mapează o
    solicitare (împachetată sub forma unei intenții) către componenta
    adecvată.
