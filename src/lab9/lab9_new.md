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
La finalul acestui tutorial, veți avea o aplicație funcțională de chat care utilizează Bluetooth pentru a comunica între dispozitive Android. Veți înțelege conceptele de bază

## 1. Configurarea proiectului în Android Studio:
Creați un nou proiect Android în Android Studio, folosind o temă compatibilă cu AppCompatActivity. Adăugați următoarele dependințe în build.gradle:

<details>
    <summary> build.gradle (Module) </summary>
    
```xml
implementation 'androidx.activity:activity-result:1.3.1'
implementation 'androidx.appcompat:appcompat:1.3.1'
```
</details>

## 2. Crearea layout-ului aplicației:
Creați layout-ul pentru activitatea principală, care include un ListView pentru afișarea mesajelor și un EditText cu un buton pentru trimiterea mesajelor.

<details>
    <summary> activity_main.xml </summary>
<LinearLayout
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <ListView
        android:id="@+id/list_conversation"
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1" />

    <LinearLayout
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:orientation="horizontal">

        <EditText
            android:id="@+id/ed_enter_message"
            android:layout_width="0dp"
            android:layout_height="wrap_content"
            android:layout_weight="1"
            android:hint="Enter your message" />

        <Button
            android:id="@+id/btn_send_msg"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="Send" />
    </LinearLayout>
</LinearLayout>
</details>

## 3. Crearea clasei ChatUtils:
Creați clasa ChatUtils pentru a gestiona conexiunile Bluetooth și comunicarea între dispozitive.

<details>
    <summary> ChatUtils.java </summary>

```java
public class ChatUtils {
    // Class implementation
}
```

</details>

## 4. Implementarea metodei onCreate în clasa MainActivity:
Initializați componentele vizuale, Bluetooth și clasa ChatUtils în metoda onCreate() a clasei MainActivity.

<details>
    <summary> onCreate() </summary>

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    initViews();
    initBluetooth();
    chatUtils = new ChatUtils(MainActivity.this, handler);
}
```

</details>

## 5. Implementarea metodei onResume în clasa MainActivity:
Asigurați-vă că metoda start() a clasei ChatUtils este apelată în metoda onResume() a clasei MainActivity.

<details>
    <summary> onResume() </summary>

```java
@Override
protected void onResume() {
    super.onResume();
    if (chatUtils != null && chatUtils.getState() == ChatUtils.STATE_NONE) {
        chatUtils.start();
    }
}
```
</details>

## 6. Implementarea metodei initViews în clasa MainActivity:
<details>
    <summary> initViews() </summary>

```java
private void initViews() {
    ListView listMainChat = findViewById(R.id.list_conversation);
    edCreateMessage = findViewById(R.id.ed_enter_message);
    Button btnSendMessage = findViewById(R.id.btn_send_msg);

    adapterMainChat = new ArrayAdapter<>(this, R.layout.message_layout);
    listMainChat.setAdapter(adapterMainChat);

    btnSendMessage.setOnClickListener(view -> sendMessage());
}
```
</details>

## 7. Implementarea metodei initBluetooth în clasa MainActivity:
<details>
    <summary> initBluetooth() </summary>

```java
private void initBluetooth() {
    bluetoothAdapter = BluetoothAdapter.getDefaultAdapter();
    if (bluetoothAdapter == null) {
        Toast.makeText(this, "No bluetooth found", Toast.LENGTH_SHORT).show();
    }
}
```
</details>


## 8. Crearea meniului pentru activitatea MainActivity:
<details>
    <summary> menu_main_activity.xml </summary>

```xml
<menu xmlns:android="http://schemas.android.com/apk/res/android">
    <item
        android:id="@+id/menu_enable_bluetooth"
        android:title="Enable Bluetooth" />
    <item
        android:id="@+id/menu_search_devices"
        android:title="Search Devices" />
</menu>
```
</details>

## 9. Implementarea metodelor onCreateOptionsMenu și onOptionsItemSelected în clasa MainActivity:
Creați meniul pentru a permite activarea Bluetooth și căutarea altor dispozitive.

<details>
    <summary> onCreateOptionsMenu() și onOptionsItemSelected() </summary>

```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.menu_main_activity, menu);
    return super.onCreateOptionsMenu(menu);
}

@Override
public boolean onOptionsItemSelected(MenuItem item) {
    if (item.getItemId() == R.id.menu_enable_bluetooth) {
        enableBluetooth();
        return true;
    } else if (item.getItemId() == R.id.menu_search_devices) {
        checkPermissions();
        return true;
    }
    return super.onOptionsItemSelected(item);
}
```

</details>

## 10. Implementarea metodei onActivityResult în clasa MainActivity:
Gestionați rezultatul activității DeviceListActivity pentru a obține adresa dispozitivului selectat și conectați-vă la acesta.

<details>
    <summary> onActivityResult() </summary>

```java
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    int SELECT_DEVICE = 102;
    if (requestCode == SELECT_DEVICE && resultCode == RESULT_OK) {
        String address = data.getStringExtra("deviceAddress");
        chatUtils.connect(bluetoothAdapter.getRemoteDevice(address));
    }
    super.onActivityResult(requestCode, resultCode, data);
}
```
</details>

## 11. Implementarea metodei enableBluetooth în clasa MainActivity:
Activați Bluetooth și faceți dispozitivul vizibil pentru alte dispozitive.

<details>
    <summary> enableBluetooth() </summary>

```java
private void enableBluetooth() {
    if (!bluetoothAdapter.isEnabled()) {
        if (ActivityCompat.checkSelfPermission(this, android.Manifest.permission.BLUETOOTH_CONNECT) != PackageManager.PERMISSION_GRANTED) {
            return;
        }
        bluetoothAdapter.enable();
    }

    if (bluetoothAdapter.getScanMode() != BluetoothAdapter.SCAN_MODE_CONNECTABLE_DISCOVERABLE) {
        Intent discoveryIntent = new Intent(BluetoothAdapter.ACTION_REQUEST_DISCOVERABLE);
        discoveryIntent.putExtra(BluetoothAdapter.EXTRA_DISCOVERABLE_DURATION, 300);
        startActivity(discoveryIntent);
    }
}
```
</details>

## 12. Implementarea metodei sendMessage în clasa MainActivity:
Trimiteți mesaje prin intermediul conexiunii Bluetooth către alt dispozitiv.

<details>
    <summary> sendMessage() </summary>

```java
private void sendMessage() {
    String message = edCreateMessage.getText().toString();
    if (!message.isEmpty()) {
        edCreateMessage.setText("");
        chatUtils.write(message.getBytes());
    }
}
```
</details>

## 13. Implementarea metodei checkPermissions în clasa MainActivity:
<details>
    <summary> checkPermissions() </summary>

```java
private void checkPermissions() {
    if (ContextCompat.checkSelfPermission(this, ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
        requestPermissionLauncher.launch(ACCESS_FINE_LOCATION);
    } else {
        selectDeviceLauncher.launch(new Intent(this, DeviceListActivity.class));
    }
}
```
</details>

## 14. Implementarea metodei showPermissionDialog în clasa MainActivity:
<details>
    <summary> showPermissionDialog() </summary>

```java
private void showPermissionDialog() {
    new AlertDialog.Builder(this)
            .setCancelable(false)
            .setMessage("Location permission is required.\nPlease grant")
            .setPositiveButton("Grant", (dialogInterface, i) -> checkPermissions())
            .setNegativeButton("Deny", (dialogInterface, i) -> finish()).show();
}
```
</details>

## 15. Implementarea metodei onDestroy în clasa MainActivity:
Închideți conexiunea Bluetooth la închiderea aplicației.

<details>
    <summary> onDestroy() </summary>

```java
@Override
protected void onDestroy() {
    super.onDestroy();
    if (chatUtils != null) {
        chatUtils.stop();
    }
}
```
</details>
