
> comanda adb se regăsește acolo unde ați instalat SDK-ul, de exemplu la: ```/opt/Android/SDK/platform-tools/adb``` 

### USB setup 
- Dacă laptopul Linux nu vede telefonul la comanda ```adb devices```

- [udev rules](https://lynxbee.com/solved-no-permissions-user-in-plugdev-group-are-your-udev-rules-wrong/)

### adb over wifi 


#### using CLI 

- [adb over wifi](https://help.famoco.com/developers/dev-env/adb-over-wifi/)

- Connect the device and the computer to the same Wi-Fi network
- Plug the device to the computer with a USB cable to configure the connection
- On the computer command line type:
``` adb tcpip 5555```
- On the computer command line type: 
```adb shell ip addr show wlan0``` and copy the IP address after the "inet" until the "/". You can also go inside the Settings of the device to retrieve the IP address in Settings → About → Status.
- On the computer command line type: 
```adb connect ip-address-of-device:5555```
- You can disconnect the USB cable from the device and check with adb devices that the device is still detected.

#### using Android Studio menus
- Din meniul de device-uri, se selectează "Pair Devices Using WiFi"
