### Controale pentru gestiunea datei calendaristice și a timpului -- facultativ

Majoritatea bibliotecilor de controale pun la dispoziția dezvoltatorilor
componente pentru gestiunea informațiilor legate de data calendaristică
și timp. În Android, cele mai frecvent uzitate elemente de acest tip
sunt `DatePicker`, `TimePicker`, `AnalogClock` și `DigitalClock`.

![](images/date_time_samples.png)

#### DatePicker

Obiectul de tip `DatePicker` este folosit pentru gestiunea componentelor
unei date calendaristice (zi, lună, an).

Inițializarea unei astfel de componente se realizează prin metoda
`init()`, ce primește ca parametrii anul, luna, ziua și o clasă
ascultător (ce implementează interfața
`DatePicker.OnDateChangedListener` cu metoda `onDateChanged()`). De
regulă, evenimentele pe acest control nu sunt monitorizate, preluându-se
conținutul său la un moment de timp ulterior. În cazul în care nu se
specifică nici o valoare pentru acest control, va fi preluată data
calendaristică a sistemului Android.

Conținutul controlului se obține prin metodele `getDayOfMonth()`,
`getMonth()`, respectiv `getYear()`.

---
**Note**

Numerotarea unei luni se face pornind de la 0, astfel
încât valoarea furnizată de acest control va trebui incrementată.
Invers, la inițializarea conținutului unei componente de tip
`DatePicker`, se va realiza operația de decrementare înainte de
transmiterea unei date calendaristice.\

---

Valorile pe care le poate lua acest element pot fi controlate prin
intermediul proprietăților `minDate` (respectiv `minYear`) și `maxDate`
(respectiv `maxYear`). De asemenea, dacă se dorește sau nu afișarea unui
calendar va fi indicat prin intermediul proprietății
`calendarViewShown`.

#### TimePicker

Obiectul de tip `TimePicker` este folosit pentru gestiunea componentelor
timpului (oră, minut).

Inițializarea unei astfel de componente se realizează prin metodele
`setCurrentHour()`, respectiv `setCurrentMinute()` care primesc ca
parametrii obiecte de tip `Integer`. Clasa ascultător pentru
evenimentele produse în legătură cu acest obiect implementează interfața
`TimePicker.OnTimeChangedListener` și metoda `onTimeChanged()`. În cazul
în care nu se specifică nici o valoare pentru acest control, va fi
preluat timpul sistemului Android.

\<note>Formatul utilizat pentru oră (12/24 ore) se precizează prin
intermediul proprietății `is24HourView`.\

---

Conținutul controlului se obține prin metodele `getCurrentHour()`,
respectiv `getCurrentMinute()`.

#### AnalogClock

Obiectul de tip `AnalogClock` este folosit pentru afișarea timpului
curent, folosind un ceas analogic. Utilizatorul nu poate interacționa cu
un astfel de control, actualizarea conținutului său fiind realizată în
mod automat, la fiecare minut.

---
**Note**

Un obiect de tip `AnalogClock` poate fi particularizat în
sensul că se pot specifica anumite resurse grafice pentru afișarea
cadranului orar și a limbilor care indică ora și minutul.\

---
#### TextClock (nivel API \>= 17)

Obiectul de tip `TextClock` este folosit pentru afișarea datei
calendaristice și/sau a timpului curent (folosind formatul 12/24 ore și
permițând schimbarea zonei de timp).

Implicit, acest control nu afișează și secundele.

#### Chronometer

Un obiect de tip `Chronometer` este utilizat pentru monitorizarea
timpului scurs începând de la un anumit moment, pentru activitățile în
care un astfel de element este esențial.

Modul în care este afișat contorul ce indică trecerea timpului este
controlat prin intermediul parametrului `android:format`:

-   `%h` - număr de ore;
-   `%m` - număr de minute;
-   `%s` - număr de secunde.

Cronometrarea propriu-zisă este realizată între apelurile metodelor
`start()`, respectiv `stop()`. De asemenea, se poate indica momentul de
timp care este considerat drept referință pentru numărătoare, prin
intermediul metodei `setBase()`. Pornirea de la 0 se face transmițând
metodei `setBase()` un parametru de tip
`android.os.SystemClock.elapsedRealTime()`.

Monitorizarea evenimentelor legate de un obiect de tip `Chronometer` se
face prin implementarea unui obiect ascultător de tip
`Chronometer.OnChronometerTickListener` prin (re)definirea metodei
`onChronometerTick()`.
