# Bluetooth

Bluetooth, din perspectiva dezvoltării pe Android, reprezintă o tehnologie wireless esențială care permite dispozitivelor să comunice între ele pe distanțe scurte. Android oferă un API extins pentru [Bluetooth](https://developer.android.com/develop/connectivity/bluetooth), care permite dezvoltatorilor să realizeze diverse funcționalități, de la transferul simplu de date până la gestionarea conexiunilor complexe între dispozitive.

API-ul Bluetooth în Android este împărțit în două categorii principale:

- [**Bluetooth clasic**]((https://developer.android.com/develop/connectivity/bluetooth)) - Este folosit pentru comunicarea punct-la-punct între dispozitive, ideal pentru transferul de date la volum mare, cum ar fi fișierele audio sau datele de pe un dispozitiv periferic. Este utilizat frecvent în cazul căștilor, difuzoarelor și al altor dispozitive de periferie.

- [**Bluetooth Low Energy (BLE)**](https://developer.android.com/develop/connectivity/bluetooth/ble/ble-overview) - Cunoscut și sub numele de Bluetooth 4.0+, este optimizat pentru consum redus de energie, fiind ideal pentru dispozitivele și senzorii care necesită transferuri de date mici și ocazionale. BLE este utilizat adesea în dispozitive wearable, dispozitive de urmărire a fitnessului și alte gadgeturi inteligente.

API-ul Android pentru Bluetooth permite dezvoltatorilor să execute o serie de acțiuni, inclusiv:

- **Scanarea dispozitivelor** Bluetooth din apropiere și afișarea informațiilor despre acestea.
- **Inițializarea conexiunilor** între dispozitive și gestionarea datelor transmise.
- **Crearea unui server Bluetooth** pe dispozitiv, care poate accepta conexiuni de la alte dispozitive.
- **Gestionarea dispozitivelor asociate**  și păstrarea unei liste a dispozitivelor cunoscute.
- **Comunicarea cu profiluri Bluetooth specifice**, cum ar fi A2DP (Advanced Audio Distribution Profile) pentru transmiterea audio sau HFP (Hands-Free Profile) pentru apeluri telefonice.

Pentru a utiliza Bluetooth în aplicațiile Android, dezvoltatorii trebuie să includă permisiunile necesare în fișierul manifest al aplicației și, în cazul accesului la BLE, să verifice dacă dispozitivul suportă BLE.

Pentru a utiliza funcționalitatea Bluetooth, va trebui să adăugați următoarele [permisiuni](https://developer.android.com/develop/connectivity/bluetooth/bt-permissions) în fișierul `AndroidManifest.xml`:

```xml
    <uses-permission android:name="android.permission.BLUETOOTH" />
    <uses-permission android:name="android.permission.BLUETOOTH_ADMIN" />
    <uses-permission android:name="android.permission.ACCESS_FINE_LOCATION" />
    <uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION" />

    <uses-feature android:name="android.hardware.bluetooth_le" android:required="true" />

    <uses-permission android:name="android.permission.BLUETOOTH_ADVERTISE" />
    <uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
    <uses-permission android:name="android.permission.BLUETOOTH_SCAN" />
```
## [BlueetoothAdapter](https://developer.android.com/reference/android/bluetooth/BluetoothAdapter)
Pentru a activa Bluetooth pe dispozitiv, vom folosi BluetoothAdapter. Mai întâi, obțineți o referință la adaptatorul Bluetooth, apoi verificați dacă Bluetooth este activat. Dacă nu este activat, solicitați utilizatorului să activeze Bluetooth.

## [Descoperirea dispozitivelor](https://developer.android.com/develop/connectivity/bluetooth/find-bluetooth-devices)
Pentru a descoperi alte dispozitive Bluetooth, vom utiliza metoda startDiscovery() a BluetoothAdapter. De asemenea, vom înregistra un BroadcastReceiver pentru a primi informații despre dispozitivele descoperite.

## Conectarea dispozitivelor
După ce am descoperit alte dispozitive, vom crea o conexiune între dispozitivele noastre, folosind clasele [**BluetoothServerSocket**](https://developer.android.com/reference/android/bluetooth/BluetoothServerSocket) și [**BluetoothSocket**](https://developer.android.com/reference/android/bluetooth/BluetoothSocket)

## Trimiterea și primirea mesajelor
Odată ce conexiunea este stabilită, vom utiliza [InputStream](https://developer.android.com/reference/java/io/InputStream) și [OutputStream](https://developer.android.com/reference/java/io/OutputStream) pentru a trimite și a primi mesaje între dispozitive.

