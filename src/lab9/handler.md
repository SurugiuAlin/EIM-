# Handler
Pentru comunicarea rapida intre UI si thread-uri de executie putem folosi un `Handler`.
Clasa Handler gestionează transmiterea de mesaje sau execuția unor rutine asociate unor fire de execuție prin intermediul unei cozi de așteptare (de tipul MessageQueue). Un obiect de acest tip este asociat unui singur fir de execuție. Acesta este creat în momentul în care este realizată instanța, cătrea cesta fiind transmise toate mesajele, secvențial. 

Prin intermediul acestui obiect, se permite:

* planificarea mesajelor spre a fi procesate la un moment fix din viitor (metodele de tip send…(): `sendEmptyMessage()`, `sendMessage()`, `sendMessageAtTime()`, `sendMessageDelayed())`;
* încapsularea unei acțiuni care va fi executată pe un alt fir de execuție decât firul de  execuție al interfeței grafice (metodele de tip post…(): `post()`, `postAtTime()`, `postDelayed()`).


De exemplu, daca vrem sa trimitem un mesaj dintr-un `Thread` si sa il afisam ca si un Toast
in interfata grafica vom proceda astfel:

Creeam un handler in care suprascriem metoda `handleMessage` ca sa afiseze un `Toast`
cu mesajul.
```java
handler = new Handler(Looper.getMainLooper()) {
    @Override
    public void handleMessage(Message inputMessage) {
        String messageText = (String) inputMessage.obj;
        Toast.makeText(MainActivity.this, messageText, Toast.LENGTH_SHORT).show();
    }
};
```

In thread, folosind o referinta la acest `handler` o sa chemam functia `obtainMessage()`
urmata de `sendToTarget`.

```java
button.setOnClickListener(new View.OnClickListener() {
    @Override
    public void onClick(View v) {
 
        Runnable runnable = new Runnable() {
            @Override
            public void run() {
            Log.d(TAG, "In a different thread " + Thread.currentThread());
 
            Message message = handler.obtainMessage();
            message.obj = "hello";
            message.sendToTarget();
            }
        };
        Thread thread = new Thread(runnable);
                thread.start();
    }
});
```