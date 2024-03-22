# Servicii

Un `Service` este o componentă a aplicației care poate efectua operațiuni de lungă durată în fundal. Nu oferă o interfață pentru 
utilizator. Odată pornit, un service poate continua să ruleze pentru o anumită perioadă de timp, chiar și după ce utilizatorul trece 
la o altă aplicație. În plus, o componentă se poate lega de un service pentru a interacționa cu acesta și chiar pentru a efectua 
comunicații între procese (IPC). De exemplu, un service poate gestiona tranzacții de rețea, poate reda muzică, poate efectua 
operațiuni de fișier I/O sau poate interacționa cu un furnizor de conținut, toate din fundal.


Un serviciu nu trece prin evenimentele ce fac parte din ciclul
de viață al unei activități. Totuși, un serviciu poate fi controlat
(pornit, oprit) din contextul altor componente ale unei aplicații
Android (activități, ascultători de intenții cu difuzare, alte
servicii).

**Serviciul este rulat pe firul de execuție principal al aplicației
Android**. De aceea, în situația în care operațiile pe care le
realizează poate influența experiența utilizatorului, acestea trebuie
transferate pe alte fire de execuție din fundal (folosind clasele
`HandlerThread` sau `AsyncTask`). Ar trebui să rulați orice operațiuni
blocante pe un thread separat în cadrul service-ului pentru a evita
 erorile Application Not Responding (ANR).

Un serviciu continuă să se ruleze chiar și în situația în care
componenta aplicației Android care l-a invocat prin intermediul unei
intenții devine inactivă (nu mai este vizibilă) sau chiar este distrusă.
Acest comportament este adecvat în situația în care serviciul realizează
operații de intrare/ieșire intensive, interacționează cu diverse
servicii accesibile prin intermediul rețelei sau cu furnizori de
conținut.
