# DeviceListActivity

Vom utiliza o a doua activitate pentru a selecta un dispozitiv bluetooth la care vrem sa ne conectam.

DeviceListActivity este o clasă care afișează o listă de dispozitive Bluetooth disponibile și împerecheate, permițând utilizatorului să selecteze unul pentru a stabili o conexiune. Aceasta va returna catre `MainActivity` id-ul dispozitivului selectat prin intermediul unui intent.

1. Metoda `onCreate()` inițializează activitatea și layout-ul, apoi apelează metoda `init()`.

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_device_list);
    init();
}
```

2. Metoda `init()` inițializează componentele interfeței și înregistrează BroadcastReceiver pentru a detecta dispozitivele Bluetooth disponibile.


```java
private void init() {
    // codul de inițializare a componentelor UI
    ListView listPairedDevices = findViewById(R.id.list_paired_devices);
    ListView listAvailableDevices = findViewById(R.id.list_available_devices);
    progressScanDevices = findViewById(R.id.progress_scan_devices);

    adapterPairedDevices = new ArrayAdapter<>(this, R.layout.device_list_item);
    adapterAvailableDevices = new ArrayAdapter<>(this, R.layout.device_list_item);

    listPairedDevices.setAdapter(adapterPairedDevices);
    listAvailableDevices.setAdapter(adapterAvailableDevices);

    listAvailableDevices.setOnItemClickListener(this::onDeviceClick);
    listPairedDevices.setOnItemClickListener(this::onDeviceClick);

    // adapter-ul
    bluetoothAdapter = BluetoothAdapter.getDefaultAdapter();
    populatePairedDevices();

    // inregistrarea actiunilor pt broadcastReceiver
    registerReceiver(bluetoothDeviceListener, new IntentFilter(BluetoothDevice.ACTION_FOUND));
    registerReceiver(bluetoothDeviceListener, new IntentFilter(BluetoothAdapter.ACTION_DISCOVERY_FINISHED));
}
```

3. Metoda `onDeviceClick()` este apelată atunci când utilizatorul selectează un dispozitiv din listă. Aceasta oprește procesul de descoperire și trimite adresa dispozitivului selectat ca rezultat.


```java
private void onDeviceClick(AdapterView<?> adapterView, View view, int i, long l) {
    // verificarea permisiunilor
    if (ActivityCompat.checkSelfPermission(this, android.Manifest.permission.BLUETOOTH_SCAN) != PackageManager.PERMISSION_GRANTED) {
        return;
    }

    bluetoothAdapter.cancelDiscovery();

    String info = ((TextView) view).getText().toString();
    String address = info.substring(info.length() - 17);

    // Returnam printr-o intentie id-ul dispozitivului catre activitatea principala.
    Intent intent = new Intent();
    intent.putExtra("deviceAddress", address);
    setResult(RESULT_OK, intent);
    finish();
}
```

4. Metoda `populatePairedDevices()` adaugă dispozitivele împerecheate în lista corespunzătoare.

```java
private void populatePairedDevices() {
    // ... verificarea permisiunilor
    Set<BluetoothDevice> pairedDevices = bluetoothAdapter.getBondedDevices();
    if (pairedDevices != null && pairedDevices.size() > 0) {
        for (BluetoothDevice device : pairedDevices) {
            adapterPairedDevices.add(device.getName() + "\n" + device.getAddress());
        }
    }
}
```
5. Metoda `onDiscoveryFinished()` este apelată atunci când procesul de descoperire a dispozitivelor Bluetooth este finalizat.

```java
private void onDiscoveryFinished() {
    progressScanDevices.setVisibility(View.GONE);
    int availableDevicesCount = adapterAvailableDevices.getCount();
    Toast.makeText(this, availableDevicesCount == 0 ? "No new devices found" : "Click on the device to start the chat", Toast.LENGTH_SHORT).show();
}
```

6. Metoda `scanDevices()` inițiază procesul de scanare a dispozitivelor Bluetooth disponibile.

```java
private void scanDevices() {
    progressScanDevices.setVisibility(View.VISIBLE);
    adapterAvailableDevices.clear();
    Toast.makeText(this, "Scan started", Toast.LENGTH_SHORT).show();
    if (bluetoothAdapter.isDiscovering()) {
        bluetoothAdapter.cancelDiscovery();
    }

    bluetoothAdapter.startDiscovery();
}
```


7. Metoda `onCreateOptionsMenu()` creează meniul din activitate.


```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.menu_device_list, menu);
    return super.onCreateOptionsMenu(menu);
}
```

8. Metoda `onOptionsItemSelected()` gestionează acțiunea de apăsare a butonului "Scan devices" din meniul activității.

```java
@Override
public boolean onOptionsItemSelected(MenuItem item) {
    if (item.getItemId() == R.id.menu_scan_devices) {
        scanDevices();
        return true;
    }
    return super.onOptionsItemSelected(item);
}
```

## BroadcastReceiver bluetoothDeviceListener
`bluetoothDeviceListener` este un `BroadcastReceiver` care ascultă pentru evenimentele de dispozitive Bluetooth găsite și finalizarea descoperirii dispozitivelor.

```java
private final BroadcastReceiver bluetoothDeviceListener = new BroadcastReceiver() {
    @Override
    public void onReceive(Context context, Intent intent) {
        String action = intent.getAction();

        if (BluetoothDevice.ACTION_FOUND.equals(action)) {
            BluetoothDevice device = intent.getParcelableExtra(BluetoothDevice.EXTRA_DEVICE);
            // ... verificarea permisiunilor
            if (device.getBondState() != BluetoothDevice.BOND_BONDED) {
                adapterAvailableDevices.add(device.getName() + "\n" + device.getAddress());
            }
        } else if (BluetoothAdapter.ACTION_DISCOVERY_FINISHED.equals(action)) {
            onDiscoveryFinished();
        }
    }
};
```


Metoda `onDestroy()` este apelată atunci când activitatea este distrusă și se ocupă de dezînregistrarea BroadcastReceiver.


```java
@Override
protected void onDestroy() {
    super.onDestroy();
    unregisterReceiver(bluetoothDeviceListener);
}
```

