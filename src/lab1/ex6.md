# Roll Magic

Acum că toate elementele compozabile necesare sunt prezente, vom modifica aplicația astfel încât o atingere a butonului să arunce zarurile.

```kotlin
/* MainActivity.kt */

fun DiceWithButtonAndImage(modifier: Modifier = Modifier) {
    var result = 1
    Column(
        modifier = modifier,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {
        Image(
            painter = painterResource(R.drawable.dice_1),
            contentDescription = "1"
        )
        Spacer(modifier = Modifier.height(16.dp))
        Button(onClick = { result = (1..6).random() }) {
            Text(stringResource(R.string.roll))
        }
    }
}
```

**1.** În funcția `DiceWithButtonAndImage()`, înainte de funcția `Column()`, creăm o variabilă `result` și o setăm la valoarea 1.

**2.** Privim la elementul compozabil `Button`. Vom observa că i se transmite un parametru `onClick` care este setat cu o pereche de acolade conținând comentariul `/*TODO*/`. Acoladele, în acest caz, reprezintă ceea ce se numește o lambda, zona din interiorul acoladelor fiind corpul lambda. Când o funcție este transmisă ca argument, poate fi denumită și "callback".

```kotlin
/* MainActivity.kt */
Button(onClick = { /*TODO*/ })
```

O lambda este o funcție literală, care este o funcție ca oricare alta, dar în loc să fie declarată separat cu cuvântul cheie `fun`, este scrisă inline și transmisă ca expresie. Elementul compozabil `Button` așteaptă să i se transmită o funcție ca parametru `onClick`. Acesta este locul perfect pentru a utiliza o lambda, și vom scrie corpul lambda în această secțiune.

**3.** În funcția `Button()`, eliminăm comentariul `/*TODO*/` din valoarea corpului lambda al parametrului `onClick`.

**4.** O aruncare de zaruri este aleatorie. Pentru a reflecta acest lucru în cod, trebuie să folosim sintaxa corectă pentru a genera un număr aleatoriu. În Kotlin, putem utiliza metoda `random()` pe un interval de numere. În corpul lambda al `onClick`, setăm variabila `result` la un interval între 1 și 6 și apoi apelăm metoda `random()` pe acel interval. Ne amintim că, în Kotlin, intervalele sunt desemnate prin două puncte între primul număr din interval și ultimul număr din interval.


Acum butonul poate fi atins, dar o atingere a butonului nu va cauza încă nicio schimbare vizuală deoarece trebuie să construim acea funcționalitate.

### Adăugăm o condiție la aplicația de aruncare a zarurilor

Pana acum, am creat o variabilă `result` și am setat-o manual la valoarea 1. În
cele din urmă, valoarea variabilei `result` este resetată când butonul Roll
este atins și ar trebui să determine ce imagine este afișată.

Elementele compozabile sunt fără stare în mod implicit, ceea ce înseamnă că nu
păstrează o valoare și pot fi recompuse oricând de către sistem, rezultând în
resetarea valorii. Cu toate acestea, Compose oferă o modalitate convenabilă de
a evita acest lucru. Funcțiile compozabile pot stoca un obiect în memorie
utilizând elementul compozabil `remember`.

```kotlin
/* MainActivity.kt */

var result by remember { mutableStateOf(1) }
```

**1.** Facem variabila `result` un element compozabil `remember`. Elementul compozabil `remember` necesită transmiterea unei funcții.

**2.** În corpul elementului compozabil `remember`, transmitem o funcție `mutableStateOf()` și apoi îi transmitem acestei funcții argumentul 1. Funcția `mutableStateOf()` returnează un observabil. Vom învăța mai multe despre observabile mai târziu, dar pentru moment, acest lucru înseamnă practic că atunci când valoarea variabilei `result` se schimbă, se declanșează o recompunere, valoarea lui `result` este reflectată, iar interfața utilizator se reîmprospătează.

Acum, când butonul este atins, variabila `result` este actualizată cu o valoare de număr aleatoriu.

**3.** Sub instanțierea variabilei `result`, creăm o variabilă imutabilă `imageResource` setată la o expresie `when` care acceptă variabila `result` și apoi setăm fiecare rezultat posibil la resursa sa drawable.

```kotlin
/* MainActivity.kt */

val imageResource = when (result) {
    1 -> R.drawable.dice_1
    2 -> R.drawable.dice_2
    3 -> R.drawable.dice_3
    4 -> R.drawable.dice_4
    5 -> R.drawable.dice_5
    else -> R.drawable.dice_6
}
```

**4.** Schimbăm ID-ul transmis parametrului `painterResource` al elementului compozabil `Image` de la resursa `R.drawable.dice_1` la variabila `imageResource`.

**5.** Schimbăm parametrul `contentDescription` al elementului compozabil `Image` pentru a reflecta valoarea variabilei `result` prin convertirea variabilei `result` la un șir de caractere cu `toString()` și transmiterea acestuia ca `contentDescription`.

```kotlin
/* MainActivity.kt */

Image(
   painter = painterResource(imageResource),
   contentDescription = result.toString()
)
```

**6.** Rulăm aplicația noastră.
