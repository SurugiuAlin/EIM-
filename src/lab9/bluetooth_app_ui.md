# Clasa DeviceListActivity
DeviceListActivity este o clasă care afișează o listă de dispozitive Bluetooth disponibile și împerecheate, permițând utilizatorului să selecteze unul pentru a stabili o conexiune.

1. Metoda `onCreate()` inițializează activitatea și layout-ul, apoi apelează metoda `init()`.
<details>
<summary>onCreate()</summary>

```java
@Override
protected void onCreate(Bundle savedInstanceState) {
    super.onCreate(savedInstanceState);
    setContentView(R.layout.activity_device_list);
    init();
}
```
</details>

2. Metoda `init()` inițializează componentele interfeței și înregistrează BroadcastReceiver pentru a detecta dispozitivele Bluetooth disponibile.
<details>
<summary>init()</summary>

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
</details>

3. Metoda `onDeviceClick()` este apelată atunci când utilizatorul selectează un dispozitiv din listă. Aceasta oprește procesul de descoperire și trimite adresa dispozitivului selectat ca rezultat.
<details>
<summary> onDeviceClick()</summary>

```java
private void onDeviceClick(AdapterView<?> adapterView, View view, int i, long l) {
    // verificarea permisiunilor
    if (ActivityCompat.checkSelfPermission(this, android.Manifest.permission.BLUETOOTH_SCAN) != PackageManager.PERMISSION_GRANTED) {
        return;
    }

    bluetoothAdapter.cancelDiscovery();

    String info = ((TextView) view).getText().toString();
    String address = info.substring(info.length() - 17);

    Intent intent = new Intent();
    intent.putExtra("deviceAddress", address);
    setResult(RESULT_OK, intent);
    finish();
}
```
</details>

4. Metoda `populatePairedDevices()` adaugă dispozitivele împerecheate în lista corespunzătoare.
<details>
<summary>populatePairedDevices()</summary>

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
</details>

5. Metoda `onDiscoveryFinished()` este apelată atunci când procesul de descoperire a dispozitivelor Bluetooth este finalizat.

<details>
<summary>onDiscoveryFinished()</summary>

```java
private void onDiscoveryFinished() {
    progressScanDevices.setVisibility(View.GONE);
    int availableDevicesCount = adapterAvailableDevices.getCount();
    Toast.makeText(this, availableDevicesCount == 0 ? "No new devices found" : "Click on the device to start the chat", Toast.LENGTH_SHORT).show();
}
```
</details>

6. Metoda `scanDevices()` inițiază procesul de scanare a dispozitivelor Bluetooth disponibile.
<details>
<summary>scanDevices()</summary>

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
</details>

</details>

7. Metoda `onCreateOptionsMenu()` creează meniul din activitate.
<details>
<summary> onCreateOptionsMenu()</summary>


```java
@Override
public boolean onCreateOptionsMenu(Menu menu) {
    getMenuInflater().inflate(R.menu.menu_device_list, menu);
    return super.onCreateOptionsMenu(menu);
}
```
</details>

8. Metoda `onOptionsItemSelected()` gestionează acțiunea de apăsare a butonului "Scan devices" din meniul activității.
<details>
<summary>onOptionsItemSelected()</summary>

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
</details>

## BroadcastReceiver bluetoothDeviceListener
`bluetoothDeviceListener` este un `BroadcastReceiver` care ascultă pentru evenimentele de dispozitive Bluetooth găsite și finalizarea descoperirii dispozitivelor.

<details>
    <summary> BroadcastReceiver </summary>

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

</details>

Metoda `onDestroy()` este apelată atunci când activitatea este distrusă și se ocupă de dezînregistrarea BroadcastReceiver.
<details>
<summary> onDestroy()</summary>

```java
@Override
protected void onDestroy() {
    super.onDestroy();
    unregisterReceiver(bluetoothDeviceListener);
}
```
</details>

