### Versiuni Android

Ca majoritatea sistemelor de operare, Android foloseste un release pe versiuni.
Aceste versiuni aduc schimbari fie in functionalitate oferita utilizatorului, dar si in cea pentru 
dezvoltator sub forma de schimbari la API. Mai jos avem cateva exemple de versiuni Android si unele din
modificarile aduse.

## Android 4.4 KitKat (API level 19) - Released in 2013

- **API change:** Introduction of the `TransitionManager` class for creating animations between scenes.
- **Functionality:** Added "OK Google" voice command support for hands-free operation.

## Android 10 (API level 29) - Released in 2019

- **API change:** Introduction of the system-wide dark theme and APIs to support it.
- **Functionality:** Enhanced location privacy controls, allowing users to give apps location access only while the app is in use.

Example of supporting dark theme in XML:

```xml
<style name="AppTheme" parent="Theme.AppCompat.DayNight">
    <!-- Theme colors -->
</style>
```
