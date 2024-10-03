# Restructurare Cod Template

Restructurarea codului din template-ul de **Empty Activity**. Cum am observat deja, codul din template ne afiseaza mesajul Hello World.
Vom modifica o parte din codul generat pentru a se asemăna mai mult cu tema unei aplicații de aruncare a zarului. Vom realiza urmatoarele modificari:

* Eliminăm funcția `GreetingPreview()`.
* Definim o funcție `DiceWithButtonAndImage()` cu adnotarea `@Composable`. Această funcție compozabilă reprezintă componentele UI ale layout-ului și conține, de asemenea, logica pentru click-ul butonului și afișarea imaginii.
* Eliminăm funcția `Greeting(name: String, modifier: Modifier = Modifier)`.
* Definim o funcție `DiceRollerApp()` cu adnotările `@Preview` și `@Composable`.
* Deoarece această aplicație constă doar dintr-un buton și o imagine, 
putem considera această funcție compozabilă ca fiind aplicația în sine. De aici si numele, `DiceRollerApp()`.


```kotlin
/* MainActivity.kt */

@Preview
@Composable
fun DiceRollerApp() {

}

@Composable
fun DiceWithButtonAndImage() {

}
```

Deoarece am eliminat funcția `Greeting()`, apelul către `Greeting("Android")` din corpul lambda-ului `DiceRollerTheme()` este evidențiat cu roșu. Asta pentru că compilatorul nu mai poate găsi o referință la acea funcție.

* Ștergem tot codul din interiorul lambda-ului `setContent{}` găsit în metoda `onCreate()`.
* În corpul lambda-ului `setContent{}`, apelează lambda-ul `DiceRollerTheme{}` și apoi în interiorul lambda-ului `DiceRollerTheme{}`, apelează funcția `DiceRollerApp()`.

```kotlin
/* MainActivity.kt */
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContent {
        // Aici o sa punem numele temei, implicit este creata o tema cu numele proiectului
        // O gasiti si in uithemes/Theme.kt
        DiceRollerTheme {
            DiceRollerApp()
        }
    }
}
```

În funcția `DiceRollerApp()`, apelam `DiceWithButtonAndImage()`, functie in care vom defini interfata grafica.

```kotlin
/* MainActivity.kt */

@Preview
@Composable
fun DiceRollerApp() {
    DiceWithButtonAndImage()
}
```
