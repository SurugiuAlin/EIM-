# Clasa ChatUtils
Clasa ChatUtils gestionează conexiunile Bluetooth și comunicarea între dispozitivele conectate.


## Constructor
Constructorul inițializează handler, context, state și bluetoothAdapter.
Cand se va importa `Handler`-ul, se va alege cel din `android.os`.
<details>
<summary>Constructorul</summary>

```java
public ChatUtils(Context context, Handler handler) {
    this.handler = handler;
    this.context = context;
    state = STATE_NONE;
    bluetoothAdapter = BluetoothAdapter.getDefaultAdapter();
}
```
</details>

## Gestionarea stării
Metodele getState() și setState() permit obținerea și modificarea stării conexiunii si trimiterea unui mesaj handle-urului cu noua stare.

<details>
<summary>Metode pentru gestionarea stării</summary>

```java
public int getState() {
    return state;
}

public synchronized void setState(int state) {
    this.state = state;
    handler.obtainMessage(MainActivity.MESSAGE_STATE_CHANGED, state, -1).sendToTarget();
}
```
</details>

## Gestionarea conexiunilor
Metodele start(), stop(), connect(), și write() permit inițierea, oprirea, conectarea și trimiterea de mesaje între dispozitive.

<details>
<summary>Metode pentru gestionarea conexiunilor</summary>

### Start()
Această metodă anulează thread-urile connectThread și connectedThread, creează și pornește un nou thread acceptThread, și setează starea conexiunii la STATE_LISTEN.
```java
public synchronized void start() {
    cancelConnectThread();
    createAndStartAcceptThread();
    cancelConnectedThread();
    setState(STATE_LISTEN);
}
```

### Stop()
Această metodă anulează toate thread-urile și setează starea conexiunii la STATE_NONE.

```java
public synchronized void stop() {
    cancelConnectThread();
    cancelAcceptThread();
    cancelConnectedThread();
    setState(STATE_NONE);
}
```

### Connect()
Această metodă inițiază o conexiune cu un dispozitiv Bluetooth specificat, anulând thread-urile connectThread și connectedThread dacă este necesar, și setând starea conexiunii la STATE_CONNECTING.

```java
public void connect(BluetoothDevice device) {
    if (state == STATE_CONNECTING) {
        cancelConnectThread();
    }
    createAndStartConnectThread(device);
    cancelConnectedThread();
    setState(STATE_CONNECTING);
}
```
### Write()
Această metodă trimite un mesaj (buffer de octeți) prin conexiunea Bluetooth către un alt dispozitiv.

```java
public void write(byte[] buffer) {
    ConnectedThread connThread;
    synchronized (this) {
        if (state != STATE_CONNECTED) {
            return;
        }
        connThread = connectedThread;
    }
    connThread.write(buffer);
}
```
</details>

## Metode Auxiliare
Metodele createAndStartAcceptThread(), createAndStartConnectThread(device), cancelAcceptThread(), cancelConnectThread() și cancelConnectedThread() sunt utilizate pentru a crea, porni și opri firele de execuție.
<details>
<summary>Metode auxiliare</summary>

```java
    private void createAndStartAcceptThread() {
        acceptThread = new AcceptThread();
        acceptThread.start();
    }

    private void createAndStartConnectThread(BluetoothDevice device) {
        connectThread = new ConnectThread(device);
        connectThread.start();
    }

    private void cancelAcceptThread() {
        if (acceptThread != null) {
            acceptThread.cancel();
            acceptThread = null;
        }
    }

    private void cancelConnectThread() {
        if (connectThread != null) {
            connectThread.cancel();
            connectThread = null;
        }
    }

    private void cancelConnectedThread() {
        if (connectedThread != null) {
            connectedThread.cancel();
            connectedThread = null;
        }
    }
```
</details>

Alte metode auxiliare:

<details>
<summary> connectionLost(), connectionFailed() </summary>

```java
    private void connectionLost() {
        Message message = handler.obtainMessage(Constants.MESSAGE_TOAST);
        Bundle bundle = new Bundle();
        bundle.putString(Constants.TOAST, "Connection Lost");
        message.setData(bundle);
        handler.sendMessage(message);

        ChatUtils.this.start();
    }
```

```java
    private synchronized void connectionFailed() {
        Message message = handler.obtainMessage(Constants.MESSAGE_TOAST);
        Bundle bundle = new Bundle();
        bundle.putString(Constants.TOAST, "Cant connect to the device");
        message.setData(bundle);
        handler.sendMessage(message);

        ChatUtils.this.start();
    }
```

```java
     private synchronized void connected(BluetoothSocket socket, BluetoothDevice device) {
        if (connectThread != null) {
            connectThread.cancel();
            connectThread = null;
        }

        if (connectedThread != null) {
            connectedThread.cancel();
            connectedThread = null;
        }

        connectedThread = new ConnectedThread(socket);
        connectedThread.start();

        Message message = handler.obtainMessage(Constants.MESSAGE_DEVICE_NAME);
        Bundle bundle = new Bundle();
        if (ActivityCompat.checkSelfPermission(context, android.Manifest.permission.BLUETOOTH_CONNECT) != PackageManager.PERMISSION_GRANTED) {
            return;
        }
        bundle.putString(Constants.DEVICE_NAME, device.getName());
        message.setData(bundle);
        handler.sendMessage(message);

        setState(STATE_CONNECTED);
    }
```
</details>


## AcceptThread 
AcceptThread așteaptă și acceptă conexiuni de la alte dispozitive Bluetooth.
Constructorul creează un BluetoothServerSocket pentru a asculta conexiunile Bluetooth.

<details>
    <summary> Constructor, run(), cancel() </summary>

```java
public AcceptThread() {
    BluetoothServerSocket tmp = null;
    if (ActivityCompat.checkSelfPermission(context, android.Manifest.permission.BLUETOOTH_CONNECT) != PackageManager.PERMISSION_GRANTED) {
        return;
    }
    try {
        String APP_NAME = "BluetoothChatApp";
        tmp = bluetoothAdapter.listenUsingRfcommWithServiceRecord(APP_NAME, APP_UUID);
    } catch (IOException e) {
        Log.e("Accept->Constructor", e.toString());
    }

    serverSocket = tmp;
}
```

### Metoda Run()
Metoda run() așteaptă conexiuni și acceptă aceste conexiuni. În funcție de starea curentă, va apela metoda connected().

```java
public void run() {
    // ...
    if (socket != null) {
        switch (state) {
            case STATE_LISTEN:
            case STATE_CONNECTING:
                connected(socket, socket.getRemoteDevice());
                break;
            case STATE_NONE:
            case STATE_CONNECTED:
                try {
                    socket.close();
                } catch (IOException e) {
                    Log.e("Accept->CloseSocket", e.toString());
                }
                break;
        }
    }
}
```


### Metoda Cancel()
Această metodă închide serverSocket.

```java
public void cancel() {
    try {
        serverSocket.close();
    } catch (IOException e) {
        Log.e("Accept->CloseServer", e.toString());
    }
}
```

</details>

## Clasa ConnectThread
`ConnectThread` încearcă să stabilească o conexiune cu un dispozitiv Bluetooth specificat.
Constructorul creează un `BluetoothSocket` pentru a se conecta la un dispozitiv Bluetooth specificat.

<details>
    <summary> Constructor, run(), cancel() </summary>

```java
public ConnectThread(BluetoothDevice device) {
    this.device = device;
    if (ActivityCompat.checkSelfPermission(context, android.Manifest.permission.BLUETOOTH_CONNECT) != PackageManager.PERMISSION_GRANTED) {
        return;
    }
    BluetoothSocket tmp = null;
    try {
        tmp = device.createRfcommSocketToServiceRecord(APP_UUID);
    } catch (IOException e) {
        Log.e("Connect->Constructor", e.toString());
    }

    socket = tmp;
}
```
### Metoda run()
Metoda `run()` încearcă să stabilească o conexiune cu dispozitivul Bluetooth și, dacă reușește, apelează metoda `connected().`

```java
public void run() {
    // ...
    try {
        socket.connect();
    } catch (IOException e) {
        // ...
        connectionFailed();
        return;
    }

    synchronized (ChatUtils.this) {
        connectThread = null;
    }

    connected(socket, device);
}
```

### Metoda cancel()
Această metodă închide `socket`.

```java
public void cancel() {
    try {
        socket.close();
    } catch (IOException e) {
        Log.e("Connect->Cancel", e.toString());
    }
}
```

</details>

## ConnectedThread

`ConnectedThread` gestionează comunicarea între dispozitive prin conexiunea Bluetooth stabilită.

Constructorul primește un obiect `BluetoothSocket` și inițializează fluxurile de intrare și ieșire pentru comunicare.

<details>
    <summary> Constructor, run(), write(), cancel() </summary>

```java
public ConnectedThread(BluetoothSocket socket) {
    this.socket = socket;

    InputStream tmpIn = null;
    OutputStream tmpOut = null;

    try {
        tmpIn = socket.getInputStream();
        tmpOut = socket.getOutputStream();
    } catch (IOException e) {
        Log.d("Connected->Constructor", e.toString());
    }

    inputStream = tmpIn;
    outputStream = tmpOut;
}
```

### Run()
Metoda `run()` citește în mod continuu datele primite prin fluxul de intrare și trimite mesajele către handler.

```java
public void run() {
    byte[] buffer = new byte[1024];
    int bytes;

    while (true) {
        try {
            bytes = inputStream.read(buffer);
            handler.obtainMessage(MainActivity.MESSAGE_READ, bytes, -1, buffer).sendToTarget();
        } catch (IOException e) {
            connectionLost();
        }
    }
}
```

### Write()
Metoda write() trimite datele prin fluxul de ieșire și trimite un mesaj către handler.

```java
public void write(byte[] buffer) {
    try {
        outputStream.write(buffer);
        handler.obtainMessage(MainActivity.MESSAGE_WRITE, -1, -1, buffer).sendToTarget();
    } catch (IOException e) {
        Log.d("Connected->Write", e.toString());
    }
}
```

### Cancel()
Metoda cancel() închide conexiunea Bluetooth prin închiderea obiectului BluetoothSocket.

```java
public void cancel() {
    try {
        socket.close();
    } catch (IOException e) {
        Log.d("Connected->Cancel", e.toString());
    }
}
```

</details>








