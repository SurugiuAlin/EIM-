# Servicii

În Android, clasa
[android.app.Service](http:*developer.android.com/reference/android/app/Service.html)
este utilizată pentru componente a căror funcționalitate implică
procesări complexe, de lungă durată, necesitând acces la anumite
resurse, fără a fi necesar să pună la dispoziție o interfață grafică sau
un mecanism de interacțiune cu utilizatorul. Prin intermediul unui
serviciu, se asigură faptul că aplicația Android continuă să se găsească
în execuție, chiar și atunci când interfața grafică a acesteia nu este
vizibilă.

---
**Note**

Întrucât prioritatea unui serviciu este mai mare decât a unei
activități inactive, este mai puțin probabil ca acestea să fie distruse
atunci când trebuie eliberate resursele sistemului de operare. De
altfel, un serviciu poate fi configurat să fie repornit imediat ce este
posibil sau chiar pentru a i se asocia o prioritate echivalentă cu a
unei activități active (dacă distrugerea serviciului are un impact la
nivelul interfeței grafice).\

---

Astfel, un serviciu nu trece prin evenimentele ce fac parte din ciclul
de viață al unei activități. Totuși, un serviciu poate fi controlat
(pornit, oprit) din contextul altor componente ale unei aplicații
Android (activități, ascultători de intenții cu difuzare, alte
servicii).

**Serviciul este rulat pe firul de execuție principal al aplicației
Android**. De aceea, în situația în care operațiile pe care le
realizează poate influența experiența utilizatorului, acestea trebuie
transferate pe alte fire de execuție din fundal (folosind clasele
`HandlerThread` sau `AsyncTask`).

Un serviciu continuă să se ruleze chiar și în situația în care
componenta aplicației Android care l-a invocat prin intermediul unei
intenții devine inactivă (nu mai este vizibilă) sau chiar este distrusă.
Acest comportament este adecvat în situația în care serviciul realizează
operații de intrare/ieșire intensive, interacționează cu diverse
servicii accesibile prin intermediul rețelei sau cu furnizori de
conținut.

---
**Note**

Opțiunea de a utiliza un serviciu în Android trebuie luată în
considerare numai în situația în care este necesar ca o anumită
funcționalitate să fie realizată independent de starea componentei care
a invocat-o. Dacă este necesar ca o operație să fie executată în tandem
cu o anumită componentă (doar în perioada în care aceasta este vizibilă,
spre exemplu), dar fără a avea un impact asupra experienței
utilizatorului (fără a influența timpul de răspuns al aplicației
Android), se va utiliza un fir de execuție dedicat, a cărui stare va fi
gestionată pe metodele de callback ce guvernează ciclul de viață al
componentei respective.

---