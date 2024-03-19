# Constructia unui Intent



## Intent explicit

Un intent explicit este unul pe care îl folosești pentru a lansa un component de aplicație specific, cum ar fi o activitate sau un serviciu particular în aplicația ta. Pentru a crea un intent explicit, definește numele componentei pentru obiectul Intent - toate celelalte proprietăți ale intentului sunt opționale.

De exemplu, dacă vrem sa pornim o activitate SecondActivity la apasarea unui buton vom folosi urmatorul cod:

*Java* 
```java
// Vom porni o a doua activitate la apasarea unui buton
// A doua activitatea a fost creata folosind Click Dreapta pe directorul cu activitati ->
// New View Empty Activity
Button btn = (Button)findViewById(R.id.open_activity_button);    

btn.setOnClickListener(new View.OnClickListener() {         
        @Override
        public void onClick(View v) {
            startActivity(new Intent(MainActivity.this, SecondActivity.class));
        }
});
```
*Kotlin* 
```kotlin
val btn = findViewById<Button>(R.id.open_activity_button)

btn.setOnClickListener { 
    startActivity(Intent(this@MainActivity, SecondActivity::class.java)) 
}
```

## Intent implicit

Un intent implicit specifică o acțiune care poate invoca orice aplicație de pe dispozitiv capabilă să efectueze acțiunea respectivă. Utilizarea unui intent implicit este utilă atunci când aplicația ta nu poate efectua acțiunea, dar alte aplicații probabil pot și ai vrea ca utilizatorul să aleagă care aplicație să folosească.

De exemplu, dacă ai conținut pe care vrei să-l partajezi cu alte persoane, creează un intent cu acțiunea 
`ACTION_SEND` și adaugă extra-uri care specifică conținutul de partajat. Atunci când apelezi `startActivity()`` cu acest intent, utilizatorul poate selecta o aplicație prin intermediul căreia să partajeze conținutul.

```java
Intent sendIntent = new Intent();
sendIntent.setAction(Intent.ACTION_SEND)
// Date pe care vrem sa le trimitem catre activitatea pe care urmeaza sa o pornim
sendIntent.putExtra(Intent.EXTRA_TEXT, textMessage);
sendIntent.setType("text/plain");

// Try to invoke the intent.
try {
    startActivity(sendIntent);
} catch (ActivityNotFoundException e) {
    // Define what your app should do if no activity can handle the intent.
}
```
*Kotlin*
```Kotlin
val sendIntent = Intent().apply {
    action = Intent.ACTION_SEND
    // Date pe care vrem sa le trimitem catre activitatea pe care urmeaza sa o pornim
    putExtra(Intent.EXTRA_TEXT, textMessage)
    type = "text/plain"
}

// Try to invoke the intent.
try {
    startActivity(sendIntent)
} catch (e: ActivityNotFoundException) {
    // Define what your app should do if no activity can handle the intent.
}
```
