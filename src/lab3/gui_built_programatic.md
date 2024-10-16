### Dezvoltarea programatică a unei interfețe grafice

O interfață grafică poate fi definită și în codul sursă, într-un mod
similar. Se creează inițial un obiect container (de tip `Layout`,
derivat din `android.view.ViewGroup`) care va cuprinde toate
controalele, acesta fiind argumentul cu care va fi apelată metoda
`setContentView()`.

Pentru fiecare control vor fi specificate (manual, prin
apelul metodei corespunzătoare) diferitele caracteristici,
asociindu-i-se și un identificator (uzual, acesta poate fi orice număr
întreg). Pentru fiecare proprietate a unui control grafic, sunt definite
programatic metodele de tip getter și setter corespunzătoare.

---
**Note**

În situația în care unui control nu i se asociază un
identificator prin apelul metodei `setId()`, valoarea acestui parametru
va fi `NO_ID`, astfel încât acesta nu va mai putea fi referit în cod
(spre exemplu, pentru poziționarea elementelor interfeței grafice
relativ, unele față de altele).

---

Ulterior, controlul va trebui asociat containerului din care face parte,
prin intermediul metodei `addView()`, specificându-se modul în care va
fi poziționat (precum și dimensiunile sale) prin intermediul unui obiect
de tip `LayoutParams`, specific mecanismului de dispunere respectiv.

<div class="tabbed-blocks">

  <pre><code class="language-java">
public class LayoutSample2Activity extends Activity {

  final private static long TRANSPARENCY_EFFECT_DURATION = 5000;
  
  @Override
  protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    
    RelativeLayout container = new RelativeLayout(this);
    container.setLayoutParams(new LayoutParams(LayoutParams.MATCH_PARENT, LayoutParams.MATCH_PARENT));
    
    final EditText introduceYourselfEditText = new EditText(this);
    introduceYourselfEditText.setId(1);
    introduceYourselfEditText.setEms(10);
    introduceYourselfEditText.setHint(getString(R.string.introduce_yourself));
    introduceYourselfEditText.setInputType(InputType.TYPE_CLASS_TEXT);
    introduceYourselfEditText.setFocusable(true);
    RelativeLayout.LayoutParams introduceYourselfEditTextLayoutParams = new RelativeLayout.LayoutParams(RelativeLayout.LayoutParams.WRAP_CONTENT, RelativeLayout.LayoutParams.WRAP_CONTENT);
    container.addView(introduceYourselfEditText, introduceYourselfEditTextLayoutParams);
    
    final CheckBox displayIdentityCheckBox = new CheckBox(this);
    displayIdentityCheckBox.setId(2);
    displayIdentityCheckBox.setText(getString(R.string.display_identity));
    RelativeLayout.LayoutParams displayIdentityCheckBoxLayoutParams = new RelativeLayout.LayoutParams(RelativeLayout.LayoutParams.WRAP_CONTENT, RelativeLayout.LayoutParams.WRAP_CONTENT);
    displayIdentityCheckBoxLayoutParams.addRule(RelativeLayout.ALIGN_LEFT, introduceYourselfEditText.getId());
    displayIdentityCheckBoxLayoutParams.addRule(RelativeLayout.BELOW, introduceYourselfEditText.getId());
    container.addView(displayIdentityCheckBox, displayIdentityCheckBoxLayoutParams);
    
    final Button submitButton = new Button(this);
    submitButton.setId(3);
    submitButton.setText(getString(R.string.submit));
    RelativeLayout.LayoutParams submitButtonLayoutParams = new RelativeLayout.LayoutParams(RelativeLayout.LayoutParams.WRAP_CONTENT, RelativeLayout.LayoutParams.WRAP_CONTENT);
    submitButtonLayoutParams.addRule(RelativeLayout.ALIGN_LEFT, displayIdentityCheckBox.getId());
    submitButtonLayoutParams.addRule(RelativeLayout.BELOW, displayIdentityCheckBox.getId());
    container.addView(submitButton, submitButtonLayoutParams);
    
    final TextView greetingTextView = new TextView(this);
    greetingTextView.setId(4);
    greetingTextView.setText(getString(R.string.greeting));
    greetingTextView.setTextSize(32);
    greetingTextView.setGravity(Gravity.CENTER);
    greetingTextView.setAlpha(0);
    RelativeLayout.LayoutParams greetingTextViewLayoutParams = new RelativeLayout.LayoutParams(RelativeLayout.LayoutParams.MATCH_PARENT, RelativeLayout.LayoutParams.MATCH_PARENT);
    greetingTextViewLayoutParams.addRule(RelativeLayout.ALIGN_LEFT, submitButton.getId());
    greetingTextViewLayoutParams.addRule(RelativeLayout.BELOW, submitButton.getId());
    container.addView(greetingTextView, greetingTextViewLayoutParams);
    
    submitButton.setOnClickListener(new View.OnClickListener() {
    
      @Override
      public void onClick(View view) {
        String identity = introduceYourselfEditText.getText().toString();
        greetingTextView.setText(getResources().getString(R.string.greeting).replace("???", (displayIdentityCheckBox.isChecked())?identity:getResources().getString(R.string.anonymous)));
        greetingTextView.setAlpha(1);
        AlphaAnimation fadeEffect = new AlphaAnimation(1.0f, 0.0f);
        fadeEffect.setDuration(TRANSPARENCY_EFFECT_DURATION);
        fadeEffect.setFillAfter(true);
        greetingTextView.setAnimation(fadeEffect);
      }
      
    });
    
    setContentView(container);
  }
  
  * ...

}

</code></pre>
<pre><code class="language-kotlin">

class LayoutSample2Activity : Activity() {
    protected fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)

        val container: RelativeLayout = RelativeLayout(this)
        container.setLayoutParams(
            LayoutParams(
                LayoutParams.MATCH_PARENT,
                LayoutParams.MATCH_PARENT
            )
        )

        val introduceYourselfEditText: EditText = EditText(this)
        introduceYourselfEditText.setId(1)
        introduceYourselfEditText.setEms(10)
        introduceYourselfEditText.setHint(getString(R.string.introduce_yourself))
        introduceYourselfEditText.setInputType(InputType.TYPE_CLASS_TEXT)
        introduceYourselfEditText.setFocusable(true)
        val introduceYourselfEditTextLayoutParams: RelativeLayout.LayoutParams = LayoutParams(
            RelativeLayout.LayoutParams.WRAP_CONTENT,
            RelativeLayout.LayoutParams.WRAP_CONTENT
        )
        container.addView(introduceYourselfEditText, introduceYourselfEditTextLayoutParams)

        val displayIdentityCheckBox: CheckBox = CheckBox(this)
        displayIdentityCheckBox.setId(2)
        displayIdentityCheckBox.setText(getString(R.string.display_identity))
        val displayIdentityCheckBoxLayoutParams: RelativeLayout.LayoutParams = LayoutParams(
            RelativeLayout.LayoutParams.WRAP_CONTENT,
            RelativeLayout.LayoutParams.WRAP_CONTENT
        )
        displayIdentityCheckBoxLayoutParams.addRule(
            RelativeLayout.ALIGN_LEFT,
            introduceYourselfEditText.getId()
        )
        displayIdentityCheckBoxLayoutParams.addRule(
            RelativeLayout.BELOW,
            introduceYourselfEditText.getId()
        )
        container.addView(displayIdentityCheckBox, displayIdentityCheckBoxLayoutParams)

        val submitButton: Button = Button(this)
        submitButton.setId(3)
        submitButton.setText(getString(R.string.submit))
        val submitButtonLayoutParams: RelativeLayout.LayoutParams = LayoutParams(
            RelativeLayout.LayoutParams.WRAP_CONTENT,
            RelativeLayout.LayoutParams.WRAP_CONTENT
        )
        submitButtonLayoutParams.addRule(
            RelativeLayout.ALIGN_LEFT,
            displayIdentityCheckBox.getId()
        )
        submitButtonLayoutParams.addRule(RelativeLayout.BELOW, displayIdentityCheckBox.getId())
        container.addView(submitButton, submitButtonLayoutParams)

        val greetingTextView: TextView = TextView(this)
        greetingTextView.setId(4)
        greetingTextView.setText(getString(R.string.greeting))
        greetingTextView.setTextSize(32)
        greetingTextView.setGravity(Gravity.CENTER)
        greetingTextView.setAlpha(0)
        val greetingTextViewLayoutParams: RelativeLayout.LayoutParams = LayoutParams(
            RelativeLayout.LayoutParams.MATCH_PARENT,
            RelativeLayout.LayoutParams.MATCH_PARENT
        )
        greetingTextViewLayoutParams.addRule(RelativeLayout.ALIGN_LEFT, submitButton.getId())
        greetingTextViewLayoutParams.addRule(RelativeLayout.BELOW, submitButton.getId())
        container.addView(greetingTextView, greetingTextViewLayoutParams)

        submitButton.setOnClickListener(object : OnClickListener() {
            fun onClick(view: View?) {
                val identity: String = introduceYourselfEditText.getText().toString()
                greetingTextView.setText(
                    getResources().getString(R.string.greeting).replace(
                        "???",
                        if ((displayIdentityCheckBox.isChecked())) identity else getResources().getString(
                            R.string.anonymous
                        )
                    )
                )
                greetingTextView.setAlpha(1)
                val fadeEffect: AlphaAnimation = AlphaAnimation(1.0f, 0.0f)
                fadeEffect.setDuration(TRANSPARENCY_EFFECT_DURATION)
                fadeEffect.setFillAfter(true)
                greetingTextView.setAnimation(fadeEffect)
            }
        })

        setContentView(container)
    }

    companion object {
        private const val TRANSPARENCY_EFFECT_DURATION: Long = 5000
    }
}
</code></pre>
</div>