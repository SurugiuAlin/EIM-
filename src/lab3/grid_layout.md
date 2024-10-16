### GridLayout

Layout-ul de tip `GridLayout` este utilizat tot pentru dispunerea
componentelor într-un format tabelar, folosind însă o sintaxă mult mai
flexibilă. Totodată, acest mecanism este și mult mai eficient din
punctul de vedere al randării.

![](images/grid_layout_sample.png)

Astfel, pentru specificarea numărului de rânduri și de
coloane se vor utiliza proprietățile `rowCount` și `columnCount`,
indicându-se pentru fiecare element grafic în parte poziția la care va
fi plasat, prin atributele `layout_row` și `layout_column`. În cazul în
care pentru o componentă grafică nu se specifică linia sau coloana din
care face parte, atributul `orientation` (având va valori posibile
`horizontal` sau `vertical` indică dacă elementul următor va fi plasat
pe linia sau pe coloana succesivă).

În cazul în care se dorește extinderea unui element grafic pe mai multe
rânduri sau pe mai multe coloane, se vor utiliza atributele
`layout_rowSpan` și `layout_columnSpan`. Pentru controlul modului de
dispunere se va folosi proprietatea `layout_gravity`. Precizarea
`layout_width` și `layout_height` nu este neapărat necesară, valoarea
lor implicită în acest caz fiind `wrap_content`.


```xml
<?xml version="1.0" encoding="utf-8"?>
<GridLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:columnCount="2"
    android:rowCount="3"
    android:padding="16dp">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Name:"
        android:layout_column="0"
        android:layout_row="0"
        android:layout_marginEnd="8dp" />

    <EditText
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_column="1"
        android:layout_row="0"
        android:layout_gravity="fill_horizontal" />

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Email:"
        android:layout_column="0"
        android:layout_row="1"
        android:layout_marginEnd="8dp" />

    <EditText
        android:layout_width="0dp"
        android:layout_height="wrap_content"
        android:layout_column="1"
        android:layout_row="1"
        android:layout_gravity="fill_horizontal" />

    <Button
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Submit"
        android:layout_column="0"
        android:layout_row="2"
        android:layout_columnSpan="2"
        android:layout_gravity="center_horizontal" />

</GridLayout>
```
