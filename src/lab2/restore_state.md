# Restaurarea Stării

Încărcarea conținutului din obiectul de tip `Bundle` (în vederea
restaurării stării) poate fi realizată:

1.  în metoda `onCreate()`:

<div class="tabbed-blocks">

  <pre><code class="language-java">
    @Override
    protected void onCreate(Bundle savedInstanceState) {
      super.onCreate(savedInstanceState);
      setContentView(R.layout.activity_lifecycle_monitor);
      EditText usernameEditText = (EditText)findViewById(R.id.username_edit_text);
      if ((savedInstanceState != null) && (savedInstanceState.getString(Constants.USERNAME_EDIT_TEXT) != null)) {
        usernameEditText.setText(savedInstanceState.getString(Constants.USERNAME_EDIT_TEXT));
      }
    }
</code></pre>

<pre><code class="language-kotlin">
override fun onCreate(savedInstanceState: Bundle?) {
    super.onCreate(savedInstanceState)
    setContentView(R.layout.activity_lifecycle_monitor)
    
    val usernameEditText = findViewById<EditText>(R.id.username_edit_text)
    
    savedInstanceState?.getString(Constants.USERNAME_EDIT_TEXT)?.let { username ->
        usernameEditText.setText(username)
    }
}
</code></pre>

2.  prin intermediul metodei `onRestoreInstanceState()`, apelată în mod
    automat între metodele `onStart()` și `onResume()`; această abordare
    permite separarea dintre codul folosit la crearea ferestrei și codul
    utilizat la restaurarea stării unei ferestre

<div class="tabbed-blocks">
  <pre><code class="language-java">
    @Override
    protected void onRestoreInstanceState(Bundle savedInstanceState) {
      super.onRestoreInstanceState(savedInstanceState);
      EditText usernameEditText= (EditText)findViewById(R.id.username_edit_text);
      if (savedInstanceState.getString(Constants.USERNAME_EDIT_TEXT) != null) {
          usernameEditText.setText(savedInstanceState.getString(Constants.USERNAME_EDIT_TEXT));
      }
    }
</code></pre>

<pre><code class="language-kotlin">
    override fun onRestoreInstanceState(savedInstanceState: Bundle) {
        super.onRestoreInstanceState(savedInstanceState)
        
        val usernameEditText = findViewById<EditText>(R.id.username_edit_text)
        
        savedInstanceState.getString(Constants.USERNAME_EDIT_TEXT)?.let { username ->
            usernameEditText.setText(username)
        }
    }
</code></pre>
