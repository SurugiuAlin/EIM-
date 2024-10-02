# Adaugarea butonului de roll

**1.** În fișierul **strings.xml**, vom adăuga un string și îl vom seta la valoarea `Roll`.
   `res/values/strings.xml`

```xml
<string name="roll">Roll</string>
```

```kotlin
MainActivity.kt
Column(
    modifier = modifier,
    horizontalAlignment = Alignment.CenterHorizontally
) {
    Button(onClick = { /*TODO*/ }) {
        Text(stringResource(R.string.roll))
    }
}
```

**2.** În corpul lambda al `Column()`, vom adăuga o funcție `Button()`.

**3.** Next, vom adăuga o funcție `Text()` la `Button()` în corpul lambda al funcției.

**4.** Vor transmite ID-ul resursei string `roll` funcției `stringResource()` și vom transmite rezultatul componentei `Text`.
