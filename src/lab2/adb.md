## Android Debug Bridge (ADB)

Android Debug Bridge este un utilitar în linie de comandă care permite
comunicarea cu cu un dispozitiv mobil fizic sau cu un emulator, prin
intermediul unui program client-server ce include 3 componente:

-   un client, apelat prin comanda `adb` (alți clienți sunt plugin-ul
    ADT, ADM-ul, Layout Inspector);
-   un server (rulează ca proces de fundal), care gestionează
    comunicarea dintre client și daemonul ce rulează pe emulator sau
    dispozitivul mobil fizic;
-   un daemon, care rulează ca un proces de fundal pentru fiecare
    emulator sau dispozitiv mobil fizic.

ADB este integrat în SDK-ul de Android, regăsindu-se în directorul
`platform-tools`.

> [Aici](https://developer.android.com/tools/adb#connect-to-a-device-over-wi-fi) gasiti instructiunile de conectare prin ADB la dispozitiv peste Wifi.

**Comenzi ADB**

-   pentru a folosi ADB shell, device-ul Android trebuie să fie root-at
    (imaginile genymotion sunt deja).
-   comenzile ADB pot fi rulate din linia de comandă sau din script,
    având următorul
    format:`student@eim-lab:/opt/android-sdk-linux/platform-tools$ adb [-d|-e|-s <serialNumber>] <command>
    `
-   înainte de a utiliza comenzi `adb` este important să fie cunoscut
    identificatorul dispozitivului care este conectat la serverul adb,
    acesta putând fi identificat prin comanda
    `adb devices`:`student@eim-lab:/opt/android-sdk-linux/platform-tools$ adb devices
    List of devices attached 
    emulator-5556           device
    192.168.56.101:5555 device
    0123456789ABCDEF    device
    `
-   conexiunea la emulator se realizează folosind comanda
    `adb -s <serialNumber> shell`

Depanarea este foarte importantă în procesul de realizare a aplicațiilor
pentru dispozitive mobile. Există însă unele diferențe față de depanarea
programelor pentru calculator, întrucât aplicațiile rulează pe un alt
dispozitiv, fiind necesare programe specializate. De asemenea, fiind
vorba de dispozitive mobile, apar și anumite evenimente specifice, cum
ar fi apeluri telefonice, primirea unui mesaj, descărcărea bateriei,
întreruperi ce trebuie tratate intr-un fel sau altul.
