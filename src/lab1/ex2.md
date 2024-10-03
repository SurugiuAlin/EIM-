# Adaugare Modifier

Compose utilizează un obiect `Modifier`, care este o colecție de elemente care decorează sau modifică comportamentul elementelor UI Compose. Acesta va fi folosit pentru a stiliza componentele UI ale aplicației **Dice Roller**. Pentru a adăuga un modifier:

**1.** Vom modifica funcția `DiceWithButtonAndImage()` pentru a accepta un argument `modifier` de tip `Modifier` și îi vom atribui o valoare implicită de `Modifier`.

```kotlin
/* MainActivity.kt */

@Composable 
fun DiceWithButtonAndImage(modifier: Modifier = Modifier) {
}
```

Funcția permite transmiterea unui parametru `modifier`. Valoarea implicită a parametrului `modifier` este un obiect `Modifier`, de aici partea `= Modifier` din semnătura metodei. Valoarea implicită a unui parametru permite oricui apelează această metodă în viitor să decidă dacă să transmită o valoare pentru parametru. Dacă transmit propriul obiect `Modifier`, pot personaliza comportamentul și decorarea UI-ului. Dacă aleg să nu transmită un obiect `Modifier`, acesta va presupune valoarea implicită, care este obiectul `Modifier` simplu. Această practică poate fi aplicată oricărui parametru. Pentru mai multe informații despre argumentele implicite, consultați Argumente implicite.

**2.** Acum că funcția compozabilă `DiceWithButtonAndImage()` are un parametru modifier, vom transmite un modifier atunci când este apelată. Deoarece semnătura metodei pentru funcția `DiceWithButtonAndImage()` s-a schimbat, ar trebui transmis un obiect `Modifier` cu decorațiile dorite atunci când este apelată. Clasa `Modifier` este responsabilă pentru decorarea sau adăugarea de comportament unui compozabil în funcția `DiceRollerApp()`. În acest caz, există câteva decorații importante de adăugat la obiectul `Modifier` care este transmis funcției `DiceWithButtonAndImage()`.


```kotlin
/* MainActivity.kt */

DiceWithButtonAndImage(modifier = Modifier)
```

**3.** Vom înlănțui o metodă `fillMaxSize()` pe obiectul `Modifier` astfel încât layout-ul să umple întregul ecran.

```kotlin
/* MainActivity.kt */

DiceWithButtonAndImage(modifier = Modifier
    .fillMaxSize()
)
```


**4.** Centrarea obiectelor de pe ecran. Vom înlănțui metoda `wrapContentSize()` pe obiectul `Modifier` și apoi vom transmite `Alignment.Center` ca argument pentru a centra componentele. `Alignment.Center` specifică că o componentă se centrează atât vertical, cât și orizontal.

Metoda `wrapContentSize()` specifică că spațiul disponibil ar trebui să fie cel
puțin la fel de mare ca componentele din interior. Cu toate acestea, deoarece
se utilizează metoda `fillMaxSize()`, dacă componentele din interiorul
layout-ului sunt mai mici decât spațiul disponibil, un obiect `Alignment` poate
fi transmis metodei `wrapContentSize()` care specifică modul în care
componentele ar trebui aliniate în spațiul disponibil.


```kotlin
/* MainActivity.kt */

DiceWithButtonAndImage(modifier = Modifier
    .fillMaxSize()
    .wrapContentSize(Alignment.Center)
)
```
