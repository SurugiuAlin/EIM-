# Salvarea Stării

Pentru a salva starea, cum ar fi textul completat de utilizator intr-un
obiect de tip `EditText` din interfata grafica vom suprascrie metoda `onSaveInstanceState()` 
Ea primește ca parametru un obiect de tip `Bundle`, care este un fel de hashmap, în care vor
fi plasate datele din cadrul activității care se doresc a fi salvate,
acestea putând fi identificate prin intermediul unei chei (de tip
`String`).

``` java
@Override
protected void onSaveInstanceState(Bundle savedInstanceState) {
  /* Trebuie sa apelam metoda din clasa de baza întrucât API-ul Android
  furnizează o implementare implicită pentru salvarea stării unei
  activități, parcurgând ierarhia de componente grafice (obiecte de tip
  `View`) care au asociat un identificator (`android:id`), folosit drept
  cheie în obiectul `Bundle`. Astfel, de regulă, pentru elementele
  interfeței grafice, nu este necesar să se mențină starea, acest lucru
  fiind realizat în mod automat, cu respectarea condiției menționate. 
  super.onSaveInstanceState(savedInstanceState); */

  /* Determian o referinta pentru obiectul de tip EditText din interfata grafica
     cu ID-ul username_edit_text */
  EditText usernameEditText = (EditText)findViewById(R.id.username_edit_text);
  savedInstanceState.putString("SOME_STRING_USED_AS_KEY", usernameEditText.getText().toString());
}
```
