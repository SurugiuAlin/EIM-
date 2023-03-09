#### AutoCompleteTextView

Controlul de tip `AutoCompleteTextView` indică utilizatorului anumite
valori cu care poate fi completat, în funcție de conținutul pe care
acesta îl are acesta la un moment dat, pe baza unei liste de sugestii.
Momentul la care sistemul de operare va oferi o sugestie este controlat
prin intermediul proprietății `completionThreshold`, care indică numărul
(minim) de caractere pe baza căruia se face potrivirea între șirul de
caractere introdus de utilizator și valorile existente în lista de
propuneri. Se poate afișa și un text sugestiv în cadrul listei de
sugestii, prin proprietatea `completionHint`.

\<spoiler>

``` java
AutoCompleteTextView coursesAutoCompleteTextView = (AutoCompleteTextView)findViewById(R.id.courses_auto_complete_text_view);

String[] suggestions = {"vlsi", "eim", "ts", "std", "so2", "idp", "ia", "scad", "pw", "ecom"};
ArrayAdapter<String> coursesArrayAdapter = new ArrayAdapter<String>(this, android.R.layout.simple_dropdown_item_1line, suggestions);

coursesAutoCompleteTextView.setAdapter(coursesArrayAdapter);
```

Sugestia este oferită pentru întregul conținut al componentei, astfel
încât dacă se dorește specificarea mai multor cuvinte, nu se va lua în
calcul fiecare dintre acestea.

\<note>Un astfel de control nu constrânge utilizatorul să introducă doar
valori din lista de sugestii, conținutul controlului grafic putând fi
oarecare.\

---

\</spoiler>
