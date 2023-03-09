#### ImageButton

Un obiect de tip `ImageButton` (definit de clasa
`android.widget.ImageButton`) este utilizat pentru afişarea unei
imagini, specificată în fişierul XML prin proprietatea `android:src` sau
programatic prin intermediul metodei `setImageResource()`.

\<spoiler> ---
**Note**

Imaginea asociată unui buton de tip `ImageButton`
este o resursă din directorul `/res/drawable/` (accesibilă în XML prin
adnotarea `@drawable/` sau programatic prin referinţa sa din clasa
`R.drawable`. \

---

Formatele suportate sunt `png`, `jpeg`, `gif` și `bmp`.

Dacă se doreşte să se omită afişarea propriu-zisă a butonului,
reţinându-se doar imaginea sa, se poate specifica un fundal vid (în XML,
`android:background="@null"` sau în codul sursă se poate apela
`setBackground(null)`).

Un buton de tip `ImageButton` poate avea şi una din următoarele stări:

-   `focus` - dacă este controlul ce captează toate evenimentele (în
    cazul în care selecția a fost mutată pe el)
-   `pressed` - dacă este apăsat de utilizator (înainte ca evenimentul
    corespunzător să fie procesat)

În funcție de aceste stări, unui buton de tip `ImageButton` i se pot
asocia diferite imagini, specificate într-un fișier XML din directorul
`/res/drawable`, care va fi referit ulterior ca sursă a acestuia:

``` xml
<?xml version="1.0" encoding="utf-8"?>
<selector xmlns:android="http:*schemas.android.com/apk/res/android">
  <item android:state_pressed="true"
        android:drawable="@drawable/button_pressed" />
  <item android:state_focused="true"
        android:drawable="@drawable/button_focused" />
  <item android:drawable="@drawable/button" />
</selector>
```

``` xml
<Button
  ... 
  android:src="@drawable/imagebuttonselector" 
  ... />
```

---
**Note**

Ordinea elementelor în fișierul XML pentru realizarea
selecției este important întrucât Android îl va verifica pe fiecare în
parte pentru a vedea dacă acesta corespunde stării controlului. De
aceea, imaginea pentru starea normală a controlului trebuie să se
regăsească întotdeauna după toate celelalte cazuri particulare, în caz
contrar aceasta fiind afișată întotdeauna de vreme ce nu impune nici o
restricție asupra componentei.\

--- \</spoiler>
