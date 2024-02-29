### Activity

**O activitate in android reprezinta o fereastra vizibila dintr-o aplicatie.**
O aplicație Android este formată din una sau mai multe activități (slab
cuplate între ele). Există întotdeauna o activitate principală care este
afișată atunci când aplicația Android este lansată în execuție inițial.

<img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*yd1E59p-wPXEgTOnYsyE-A.png" alt=""/>

O activitate poate invoca o altă activitate pentru a realiza diferite
sarcini, prin intermediul unui obiect de tip **intent**.

O activitate este formata din doua parti, partea de cod Java care
defineste ce se va intampla cand utilizatorul interactioneaza cu activitatea:

```java
 public class Activity extends ApplicationContext {
     ...
 }
```

Si intr-un mod similar cu HTML, un cod cod `XML` care este folosit pentru design-ul vizual al activitatii:

``` xml
<LinearLayout xmlns:android="http:*schemas.android.com/apk/res/android"
    xmlns:tools="http:*schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="wrap_content"
    android:paddingBottom="@dimen/activity_vertical_margin"
    android:paddingLeft="@dimen/activity_horizontal_margin"
    android:paddingRight="@dimen/activity_horizontal_margin"
    android:paddingTop="@dimen/activity_vertical_margin"
    android:orientation="vertical"
    tools:context="ro.pub.cs.systems.eim.lab02.graphicuserinterface.LifecycleMonitorActivity" >
```

In final, o activitate poate fi utilizată numai dacă este definită în fișierul
`AndroidManifest.xml`:

```xml
<manifest ... >
  <application ... >
      <activity android:name=".ExampleActivity" />
      ...
  </application ... >
  ...
</manifest >
```

Apare notiunea de **activitate principala**, prima activitate care este lansata atunci cand pornim aplicatia. 
O activitate principală din cadrul unei aplicații Android
este caracterizată prin următoarele proprietăți:

-   acțiunea are valoarea `android.intent.action.MAIN`, întrucât
    reprezintă punctul de intrare al aplicației Android;
-   categoria are valoarea `android.intent.category.LAUNCHER`, întrucât
    activitatea trebuie inclusă în meniul dispozitivului mobil pentru a
    putea fi lansată în execuție.


``` xml
<?xml version="1.0" encoding="utf-8"?>
<manifest ... >
  <!-- ... -->
  <application ... >
    <activity
      android:name=".LifecycleMonitorActivity"
      android:label="@string/app_name" >
      <intent-filter>
        <action android:name="android.intent.action.MAIN" />
        <category android:name="android.intent.category.LAUNCHER" />
      </intent-filter>
    </activity>
  </application>
</manifest>
```
