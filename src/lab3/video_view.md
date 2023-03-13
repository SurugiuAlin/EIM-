#### VideoView

Controlul de tip `VideoView` este utilizat pentru redarea de conținut
video, într-unul din formatele `H.263`, `H.264 AVC`, `MPEG-4 SP` sau
`VP8`.

Conținutul acestui control poate fi specificat prin una din
metodele `setVideoPath(String)` sau `setVideoUri(Uri)`, prin care se
indică locația unui fișier stocat pe dispozitiv sau aflat la distanță,
pe un server.

---
**Note**

Pentru a se putea accesa conținutul aflat la distanță, în
fișierul `AndroidManifest.xml` trebuie să se specifice o permisiune
explicită în acest sens:  
`<uses-permission android:name="android.permission.INTERNET" />`\

---

Metodele pe care le pune la dispoziție un astfel de obiect pentru
controlul procesului de redare sunt `start()`, `pause()`, respectiv
`stopPlayback()`. De asemenea, se pot verifica anumiți parametri ai
conținutului prin metodele `isPlaying()`, `getDuration()` și
`getCurrentPosition()`.

De asemenea, pot fi monitorizate o serie de evenimente, cum ar fi
începutul și sfârșitul redării conținutului video, generarea unor
informații cu privire la redarea conținutului, producerea unei erori:

``` java
videoView.setOnPreparedListener(new MediaPlayer.OnPreparedListener() {
  @Override
  public void onPrepared(MediaPlayer mediaPlayer) {
    * TODO Auto-generated method stub
  }
});
videoView.setOnCompletionListener(new MediaPlayer.OnCompletionListener() {
  @Override
  public void onCompletion(MediaPlayer mediaPlayer) {
    * TODO Auto-generated method stub
  }
});
videoView.setOnInfoListener(new MediaPlayer.OnInfoListener() {
  @Override
  public boolean onInfo(MediaPlayer mediaPlayer, int what, int extra) {
    * TODO Auto-generated method stub
    return false;
  }
});
videoView.setOnErrorListener(new MediaPlayer.OnErrorListener() {
  @Override
  public boolean onError(MediaPlayer mediaPlayer, int what, int extra) {
    * TODO Auto-generated method stub
    return false;
  }
});
```

Pentru ca utilizatorul aplicației să poată controla redarea conținutului
video, obiectului de tip `VideoView` trebuie să i se asocieze un obiect
`MediaController` care va pune la dispoziție o serie de controale prin
care se poate realiza pornirea și oprirea procesului.

``` java
MediaController mediaController = new MediaController(this);
mediaController.setAnchorView(videoView);
videoView.setMediaController(mediaController);
```

Controalele obiectului `MediaController` pot fi afișate sau nu prin
metodele `show(int timeout)` respectiv `hide()`.

