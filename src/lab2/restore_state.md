# Restaurarea Stării

Încărcarea conținutului din obiectul de tip `Bundle` (în vederea
restaurării stării) poate fi realizată:

1.  în metoda `onCreate()`:

    ```java
    @Override
    protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_lifecycle_monitor);
      EditText usernameEditText = (EditText)findViewById(R.id.username_edit_text);
      if ((savedInstanceState != null) && (savedInstanceState.getString(Constants.USERNAME_EDIT_TEXT) != null)) {
        usernameEditText.setText(savedInstanceState.getString(Constants.USERNAME_EDIT_TEXT));
      }
    }
    ```
2.  prin intermediul metodei `onRestoreInstanceState()`, apelată în mod
    automat între metodele `onStart()` și `onResume()`; această abordare
    permite separarea dintre codul folosit la crearea ferestrei și codul
    utilizat la restaurarea stării unei ferestre

    ```java
    @Override
    protected void onRestoreInstanceState(Bundle savedInstanceState) {
      super.onRestoreInstanceState(savedInstanceState);
      EditText usernameEditText= (EditText)findViewById(R.id.username_edit_text);
      if (savedInstanceState.getString(Constants.USERNAME_EDIT_TEXT) != null) {
          usernameEditText.setText(savedInstanceState.getString(Constants.USERNAME_EDIT_TEXT));
      }
    }
    ```
