#### CheckBox

Controlul de tip `CheckBox` (din clasa `android.widget.CheckBox`) este
tot un element de tip buton ce poate avea două stări (selectat și
neselectat), accesibile prin intermediul proprietății `checked`
(`android:checked` în fișierul XML și `setChecked()` sau `toggle()` în
codul sursă).

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical"
    android:padding="16dp">

    <CheckBox
        android:id="@+id/myCheckBox"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="My Checkbox" />

    <TextView
        android:id="@+id/statusTextView"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:layout_marginTop="16dp"
        android:textSize="18sp" />

</LinearLayout>
```

```java
public class MainActivity extends AppCompatActivity {

    private CheckBox checkBox;
    private TextView statusTextView;

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        checkBox = findViewById(R.id.myCheckBox);
        statusTextView = findViewById(R.id.statusTextView);

        checkBox.setOnCheckedChangeListener((buttonView, isChecked) -> {
            updateStatus(isChecked);
        });

        // Set initial status
        updateStatus(checkBox.isChecked());
    }

    private void updateStatus(boolean isChecked) {
        String status = isChecked ? "Checked" : "Unchecked";
        statusTextView.setText("Checkbox status: " + status);
    }
}
```

Deși este definit un tip de eveniment asociat selecției sau deselecției
acestei componente (specificat de interfața
`CompoundButton.OnCheckedChangeListener` pentru care trebuie
implementată metoda `onCheckedChange()`), de cele mai multe ori nu i se
asociază o clasă ascultător, verificându-se starea sa prin intermediul
metodei `isChecked()` la producerea unui alt eveniment.

