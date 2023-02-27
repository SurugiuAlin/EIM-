## Mediu de dezvoltare

Pentru dezvoltarea unei aplicații Android sunt necesare:

- [kit-ul de dezvoltare pentru limbajul de programare Java](https://ocw.cs.pub.ro/courses/eim/tutoriale/java)
- [SDK-ul de Android](https://ocw.cs.pub.ro/courses/eim/tutoriale/sdk_android), pentru care se descarcă definițiile corespunzătoare unuia sau mai multor niveluri de API
- un mediu integrat de dezvoltare (IDE)
  - [Android Studio](https://ocw.cs.pub.ro/courses/eim/tutoriale/android_studio)
- un dispozitiv pe care să se ruleze aplicațiile`
  - un emulator
    - [Genymotion](https://ocw.cs.pub.ro/courses/eim/tutoriale/genymotion)
    - [Android Virtual Device](https://ocw.cs.pub.ro/courses/eim/tutoriale/android_virtual_device) (livrat împreună cu SDK-ul de Android)
  - un telefon mobil cu sistemul de operare Android pentru care s-a dezvoltat
  aplicația
  
Pentru a se putea rula o aplicație pe un dispozitiv mobil fizic,
trebuie să se activeze posibilitatea de depanare prin USB, din Settings →
*System* → *Developer Options*. Această opțiune trebuie activată, ca de
altfel și opțiunea *Debugging* → *Android Debugging* (pe unele sisteme poate
apărea ca *USB Debugging*).
  
---
**Note**

În situația în care opțiunea Developer Options nu este disponibilă, aceasta poate fi vizualizată prin intermediul modului Developer, obțiunut prin apăsarea de mai multe ori asupra opțiunii Build Number din secțiunea Settings → System → About Phone.

---

Dacă telefonul nu este recunoscut la conectarea prin USB, trebuie
instalate niște reguli pentru udev, conform instrucțiunilor de pe
[stackexchange](http://unix.stackexchange.com/questions/119128/linux-mint-16-android-device-not-listed-with-lsusb):

```
student@eim-lab:~$ sudo bash 
student@eim-lab:~# lsusb
```

După ce s-a identificat dispozitivul mobil (prin intermediul comenzii
*lsusb*), se precizează o regulă pentru acesta:

```
student@eim-lab:~# cat /etc/udev/rules.d/51-android.rules

<file text /etc/udev/rules.d/51-android.rules> SUBSYSTEM==\"usb\",
ATTR{idVendor}==\"18d1\", ATTR{idProduct}==\"d002\", MODE=\"0660\",
GROUP=\"plugdev\", SYMLINK+=\"android%n\"
```

Se reîncarcă dispozitivele conectate prin USB:

`student@eim-lab:~# /etc/init.d/udev restart`

Fie că ați instalat un emulator, fie un telefon conectat prin cablu USB,
puteti verifica că el este pornit si este vizibil

`/opt/Android/SDK/platform-tools/adb devices`

Dacă dispozitivul este listat, va puteti conecta la prompt:

`/opt/Android/SDK/platform-tools/adb shell`
