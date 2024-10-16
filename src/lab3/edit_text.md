#### EditText

`EditText` este o componentă utilizată pentru obținerea unui text de la
utilizator. Implementarea sa pornește de la obiectul de tip `TextView`,
astfel încât sunt moștenite toate proprietățile sale.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <EditText
        android:id="@+id/editText"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:hint="Enter text here" />

    <Button
        android:id="@+id/getTextButton"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="16dp"
        android:text="Get Text" />

    <TextView
        android:id="@+id/resultTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_gravity="center_horizontal"
        android:layout_marginTop="16dp"
        android:textSize="18sp" />

</LinearLayout>
```

```java
public class MainActivity extends AppCompatActivity {

    private EditText editText;
    private TextView resultTextView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        editText = findViewById(R.id.editText);
        resultTextView = findViewById(R.id.resultTextView);
        Button getTextButton = findViewById(R.id.getTextButton);

        getTextButton.setOnClickListener(v -> {
            String inputText = editText.getText().toString();
            resultTextView.setText("You entered: " + inputText);
        });
    }
}
```

În mod obișnuit, valoarea introdusă va fi afișată doar pe o
linie. Dacă se dorește redimensionarea controlului pe măsură ce este
introdus un text de dimensiuni mai mari, va trebui specificată
proprietatea `inputType="textMultiLine"`. De asemenea, se poate
specifica explicit numărul de linii prin intermediul proprietății
`lines` (în cazul în care aceasta nu este specificată, câmpul va fi
redimensionat în mod automat pentru ca textul introdus să poată fi
afișat; totuși indicarea acestui atribut este util pentru că impune o
dimensiune fixă, utilizatorul având posibilitatea de a naviga în cadrul
textului prin operația de derulare).
