#### EditText

`EditText` este o componentă utilizată pentru obținerea unui text de la
utilizator. Implementarea sa pornește de la obiectul de tip `TextView`,
astfel încât sunt moștenite toate proprietățile sale.

În mod obișnuit, valoarea introdusă va fi afișată doar pe o
linie. Dacă se dorește redimensionarea controlului pe măsură ce este
introdus un text de dimensiuni mai mari, va trebui specificată
proprietatea `inputType="textMultiLine"`. De asemenea, se poate
specifica explicit numărul de linii prin intermediul proprietății
`lines` (în cazul în care aceasta nu este specificată, câmpul va fi
redimensionat în mod automat pentru ca textul introdus să poată fi
afișat; totuși indicarea acestui atribut este util pentru că impune o
dimensiune fixă, utilizatorul având posibilitatea de a naviga în cadrul
textului prin operația de derulare).

De asemenea, există posibilitatea indicării unei sugestii, care va fi
afișată pe fundal, semitransparentă, prin intermediul proprietății
`hint`. Aceasta precizează utilizatorului ce fel de informații ar trebui
specificate prin intermediul controlului. Ea va dispare în mod automat
în momentul în care utilizatorul începe să introducă textul respectiv.

Printre funcționalitățile elementului de tip `EditText` se numără și
posibilitatea de a corecta un text (proprietatea `inputType` are
valoarea `textAutoCorrect`) sau de a accepta doar valori care respectă
un anumit format (număr de telefon, adresă de poștă electronică, parolă,
număr zecimal (cu sau fără semn), dată calendaristică, oră). Totodată,
utilizatorul poate fi forțat să introducă valori care respectă doar un
anumit format, prin intermediul metodei `setFilters()` care primește ca
parametru un tablou de filtre (asigurându-se în acest mod îndeplinirea
concomitentă a condițiilor specificate de fiecare în parte):

-   predefinite în clasa
    [InputFilter](http:*developer.android.com/reference/android/text/InputFilter.html)
    -   `InputFilter.AllCaps` - toate caracterele trebuie scrise cu
        majusculă;
    -   `InputFilter.LengthFilter` - sunt acceptate doar șiruri de
        caractere care au o dimensiune fixă (precizată ca parametru în
        constructor);
-   definite de utilizator, prin implementarea metodei `filter()` din
    interfața `InputFilter`, indicându-se valoarea cu care se
    înlocuiește o anumită secvență.

Operația de tip apăsare lungă în cadrul unui control de tip `EditText`
invocă meniul contextual, care oferă facilități pentru copierea unui
text într-o / dintr-o zonă de memorie tampon (*eng.* copy-cut-paste),
schimbarea mecanismului de introducere a textului, modificarea
dicționarului ce conține cele mai frecvent folosite cuvinte. De
asemenea, poate fi selectată (evidențiată) un fragment din textul
respectiv (programatic, această funcționalitate poate fi obținută prin
metodele `setSelection()` / `selectAll()`).
