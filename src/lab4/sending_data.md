# Transmiterea de informații între componente prin intermediul intențiilor

Intențiile pot încapsula anumite informații care pot fi partajate de
componentele între care fac legătura (însă unidirecțional, de la
componenta care invocă spre componenta invocată!) prin intermediul
secțiunii `extra` care conține un obiect de tip `Bundle`. Obținerea
valorii secțiunii `extra` corespunzătoare unei intenții poate fi
obținute folosind metoda `getExtras()`, în timp ce specificarea unor
informații care vor fi asociate unei intenții poate fi realizată
printr-un apel al metodei `putExtras()`.


O activitate copil, lansată în execuție prin intermediul metodei
`startActivity()`, este independentă de activitatea părinte, astfel
încât aceasta nu va fi notificată cu privire la terminarea sa. În
situațiile în care un astfel de comportament este necesar, activitatea
copil va fi pornită de activitatea părinte ca subactivitate care
transmite înapoi un rezultat. Acest lucru se realizează prin lansarea în
execuție a activității copil prin intermediul metodei
`startActivityForResult()`. În momentul în care este finalizată, va fi
invocată automat metoda `onActivityResult()` de la nivelul activității
părinte.


```java
final private static int ANOTHER_ACTIVITY_REQUEST_CODE = 2017;

@Override
protected void onCreate(Bundle state) {
    super.onCreate(state);
    setContentView(R.layout.activity_main);
    Button btn = (Button)findViewById(R.id.open_activity_button);    

    btn.setOnClickListener(new View.OnClickListener() {         
            @Override
            public void onClick(View v) {
                Intent intent = new Intent(MainActivity.this, SecondActivity.class);
                intent.putExtra("some_key", someValue);
                // Pornim intent, adaugam un int pe care il vom folosi ca filtru
                // in onActivityResult
                startActivityForResult(intent, ANOTHER_ACTIVITY_REQUEST_CODE);
            }
    });
}
// Aici vom extrage un bundle ce contine datele intoarse de `SecondActivity`
public void onActivityResult(int requestCode, int resultCode, Intent intent) {
  switch(requestCode) {
    case ANOTHER_ACTIVITY_REQUEST_CODE:
      if (resultCode == Activity.RESULT_OK) {
        Bundle data = intent.getExtras();
      }
      break;
      // process other request codes
  }
}
```

În **activitatea copil**, înainte de apelul metodei `finish()`, va
trebui transmis activității părinte codul de rezultat
(`Activity.RESULT_OK`, `Activity.RESULT_CANCELED` sau orice fel de
rezultat de tip întreg) și obiectul de tip intenție care conține datele
(opțional, în situația în care trebuie întoarse rezultate explicit), ca
parametrii ai metodei `setResult()`. La polul opus, activitatea `SecondActivity` va prelua datele astfel:

```java
@Override
protected void onCreate(Bundle state) {
  super.onCreate(state);
  setContentView(R.layout.second_activity);

  /* Get intent from parent */
  Intent intentFromParent = getIntent();
  Bundle data = intentFromParent.getExtras();
  /* data has now some_key which we can use */
  
  /* Return some data to the calling Intent */
  Intent intentToParent = new Intent();
  intent.putExtra("another_key", anotherValue);
  setResult(RESULT_OK, intentToParent);
  finish();
```

## ResultsLauncher API
`onActivityResult` e deprecated. Google recomandă folosirea  [ActivityResultsLauncherAPI](https://developer.android.com/training/basics/intents/result).
Aceasta nouă abordare este mai sigură și mai ușor de gestionat, deoarece elimină necesitatea de a utiliza coduri de cerere hardcoded și simplifică gestionarea callback-urilor pentru rezultatele activității.

**Activitatea părinte (MainActivity)**
În activitatea părinte, înlocuiește `startActivityForResult()` și `onActivityResult()` cu utilizarea unui `ActivityResultLauncher`.

```kotlin
class MainActivity : AppCompatActivity() {
    // Definește un ActivityResultLauncher
    private lateinit var startForResult: ActivityResultLauncher<Intent>

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        // Inițializează launcher-ul cu un callback pentru rezultat
        startForResult = registerForActivityResult(StartActivityForResult()) { result ->
            if (result.resultCode == Activity.RESULT_OK) {
                // Procesează rezultatul aici
                val data: Intent? = result.data
                val someData = data?.getStringExtra("another_key")
                // Folosește `someData` cum este necesar
            }
        }

        val btn = findViewById<Button>(R.id.open_activity_button)
        btn.setOnClickListener {
            val intent = Intent(this, SecondActivity::class.java).apply {
                putExtra("some_key", "someValue")
            }
            // Lansează activitatea copil folosind launcher-ul
            startForResult.launch(intent)
        }
    }
}
```

**Activitatea Copil (SecondActivity)**
```Kotlin
class SecondActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.second_activity)

        // Presupunând că vrei să returnezi rezultatul la un anumit eveniment, de exemplu, la apăsarea unui buton
        val someButton: Button = findViewById(R.id.some_button)
        someButton.setOnClickListener {
            val returnIntent = Intent().apply {
                putExtra("another_key", "anotherValue")
            }
            setResult(RESULT_OK, returnIntent)
            finish()
        }

        // Dacă activitatea se încheie fără a seta explicit un rezultat, poți să nu faci nimic sau să setezi RESULT_CANCELED
    }
}
```