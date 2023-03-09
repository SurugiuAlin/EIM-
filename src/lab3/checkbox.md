#### CheckBox

Controlul de tip `CheckBox` (din clasa `android.widget.CheckBox`) este
tot un element de tip buton ce poate avea două stări (selectat și
neselectat), accesibile prin intermediul proprietății `checked`
(`android:checked` în fișierul XML și `setChecked()` sau `toggle()` în
codul sursă).

Deși este definit un tip de eveniment asociat selecției sau deselecției
acestei componente (specificat de interfața
`CompoundButton.OnCheckedChangeListener` pentru care trebuie
implementată metoda `onCheckedChange()`), de cele mai multe ori nu i se
asociază o clasă ascultător, verificându-se starea sa prin intermediul
metodei `isChecked()` la producerea unui alt eveniment.
