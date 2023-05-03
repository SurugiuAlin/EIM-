# Aplicație de Chat folosind Bluetooth

Acest tutorial pas cu pas vă va arăta cum să creați o aplicație de chat folosind Bluetooth. Vom trece prin următoarele etape:

1. [Introducere](#introducere)
2. [Permisiuni](#permisiuni)
3. [Activarea Bluetooth](#activarea-bluetooth)
4. [Descoperirea dispozitivelor](#descoperirea-dispozitivelor)
5. [Conectarea dispozitivelor](#conectarea-dispozitivelor)
6. [Trimiterea și primirea mesajelor](#trimiterea-și-primirea-mesajelor)
7. [Încheiere](#încheiere)

## Introducere <a name="introducere"></a>

În acest tutorial, vom crea o aplicație de chat care va utiliza Bluetooth pentru a comunica între dispozitive Android. Vom explora cum să obținem permisiunile necesare, să activăm și să gestionăm Bluetooth, să descoperim și să ne conectăm la alte dispozitive și să trimitem și să primim mesaje.

## Permisiuni <a name="permisiuni"></a>

Pentru a utiliza funcționalitatea Bluetooth, va trebui să adăugați următoarele permisiuni în fișierul `AndroidManifest.xml`:

```xml
<uses-permission android:name="android.permission.BLUETOOTH"/>
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
```

## Activarea Bluetooth <a name="activarea-bluetooth"></a>
Pentru a activa Bluetooth pe dispozitiv, vom folosi BluetoothAdapter. Mai întâi, obțineți o referință la adaptatorul Bluetooth, apoi verificați dacă Bluetooth este activat. Dacă nu este activat, solicitați utilizatorului să activeze Bluetooth.

## Descoperirea dispozitivelor <a name="descoperirea-dispozitivelor"></a>
Pentru a descoperi alte dispozitive Bluetooth, vom utiliza metoda startDiscovery() a BluetoothAdapter. De asemenea, vom înregistra un BroadcastReceiver pentru a primi informații despre dispozitivele descoperite.

## Conectarea dispozitivelor <a name="conectarea-dispozitivelor"></a>
După ce am descoperit alte dispozitive, vom crea o conexiune între dispozitivele noastre, folosind clasele BluetoothServerSocket și BluetoothSocket.

## Trimiterea și primirea mesajelor <a name="trimiterea-și-primirea-mesajelor"></a>
Odată ce conexiunea este stabilită, vom utiliza InputStream și OutputStream pentru a trimite și a primi mesaje între dispozitive.

## Încheiere <a name="încheiere"></a>
La finalul acestui tutorial, veți avea o aplicație funcțională de chat care utilizează Bluetooth pentru a comunica între dispozitive Android.
