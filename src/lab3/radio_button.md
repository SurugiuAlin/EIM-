
#### RadioButton / RadioGroup

Un element de tip `android.widget.RadioButton` este tot un buton cu două
stări (selectat / neselectat), de obicei utilizat pentru selecția unei
singure opțiuni dintr-o listă, excluderea mutuală fiind realizată prin
includerea mai multor obiecte de acest tip într-o componentă de tip
`android.widget.RadioGropup`. \<spoiler> \<note>Un obiect de tip
`RadioButton` se poate afla și în afara unui grup la fel cum un obiect
de tip `RadioGroup` poate conține și alte controale decât
butoane.\

---

Inițial, toate butoanele din cadrul unui grup sunt deselectate, deși se
poate preciza această proprietate atât prin fișierul XML cât și
programatic. Odată ce un utilizator a selectat un buton radio din cadrul
unui grup, acesta nu mai poate fi deselectat (decât prin schimbarea
selecției pe un alt buton radio din cadrul grupului), anularea selecției
putând fi realizată prin metoda `clearCheck()` apelată pe obiectul
`RadioGroup` care conține obiectul de tip `RadioButton`.

Proprietățile care determină selecția unui `RadioButton` sunt aceleași
ca și în cazul celorlalte tipuri de butoane cu două stări.

Evenimentele de selecție a unui `RadioButton` în cadrul unui
`RadioGroup` pot fi realizate:

1.  prin definirea unei clase ascultător pe fiecare buton radio din
    cadrul grupului, aceasta implementând interfața
    `CompoundButton.OnCheckChangeListener` cu metoda
    `onCheckChanged(CompoundButton, boolean)` care transmite starea
    butonului radio (selectat, deselectat)
2.  prin definirea unei clase ascultător pe grupul de butoane, aceasta
    implementând interfața `RadioGroup.OnCheckChangeListener` cu metoda
    `onCheckChanged(RadioGroup, int)` care transmite identificatorul
    (din clasa `R.id`) butonului care a fost selectat

---
**Note**

Se va genera un eveniment de modificare a selecției și
atunci când aceasta este anulată (programatic).\

---

În situația în care nu se dorește generarea unui eveniment de fiecare
dată când se realizează o selecție, ci preluarea acesteia la un moment
dat de timp ulterior, va fi utilizată metoda `getCheckedRadioButtonId()`
din clasa `RadioGroup` care întoarce identificatorul butonului (din
clasa `R.id`) care a fost selectat (sau -1 dacă nu este selectat nici un
buton radio din cadrul grupului). \</spoiler>
