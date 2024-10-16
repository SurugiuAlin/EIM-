### LinearLayout (obligatoriu)

În cadrul unui grup de tip `LinearLayout`, componentele sunt dispuse fie
pe orizontală, fie pe verticală, în funcție de proprietatea
`orientation` (putând lua valorile `horizontal` - implicită sau
`vertical`).

![](images/linear_layout_vertical_sample.png)

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:orientation="vertical"
    android:padding="16dp">

    <Button
        android:id="@+id/btnMonday"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Monday"
        android:layout_marginBottom="8dp" />

    <Button
        android:id="@+id/btnTuesday"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Tuesday"
        android:layout_marginBottom="8dp" />

    <Button
        android:id="@+id/btnWednesday"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Wednesday"
        android:layout_marginBottom="8dp" />

    <Button
        android:id="@+id/btnThursday"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Thursday"
        android:layout_marginBottom="8dp" />

    <Button
        android:id="@+id/btnFriday"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Friday"
        android:layout_marginBottom="8dp" />

    <Button
        android:id="@+id/btnSaturday"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Saturday"
        android:layout_marginBottom="8dp" />

    <Button
        android:id="@+id/btnSunday"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:text="Sunday" />

</LinearLayout>
```
