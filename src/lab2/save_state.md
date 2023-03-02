##### Salvarea Stării

Metoda `onSaveInstanceState()` este înainte de metoda `onStop()` și
posibil înainte de metoda `onPause()`, deși acest lucru nu este
garantat. Ea primește ca parametru un obiect de tip `Bundle` în care vor
fi plasate datele din cadrul activității care se doresc a fi salvate,
acestea putând fi identificate prin intermediul unei chei (de tip
`String`).

\<note>Apelul metodei `onSaveInstanceState()` nu este garantat să fie
realizat de fiecare dată întrucât pot fi situații în care nu este
necesar ca starea activității să fie restaurată (utilizatorul a terminat
activitatea prin apăsarea butonului *Back*).\

---

În cazul în care se dorește salvarea explicită a conținutului unui
obiect `EditText`, se poate proceda astfel:

``` java
@Override
protected void onSaveInstanceState(Bundle savedInstanceState) {
  super.onSaveInstanceState(savedInstanceState);
  EditText usernameEditText = (EditText)findViewById(R.id.username_edit_text);
  savedInstanceState.putString(Constants.USERNAME_EDIT_TEXT, usernameEditText.getText().toString());
}
```

Valoarea introdusă de utilizator va fi salvată în obiectul de tip
`Bundle` sub denumirea `userNameEditText`, acesta fiind menținut și prin
urmare utilizat între mai multe instanțe ale acestei activități.

Apelarea metodei părinte este necesară întrucât API-ul Android
furnizează o implementare implicită pentru salvarea stării unei
activități, parcurgând ierarhia de componente grafice (obiecte de tip
`View`) care au asociat un identificator (`android:id`), folosit drept
cheie în obiectul `Bundle`. Astfel, de regulă, pentru elementele
interfeței grafice, nu este necesar să se mențină starea, acest lucru
fiind realizat în mod automat, cu respectarea condiției menționate. De
aceea, în metoda `onSaveInstanceState`, va fi realizată salvarea unor
informații (obiecte ale clasei) pentru care procesul de salvare a stării
nu este apelat. Totuși, asigurarea persistenței datelor nu se va realiza
niciodată aici (întrucât nu se garantează apelarea sa), ci în metoda
`onPause()`.

În obiectul de tip `Bundle`, prin cheia `android:viewHierarchyState` se
va reține un alt obiect de tip `Bundle` care reține starea tuturor
obiectelor de tip `View` din cadrul activității (care sunt identificate
prin intermediul unui câmp `android:id`). În cadrul acestuia, prin cheia
`android:views` se reține un obiect de tip `SparseArray` (un tip de dată
specific Android care realizează mapări între întregi și obiecte, mai
eficient decât un hashmap) care conține starea fiecărui obiect de tip
`View` prin intermediul identificatorului său.

``` java
Bundle viewHierarchy = savedInstanceState.getBundle("android:viewHierarchyState");
if (viewHierarchy != null) {
  SparseArray<? extends Parcelable> views = viewHierarchy.getSparseParcelableArray("android:views");
  for (int k=0; k < views.size(); k++) {
    Log.d(Constants.TAG, views.get(k) + "->" + views.valueAt(k));
  }
}
else {
  Log.d(Constants.TAG, "No view information was saved!");
}
```

Prin urmare, dacă aplicația este oprită și apoi pornită din nou,
obiectele de tip `View` vor avea conținutul existent în prealabil.
Pentru a dezactiva această opțiune, trebuie specificată în fișierul .xml
care descrie interfața grafică a activității, în elementul corespunzător
obiectului de tip `View` proprietatea `android:saveEnabled="false"`.

\<note>Dezactivarea se poate realiza și programatic, folosind metoda
`setSaveEnabled(boolean)`.\

---

