#### ToggleButton

Un obiect `ToggleButton` (definit de `android.widget.ToggleButton`) este
un tip de buton care are asociată o stare cu două valori (selectat și
neselectat), asemenea unui checkbox sau radiobutton. Implicit, atunci
când este selectat, acesta afișează o bară de culoare albastră în partea
sa inferioară, iar atunci când nu este selectat, o bară de culoare gri.

Textele afișate pentru valorile stărilor pot fi controlate în
fișierul XML prin intermediul proprietăților `android:textOn` respectiv
`android:textOff`, iar programatic prin metodele `setTextOn()` și
`setTextOff()`.

---
**Note**

Valorile implicite pentru proprietățile `textOn` și `textOff`
sunt *ON*, respectiv *OFF*.\

---

**Note**

Atributul `text`, moștenit de la obiectul de tip `Button`, nu
este utilizat cu toate că poate fi definit.\
