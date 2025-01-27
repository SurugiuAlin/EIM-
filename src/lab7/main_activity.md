# MainActivity

Astazi vom implementa trei clase in aplicatia noastra de chat peste Bluetooth:

* `MainActivity` - Activitatea principala unde se va gasi interfata grafica a aplicatiei de chat
* `ChatUtils` - Clasa care va gestiona conexiunile Bluetooth și comunicarea între dispozitivele conectate.
* `DeviceListActivity` -  Clasă care afișează o listă de dispozitive Bluetooth disponibile și împerecheate, permițând utilizatorului să selecteze unul pentru a stabili o conexiune.

Aplicatia va avea urmatoarea interfata in care vom avea un meniu in partea de sus de unde
vom putea porni bluetooth-ul si selecta un dispozitiv cu care sa comunicam. In partea de jos
va fi un camp de text prin care vom trimite mesaje.

![](images/app_interface.png)

## 1. Descarcarea scheletului

Vom porni de la urmatorul schelet de cod.

> git clone https://github.com/eim-lab/Laborator-bt.git

## 2. Implementarea metodei initViews în clasa MainActivity:

Vom defini o fuctie numita `initViews` in care initializam componentele din interfata grafica.
De notat faptul a vom folosi un `ArrayAdapter` pentru a lega o sursa de date de un obiect din
interfata grafica.

```java
private void initViews() {
    ListView listMainChat = findViewById(R.id.list_conversation);
    edCreateMessage = findViewById(R.id.ed_enter_message);
    Button btnSendMessage = findViewById(R.id.btn_send_msg);

    // Adaptorul funcționează ca o legatura între Componenta UI și o sursa de date. 
    // Acesta convertește datele din sursele de date în elemente vizuale care pot fi afișate în Componenta UI.
    adapterMainChat = new ArrayAdapter<>(this, R.layout.message_layout);

    // Schimbarile din adaptor se vor vedea imediat in interfata grafica. In acest
    // exemplue, listMainChat de tip ListView va fi actualizata cand facem schimbari
    // la adapterMainChat
    listMainChat.setAdapter(adapterMainChat);

    // Butonul send va chema functia sendMessage pe care o vom defini mai tariu
    btnSendMessage.setOnClickListener(view -> sendMessage());
}
```

## 3. Implementarea metodei initBluetooth în clasa MainActivity:

Vom implementa o metoda `initBluetooth` care se ocupa de initilizarea unui adaptor de bluetooth.
In aceasta functie vom lua o referinta la dispozitivul Bluetooth sub forma unui `BluetoothAdapter`.

```java
private void initBluetooth() {
    // Vom lua o referinta la adaptorul de bluetooth
    // de pe telefon. Putem vedea acest adaptor ca o interfata
    // cu driver-ul de bluetooth.
    bluetoothAdapter = BluetoothAdapter.getDefaultAdapter();
    if (bluetoothAdapter == null) {
        Toast.makeText(this, "No bluetooth found", Toast.LENGTH_SHORT).show();
    }
}
```


## 4. Implementarea metodei onCreate în clasa MainActivity:

Initializam componentele vizuale, Bluetooth și clasa ChatUtils în metoda onCreate() a clasei MainActivity.

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_main);

    // Apelam functile create anterior
    initViews();
    initBluetooth();
    // Creeam o instanta a clasei ChatUtils. Clasa o vom
    // defini mai tarziu si o vom folosi pentru a
    // realiza comunicatia prin bluetooth pe un thread separat
    // de cel principal. Comunicatia dintr MainActivity si
    // ChatUtils se va face prin intermediul unei instante de
    // Handler.
    chatUtils = new ChatUtils(MainActivity.this, handler);
}
```


## 5. Implementarea metodei onResume în clasa MainActivity:

Asigurați-vă că metoda start() a clasei ChatUtils este apelată în metoda onResume() a clasei MainActivity.

```java
@Override
protected void onResume() {
    super.onResume();
    // Vom reponrni comunicatia cu chatUtils
    if (chatUtils != null && chatUtils.getState() == ChatUtils.STATE_NONE) {
        chatUtils.start();
    }
}
```


## 6. Crearea meniului pentru activitatea MainActivity:

Vom crea un meniu in care vom avea doua intrari:
* o intrare pentru activarea bluetooth-ului
* o intrare pentru a selecta la cine sa ne conectam din lista de dispozitive

In imaginea de mai jos intrarile sunt cele doua din dreapta: iconita bluetooth activeaza
bluetooth-ul pe device.

![](images/menu.png)


Pentru a crea un meniu trebuie dat click pe `res -> New -> Android Resource Directory`. Iar la **Resource Type** se va selecta "menu". Ulterior, se va adauga urmatorul fisier xml in cadrul acelui director.

![](images/create_menu.png)


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

<details>
<summary> menu_device_list.xml </summary>

```xml
<?xml version="1.0" encoding="utf-8"?>
<menu xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto">
    <item
        android:id="@+id/menu_scan_devices"
        android:icon="@drawable/ic_bluetooth_searching"
        android:title="@string/str_menu_scan_devices"
        app:showAsAction="always" />
</menu>
```

</details>

## 7. Implementarea metodelor onCreateOptionsMenu și onOptionsItemSelected în clasa MainActivity:

Meniul in android are doua functii atasate ce pot fi suprascris in `MainActivity`:
* onCreateOptionsMenu() - functia ce afiseaza meniul in interfata
* onOptionsItemSelected() - functia chemata atunci cand un obiect din meniu este selectat

Creați meniul pentru a permite activarea Bluetooth și căutarea altor dispozitive.

```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.menu_main_activity, menu);
    return super.onCreateOptionsMenu(menu);
}

@Override
public boolean onOptionsItemSelected(MenuItem item) {
    // Daca este selectata optiunea enablebluetooth, atunci
    // vom porni bluetooth-ul
    if (item.getItemId() == R.id.menu_enable_bluetooth) {
        enableBluetooth();
        return true;
    // daca este selectata optiunea de cautare de dispozitive
    // atunci va trebui sa cerem permisiuni de la utilizator
    } else if (item.getItemId() == R.id.menu_search_devices) {
        checkPermissions();
        return true;
    }
    return super.onOptionsItemSelected(item);
}
```

## 8. Implementarea metodei onActivityResult în clasa MainActivity:

Vom folosi o a doua activitate, `DeviceListActivity`, in care vom afisa lista cu toate dispozitivele ce au bluetooth pornit.
Utilizatorul va selecta un dispozitiv, iar aceasta activitate va returna adresa acestui dispozitiv.

Vom folosi datele carate de Intent pentru a realiza acest lucru. In acest sens vom suprascrie functia `onActivityResult`.

```java
@Override
protected void onActivityResult(int requestCode, int resultCode, Intent data) {
    int SELECT_DEVICE = 102;
    if (requestCode == SELECT_DEVICE && resultCode == RESULT_OK) {
        // daca activitatea DeviceListActivity a returnat un rezultat
        // acesta se va afla in deviceAddress
        String address = data.getStringExtra("deviceAddress");
        chatUtils.connect(bluetoothAdapter.getRemoteDevice(address));
    }
    super.onActivityResult(requestCode, resultCode, data);
}
```

## 9. Implementarea metodei enableBluetooth în clasa MainActivity:
Activați Bluetooth și faceți dispozitivul vizibil pentru alte dispozitive.


```java
private void enableBluetooth() {
    if (!bluetoothAdapter.isEnabled()) {
        if (ActivityCompat.checkSelfPermission(this, android.Manifest.permission.BLUETOOTH_CONNECT) != PackageManager.PERMISSION_GRANTED) {
            return;
        }
        // daca avem permisiunile necesare, pentru a porni bluetooth-ul vom chema
        // functia `enable()` pe adaptor.
        bluetoothAdapter.enable();
    }
    
    // cere permisiuni pentru scan si connect
    if (ActivityCompat.checkSelfPermission(this, BLUETOOTH_SCAN) != PackageManager.PERMISSION_GRANTED) {
        Log.d("Bluetooth", "No permission for scanning");
        requestPermissionLauncher.launch(BLUETOOTH_SCAN);
    }

    if (ActivityCompat.checkSelfPermission(this, BLUETOOTH_CONNECT) != PackageManager.PERMISSION_GRANTED) {
        Log.d("Bluetooth", "No permission for scanning");
        requestPermissionLauncher.launch(BLUETOOTH_CONNECT);
    }
    
    if (bluetoothAdapter.getScanMode() != BluetoothAdapter.SCAN_MODE_CONNECTABLE_DISCOVERABLE) {
        // De asemenea, vom porni scanarea de dispozitive folosind o intentie
        Intent discoveryIntent = new Intent(BluetoothAdapter.ACTION_REQUEST_DISCOVERABLE);
        discoveryIntent.putExtra(BluetoothAdapter.EXTRA_DISCOVERABLE_DURATION, 300);
        startActivity(discoveryIntent);
    }
}
```


## 10. Implementarea metodei sendMessage în clasa MainActivity:

In `MainActivity` vom defini o functie sendMessage. Aceasta va prelua
textul din interfata grafica si il va trimite catre `chatUtils`.
Ulterior, `chatUtils` va trimite mesajul prin intermediul conexiunii Bluetooth către alt dispozitiv.

```java
private void sendMessage() {
    String message = edCreateMessage.getText().toString();
    if (!message.isEmpty()) {
        edCreateMessage.setText("");
        chatUtils.write(message.getBytes());
    }
}
```


## 11. Implementarea metodei checkPermissions în clasa MainActivity:

Pentru a folosi bluetooth va trebui sa avem permisiunea de
locatie. Aceasta functie se va occupa de a face o cerere pentru
aceasta permisiune.


```java
private void checkPermissions() {
    if (ContextCompat.checkSelfPermission(this, ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
        requestPermissionLauncher.launch(ACCESS_FINE_LOCATION);
    } else {
        selectDeviceLauncher.launch(new Intent(this, DeviceListActivity.class));
    }
}
```

## 12. Implementarea metodei showPermissionDialog în clasa MainActivity:

Va trebui sa avem un cod boilerplate pentru a afisa in GUI dialogul
de permisiune.

```java
private void showPermissionDialog() {
    new AlertDialog.Builder(this)
            .setCancelable(false)
            .setMessage("Location permission is required.\nPlease grant")
            .setPositiveButton("Grant", (dialogInterface, i) -> checkPermissions())
            .setNegativeButton("Deny", (dialogInterface, i) -> finish()).show();
}
```

## 13. Implementarea metodei onDestroy în clasa MainActivity:
Închideți conexiunea Bluetooth la închiderea aplicației.

```java
@Override
protected void onDestroy() {
    super.onDestroy();
    if (chatUtils != null) {
        chatUtils.stop();
    }
}
```



