#### MultiAutoCompleteTextView

Controlul de tip `MultiAutoCompleteTextView` permite ca sugestiile
oferite să țină cont de fiecare componentă a textului introdus. Mai
exact, va fi specificat un delimitator (prin intermediul metodei
`setTokenizer()`) după apariția căruia vor fi luate în considerare
caracterele pentru determinarea sugestiei. Android pune la dispoziție
câteva clase standard pentru delimitatori (`CommaTokenizer` - separare
prin virgulă, `Rfc822Tokenizer` - conținutul de tip adresă de poștă
electronică) însă se pot utiliza și clase definite de utilizator, care
implementează interfața `MultiAutoCompleteTextView.Tokenizer`.
