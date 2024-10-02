# Creeam un layout vertical

În Compose, aranjamentele verticale sunt create cu funcția `Column()`.

Funcția `Column()` este un layout compozabil care își plasează copiii într-o
secvență verticală. În designul așteptat al aplicației, se poate observa că
imaginea zarului este afișată vertical deasupra butonului de aruncare:

Pentru a crea un aranjament vertical:

```kotlin
/* MainActivity.kt  */
fun DiceWithButtonAndImage(modifier: Modifier = Modifier) {
    Column (
        modifier = modifier,
        horizontalAlignment = Alignment.CenterHorizontally
    ) {}
}
```

**1.** În funcția `DiceWithButtonAndImage()`, se va adăuga o funcție `Column()`.

**2.** Se va transmite argumentul `modifier` din semnătura metodei `DiceWithButtonAndImage()` către argumentul modifier al `Column()`.
   Argumentul `modifier` asigură că compozabilele din funcția `Column()` respectă constrângerile aplicate instanței `modifier`.

**3.** Se va transmite un argument `horizontalAlignment` funcției `Column()` și apoi se va seta la o valoare de `Alignment.CenterHorizontally`.
   Aceasta asigură că copiii din coloană sunt centrați pe ecranul dispozitivului în ceea ce privește lățimea.

