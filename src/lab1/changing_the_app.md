# Modificarea Textului

Urmatorul lucru pe care il vom realiza este sa schimbam textul afisat.

Vom folosi **Code View** pentru a studia continutul fisierului MainActivity.kt. Observăm că există câteva funcții generate automat în acest cod, în special funcțiile `onCreate()` și `setContent()`.

```kotlin
class MainActivity : ComponentActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        // Punct de intrare in aplicatie, un fel de main
        super.onCreate(savedInstanceState)
        setContent {
            GreetingCardTheme {
                // Un container de suprafață care folosește culoarea 'background' din temă
                Surface(
                    modifier = Modifier.fillMaxSize(),
                    color = MaterialTheme.colorScheme.background
                ) {
                    Greeting("Android")
                }
            }
        }
    }
}
```

> Compilatorul ia codul Kotlin scris, si il translateaza in bytecode de Java Virtual Machine

Funcția `onCreate()` este punctul de intrare în această aplicație Android și
apelează alte funcții pentru a construi interfața utilizatorului. În programele
Kotlin, funcția `main()` este punctul de intrare/punctul de început al
execuției. În aplicațiile Android, funcția `onCreate()` îndeplinește acest rol.

Funcția `setContent()` din interiorul funcției `onCreate()` este utilizată
pentru a defini layoutul prin funcții compozabile. Toate funcțiile marcate cu
adnotarea `@Composable` pot fi apelate din funcția `setContent()` sau din alte
funcții Composable. Adnotarea spune compilatorului Kotlin că această funcție
este utilizată de Jetpack Compose (framework-ul ce se ocupa de interfata
grafica) pentru a genera UI-ul.

> O funcție compozabilă (composable function) în contextul Jetpack Compose, este o funcție utilizată pentru a defini elementele interfeței utilizator în mod declarativ.


În continuare, ne vom uita la funcția `Greeting()`. Funcția `Greeting()` este o
funcție Composable, observăm adnotarea `@Composable` de deasupra ei. Această
funcție Composable primește un input și generează ceea ce este afișat pe ecran.

```kotlin
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    // Afiseaza in interfata grafica un obiect (View) de tip casuta Text
    Text(
        text = "Hello $name!",
        modifier = modifier
    )
}
```


```kotlin
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Hello $name!",
        modifier = modifier
    )
}
```

În prezent, funcția `Greeting()` primește un nume și afișează "Hello" pentru acea persoană.

1. Actualizeazăm funcția `Greeting()` pentru a ne prezenta:

```kotlin
@Composable
fun Greeting(name: String, modifier: Modifier = Modifier) {
    Text(
        text = "Salut, numele meu este $name!",
        modifier = modifier
    )
}
```

2. Android ar trebui să actualizeze automat previzualizarea.

Excelent! Ai schimbat textul, dar te prezintă ca Android, ceea ce probabil nu
este numele tău. În continuare, vom personaliza aplicatia pentru a te afisa numele
nostru!

Funcția `GreetingPreview()` este o caracteristică excelentă care îți permite să
vezi cum arată composable-ul tău fără a trebui să construiești întreaga
aplicație. Pentru a activa o previzualizare a unui composable, adnotează cu
`@Composable` și `@Preview`. Adnotarea `@Preview` spune Android Studio că acest
composable ar trebui să fie afișat în vizualizarea de design a acestui fișier.

După cum poți vedea, adnotarea `@Preview` primește un parametru numit
`showBackground`. Dacă `showBackground` este setat la `true`, va adăuga un
fundal la previzualizarea composable-ului tău.

Deoarece Android Studio folosește implicit o temă luminoasă pentru editor,
poate fi dificil să vezi diferența între `showBackground = true` și
`showBackground = false`. Cu toate acestea, acesta este un exemplu de cum arată
diferența. Observă fundalul alb pe imaginea setată la true.

3. Actualizează funcția `GreetingPreview()` cu numele tău.

```kotlin
@Preview(showBackground = true)
@Composable
fun GreetingPreview() {
    GreetingCardTheme {
        Greeting("Meghan")
    }
}
```
