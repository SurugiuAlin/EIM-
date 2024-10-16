#### TextView

Controlul de tip `TextView` este utilizat pentru afișarea unui text
către utilizator, fără ca acesta să aibă posibilitatea de a-l modifica.

Conținutul pe care îl afișează un obiect `TextView` este indicat de
proprietatea `text`. De regulă, acesta referă o constantă definită în
resursa care conține șirurile de caractere utilizate în cadrul
aplicației. Gestiunea acestui atribut poate fi realizată prin metodele
getter și setter respective.

```xml
<?xml version="1.0" encoding="utf-8"?>
<RelativeLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/myTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_centerInParent="true"
        android:text="Hello, Android!"
        android:textSize="24sp" />

</RelativeLayout>
```

```java
public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        TextView textView = findViewById(R.id.myTextView);
        textView.setText("Hello, Android!");
    }
}
```

Pentru a defini lățimea și înălțimea unui control de tip
`TextView`, este de preferat să se utilizeze următoarele unități de
măsură:

-   **ems** (pentru lățime) - termen folosit în tipografie relativ la
    dimensiunea punctului unui set de caractere, oferind un control mai
    bun asupra modului în care este vizualizat textul, independent de
    dimensiunea propriu-zisă a semnelor respective;
-   **număr de linii** (pentru înălțime) - garantează afișarea
    netrunchiată a textului, indiferent de dimensiunea caracterelor;
