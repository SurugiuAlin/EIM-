# Laborator 10. Utilizarea Serviciilor de Localizare

Datele cu privire la localizare îmbunătățesc experiența utilizatorului,
întrucât unele informații furnizate de aplicații pot fi contextualizate
în funcție de regiunea în care acesta se găsește în mod curent. O astfel
de oportunitate poate fi exploatată cu atât mai mult în cadrul
dispozitivelor mobile, care dispun de componente specializate pentru
determinarea automată a poziției geografice curente (senzor pentru GPS,
folosirea informațiilor furnizate de celula de telefonie mobilă).

În cadrul SDK-ului Android, sunt implementate API-uri pentru proiectarea
și dezvoltarea unor aplicații care pun la dispoziția utilizatorilor
informații cu privire la **locația în care se află**, disponibile prin
intermediul unor metode, fără a fi necesară interacțiunea propriu-zisă
cu componentele responsabile cu determinarea acestor date. Totodată,
există posibilitatea de a identifica **punctele de interes** care se
găsesc în proximitatea utilizatorului, la un moment dat.

Există și alte [API-uri](https:*blog.rapidapi.com/top-map-apis/) pentru
localizare, geoconding, hărți, indicații de navigație, fiecare cu
avantajele și dezavantajele asociate. În acest laborator se vor folosi
serviciile Google, care sunt cotate printre cele mai rapide, diverse,
dar și scumpe pentru volum mare de apeluri.

Astfel, funcționalitățile oferite pentru dezvoltatori sunt:

1.  **furnizarea de servicii integrate pentru localizare**, având
    următoarele caracteristici: nivelul de detaliu este determinat în
    funcție de specificațiile utilizatorului (precizie înaltă sau consum
    scăzut de energie), disponibilitate imediată a celei mai recente
    locații disponibile, optimizarea nivelului de utilizare al bateriei,
    luându-se în considerare solicitările existente raportat la senzorii
    care pot fi utilizați, flexibilitatea în gama de servicii oferite
    (utilizarea în interfața grafică a aplicației, cu un nivel de
    detaliu ridicat sau folosirea de către servicii, cu un nivel de
    detaliu scăzut);
2.  **oferirea unei liste cu punctele de interes din proximitate**,
    raportat la un anumit domeniu (locații turistice, tipuri de
    organizații), acestea putând fi marcate cu ajutorul unor controale
    grafice dedicate; pentru fiecare punct de interes pot fi obținute
    informații suplimentare (descrieri, conținut multimedia), acestea
    putând fi furnizate și de utilizator, fiind stocate ulterior într-o
    bază de date Google; se poate determina astfel și locația curentă
    împreună cu alte repere din zonă; denumirile specifice ale locurilor
    respective precum și adresele corespunzătoare pot fi completate
    facil prin indicarea unor sugestii ce conțin variantele disponibile;
3.  transmiterea de notificări legate de **restricția zonală** (*eng.*
    geofencing), prin indicarea unor coordonate aflate în proximitate
    anumitor locații: pot fi gestionate mai multe arealuri geografice de
    acet tip concomitent, fără a avea un impact semnificativ asupra
    consumului de energie (actualizările cu privire la locația curentă
    sunt realizate în funcție de distanța față de zona marcată precum și
    de tipul de activitate - staționar sau în mișcare: mers, alergat, în
    vehicul, cu bicicleta); sunt oferite informații atât cu privire la
    intrarea în arealul geografic cât și cu privire la ieșirea din
    acesta;
4.  determinarea **activității pe care utilizatorul o desfășoară în mod
    curent** (staționar sau în mișcare: mers, alergat, în vehicul, cu
    bicicleta), fără un consum de baterie important (folosind senzori de
    putere mică); o astfel de funcționalitate este foarte utilă în
    contextul integrării cu aplicațiile care necesită actualizări cu
    privire la locația curentă, frecvența cu care sunt solicitate acest
    set de date fiind determinată de tipul de activitate aflat în
    desfășurare.

\<note>Este recomandat ca informațiile legate de localizarea
dispozitivului mobil să se realizeze folosind API-ul pus la dispoziție
de Google Play Services, în detrimentul mecanismelor precedente pentru
localizare (disponibile în pachetul `android.location`).\

---

## Configurare

**1.** În cadrul [Consolei Google
API](https:*console.developers.google.com), se activează API-ul *Google
Maps Android API*, generându-se totodată și o cheie Android prin care
aplicația care rulează pe dispozitivul mobil va putea să acceseze o
astfel de funcționalitate.

---
**Note**

Trebuie să fiți autentificați folosind numele de
utilizator și parola contului Google, altfel va trebui să vă creați un
astfel de cont.\

---

---
**Note**

 În situația în care nu a fost creat un proiect Google
API în prealabil, trebuie realizat acest lucru, prin selectarea opțiunii
*Select a project*.

![](images/createproject01new.png)

Se va afișa o fereastră din care poate fi selectat proiectul dorit
(împărțite în categoriile *Recent*, respectiv *All*). În situația în
care nu există nici un proiect, acesta poate fi creat, prin accesarea
pictogramei corespunzătoare semnului *+*.

![](images/createproject02new.png)

Pentru fiecare proiect trebuie să se precizeze următorii parametri:

-   denumirea;
-   identificatorul pentru proiect (este generat în mod automat, însă
    poate fi configurat suplimentar de către utilizator).

<img src="/eim/laboratoare/laborator10/createproject03new.png" class="align-center" alt="createproject03new.png" />

În situația în care există un singur proiect, acesta va fi selectat în
mod implicit ca proiect curent.

![](images/createproject04new.png)
\

---

-   În secțiunea *Library* → *Google APIs*, în categoria *Google Maps
    APIs*, se accesează opțiunea *Google Maps Android API*, activându-se
    acest serviciu (prin accesarea butonului *Enable*).

![](images/configurare01new.png)

![](images/configurare02new.png)

Acest API nu va putea fi însă utilizat în situația în care nu sunt
create credențialele (o cheie pentru API), necesare pentru a putea
accesa orice serviciu Google.

-   Credențialele pot fi obținute:
    -    prin accesarea butonului *Google Maps Android API* → *Create
        credentials*, care implică următoarele etape:  
        ![](images/configurare03new.png)  
        **1.** indicarea tipului de API folosit (în cazul de față
        *Google Maps Android API*)  
        <img src="/eim/laboratoare/laborator10/configurare04new.png" class="align-center" alt="configurare04new.png" />  
        **2.** generarea (automată) propriu-zisă a cheii, urmată de
        apăsarea butonului \\\\Done\\\\;  
        <img src="/eim/laboratoare/laborator10/configurare05new.png" class="align-center" alt="configurare05new.png" />  
        În secțiunea *Credentials* va putea fi vizualizată cheia creată,
        împreună cu denumirea sa. Pentru cheile care nu sunt
        restricționate, va fi vizibil semnul :!: care indică faptul că
        aceasta poate fi utilizată din orice context, ceea ce poate
        implica o breșă de securitate  
        <img src="/eim/laboratoare/laborator10/configurare06new.png" class="align-center" alt="configurare06new.png" />  
        Prin accesarea cheii respective, aceasta poate fi restricționată
        în sensul în care se precizează **contextul în care este
        folosită cheia** (în cazul de față, aplicații Android - *Android
        apps*), **denumirea pachetului corespunzător aplicației Android
        din care cheia respectivă poate fi folosită** precum și
        **certificatul digital SHA-1 corespunzător mașinii de pe care
        este instalată aplicația Android pe dispozitivul mobil**.  
        Se va indica și comanda care va trebui rulată pentru generarea
        certificatului digital respectiv; folosind utilitarul Java
        `keytool`, se generează semnătura digitală a mașinii de pe care
        se va dezvolta aplicația Android (pentru a putea utiliza acest
        utilitar, calea căte Java trebuie să se găsească în variabila de
        mediu `$PATH`, respectiv `%PATH`).  
        Linux
        `student@eg-106:~$ export PATH=$PATH:/usr/local/java/jdk1.8.0_131/bin
        student@eg-106:~$ keytool -list -v -keystore ~/.android/debug.keystore -alias androiddebugkey -storepass android -keypass android
        `  
        Windows
        `C:\Users\Student> set PATH=%PATH%;C:\Program Files\Java\jdk_1.8.0_131\bin
        C:\Users\Student> keytool -list -v -keystore "%USERPROFILE%\.android\debug.keystore" -alias androiddebugkey -storepass android -keypass android
        `  
        Vor fi furnizate mai multe tipuri de amprente digitale, pentru
        cheia publică de tip Android fiind necesară cea de tip SHA-1
        `Alias name: androiddebugkey
        Creation date: Mar 5, 2015
        Entry type: PrivateKeyEntry
        Certificate chain length: 1
        Certificate[1]:
        Owner: CN=Android Debug, O=Android, C=US
        Issuer: CN=Android Debug, O=Android, C=US
        Serial number: 4a38a96a
        Valid from: Thu Mar 05 13:17:44 EET 2015 until: Sat Feb 25 13:17:44 EET 2045
        Certificate fingerprints:
                 MD5:  FC:1F:95:45:78:ED:50:C6:EE:8E:02:0A:3D:A5:80:D3
                 SHA1: C7:02:98:BB:AD:1C:6E:D1:3A:35:50:8B:88:78:B6:D3:B7:9F:66:C0
                 SHA256: B3:D9:98:33:92:71:2D:CE:65:19:89:73:2A:64:3C:97:B9:37:A1:93:8C:
        50:4F:E1:13:C4:21:C7:08:94:AC:A5
                 Signature algorithm name: SHA256withRSA
                 Version: 3

        Extensions:

        #1: ObjectId: 2.5.29.14 Criticality=false
        SubjectKeyIdentifier [
        KeyIdentifier [
        0000: 99 78 63 24 A0 64 DF A8   67 45 8E 82 C6 8E 53 D1  .xc$.d..gE....S.
        0010: B8 C1 89 75                                        ...u
        ]
        ]
        `  
        se accesează butonul *Add package name and fingerprint* pentru a
        se specifica denumirea pachetului corespunzător aplicației
        Android care va accesa API-ul respectiv și certificatul SHA-1  
        <img src="/eim/laboratoare/laborator10/configurare07new.png" class="align-center" alt="configurare07new.png" />  
        În secțiunea *Credentials* pot fi vizualizate cheile pentru API
        generate anterior  
        <img src="/eim/laboratoare/laborator10/configurare08new.png" class="align-center" alt="configurare08new.png" />
    -   în secțiunea *Credentials*, prin accesarea opțiunii *Create
        credentials* din care este selectat tipul de cheie necesar (în
        cazul de față *API key*); dacă nu se cunoaște tipul de cheie
        necesar, se poate selecta valoarea *Help me choose*  
        <img src="/eim/laboratoare/laborator10/configurare09new.png" class="align-center" alt="configurare09new.png" />  
        cheia respectivă va fi generată în mod automat, existând
        posibilitatea ca aceasta să fie restricționată, pentru a nu fi
        accesată din orice context  
        <img src="/eim/laboratoare/laborator10/configurare10new.png" class="align-center" alt="configurare10new.png" />

**2.** Pe dispozitivul mobil (fizic sau virtual) pe care se va rula
aplicația care accesează serviciul de localizare, trebuie să se găsească
cea mai recentă versiune de *Google Play Services*, asociindu-se
totodată contul de utilizator Google pentru care s-a generat cheia
publică.

**3.** Se instalează SDK-ul *Google Play Services*, necesar accesării
serviciului de localizare prin intermediul unei aplicații Android.

-   Linux `student@eg-106:~$ cd /opt/android-sdk-linux/tools
    student@eg-106:/opt/android-sdk-linux/tools$ sudo ./android
    `
-   Windows - se deschide un terminal cu drepturi de administrator
    `C:\Users\Student> cd "..\..\Program Files (x86)\Android\android-sdk\tools"
    C:\Program Files (x86)\Android\android-sdk\tools>android.bat
    `

![](images/configurare11new.png)

Astfel, se instalează următoarele pachete:

-   din secțiunea *Android 4.1.2 (API 16)*, pachetul *Google APIs*;
-   din secțiunea *Extras*, pachetul *Google Play Services*.

Posibilitatea de instalare a acestor pachete există și din mediul
integrat de dezvoltare Android Studio, prin accesarea opțiunii *Tools* →
*Android* → *SDK Manager*, secțiunea *SDK Tools*.

![](images/configurare12newandroidstudio.png)

\<hidden> Biblioteca pentru accesarea funcționalității oferite de
serviciul de localizare se găsește la
`<android-sdk>/extras/google/google_play_services/libproject/google-play-services_lib`.

În mediul integrat de dezvoltare Eclipse, se realizează o referință
către biblioteca *Google Play Services*, astfel descărcată.

-   se accesează *File* → *Import* → *Android* → *Existing Android Code
    Into Workspace*  
      
    ![](images/configurare13.png)
-   se indică locația unde se găsește instalată biblioteca *Google Play
    Services*, creându-se o copie a acestuia în spațiul de lucru (se
    bifează opțiunea *Copy projects into workspace*)  
      
    ![](images/configurare14.png)

\</hidden>

**4.** În mediul integrat de dezvoltare Android Studio, se creează un
proiect corespunzător unei aplicații Android, având următoarele
proprietăți:

-   denumirea pachetului care identifică aplicația Android în mod unic
    trebuie să fie aceeași cu cea precizată în momentul în care a fost
    generată cheia publică;

<!-- -->

-   în fișierul `build.gradle` să se specifice dependința către
    biblioteca Google Play Services
    (`com.google.android.gms:play-services`), în secțiunea
    `dependencies`: `...
    dependencies {
      ...
      compile 'com.google.android.gms:play-services:10.2.4'
    }
    `

\<hidden>

-   pentru **Eclipse**, trebuie să existe o referință către biblioteca
    *Google Play Services* (click dreapta pe denumirea proiectului în
    *Package Explorer* → *Properties*), se accesează opțiunea *Android*
    și se specifică referința către aceasta respectivă în secțiunea
    *Library* (accesând butonul *Add*)  
      
    ![](images/configurare15.png)

\</hidden>

-   în fișierul `AndroidManifest.xml`
    -   se indică permisiunile necesare: `<uses-permission
          android:name="android.permission.ACCESS_COARSE_LOCATION" />
        <uses-permission
          android:name="android.permission.ACCESS_FINE_LOCATION" />    
        <uses-permission
          android:name="android.permission.ACCESS_NETWORK_STATE" />
        <uses-permission
          android:name="android.permission.INTERNET" />
        <uses-permission
          android:name="com.google.android.providers.gsf.permission.READ_GSERVICES" />
        <uses-permission
          android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
        `
        -   `android.permission.ACCESS_COARSE_LOCATION` - obține locația
            utilizatorului folosind informațiile preluate prin rețele
            fără fir și datele corespunzătoare celulei în care se
            găsește dispozitivul mobil;
        -   `android.permission.ACCESS_FINE_LOCATION` - procură locația
            utilizatorului prin intermediul coordonatelor obținute de la
            sistemul de poziționare (GPS - *eng.* Global Positioning
            System);
        -   `android.permission.ACCESS_NETWORK_STATE` - verifică starea
            conectivității în rețea, astfel încât să se determine dacă
            este posibil ca datele să fie descărcate sau nu;
        -   `android.permission.INTERNET` - determină starea
            conectivității la Internet;
        -   `com.google.android.providers.gsf.permission.READ_GSERVICES` -
            preia informațiile puse la dispoziție prin intermediul
            Google Play Services;
        -   `android.permission.WRITE_EXTERNAL_STORAGE` - utilizează un
            spațiu de stocare pentru informațiile legate de hărți;
    -   pentru redarea hărților, precum și pentru operațiile de tip
        zoom, este necesară folosirea bibliotecii OpenGL `<uses-feature
          android:glEsVersion="0x00020000"
          android:required="true" /> 
        `
    -   în secțiunea `<application> ... </application>` se indică:
        -   cheia publică utilizată pentru accesarea funcționalității
            legată de serviciile de localizare `<metadata
              android:name="com.google.android.maps.v2.API_KEY"
              android:value="AIzaSyARiJhQ-Lj6HnzQwq7MqAvjWQtNkjVcprs" />
            `
        -   versiunea folosită pentru biblioteca Google Play Services
            (preluată din cadrul proiectului referit) `<metadata
              android:name="com.google.android.gms.version"
              android:value="@integer/google_play_services_version" />
            `
    -   pentru a se asigura faptul că funcționalitatea nu va putea fi
        accesată decât prin intermediul aplicației Android, se va defini
        o permisiune, definindu-se o protecție la nivel de
        semnătură:`<permission
          android:name="ro.pub.cs.systems.eim.lab10.googlemaps.permission.MAPS_RECEIVE"
          android:protectionLevel="signature" />
        <uses-permission
          android:name="ro.pub.cs.systems.eim.lab10.googlemaps.permission.MAPS_RECEIVE" />
        `

<!-- -->

-   se precizează regulile pentru obfuscatorul Proguard (în fișierul
    `proguard-rules.pro` din directorul *app*), astfel încât acesta să
    nu elimine clasele necesare:  
    `-keep class * extends java.util.ListResourceBundle {
      protected Object[][] getContents();
    }
    -keep public class com.google.android.gms.common.internal.safeparcel.SafeParcelable {
      public static final *** NULL;
    }
    -keepnames @com.google.android.gms.common.annotation.KeepName class *
    -keepclassmembernames class * {
      @com.google.android.gms.common.annotation.KeepName *;
    }
    -keepnames class * implements android.os.Parcelable {
      public static final ** CREATOR;
    }
    `

\<hidden> ---
**Note**

Pentru rularea proiectului Eclipse (construirea
pachetului `.apk`) este necesară mai multă memorie ce trebuie alocată
mașinii virtuale Java (datorate referinței către biblioteca Google Play
Services), aceasta realizându-se prin intermediul valorilor furnizate în
cadrul fișierului de configurare `eclipse.ini`:  
`--launcher.XXMaxPermSize
1024M
--launcher.XXMaxPermSize
1024m
--launcher.appendVmargs
-vmargs
-Dosgi.requiredJavaVersion=1.7
-Xms1024m
-Xmx1024m
` \

--- \</hidden>

### Dispozitiv Fizic

Pentru accesarea funcționalităților legate de locație pe dispozitivul
fizic este necesar să se activeze opțiunea *Location* din secțiunea de
configurări (*Settings* → *Personal*).

![](images/physical_device_01.png)

Valoarea configurației *Location* trebuie să aibă valoarea *On*, pentru
ca serviciile de localizare să poată fi utilizate. De asemenea, sunt
indicate aplicațiile Android care au folosit serviciile de localizare.

![](images/physical_device_02.png)

Se poate controla acuratețea informațiilor furnizate, raportat la
consumul de energie, prin intermediul opțiunilor disponibile în
secțiunea *Location Mode* din secțiunea de configurări (*Settings* →
*Personal* → *Location* → *Mode*).

-   *High accuracy* - locația este determinată folosind toate resursele
    disponibile (sistemul global de poziționare GPS, rețelele mobile și
    fără fir);
-   *Battery saving* - locația este determinată folosind doar
    informațiile furnizate de rețelele mobile și fără fir;
-   *Device only* - locația este determinată folosind doar informațiile
    furnizate de sistemul global de poziționare GPS.

![](images/physical_device_03.png)

---
**Note**

Se recomandă ca determinarea locației să se realizeze
folosind toate resursele disponibile la un moment dat de timp pentru o
precizie cât mai mare (cu un consum de energie corespunzător).\

---

### Dispozitiv Virtual

#### Genymotion

Pentru accesarea funcționalităților legate de locație pe dispozitivul
virtual Genymotion este necesar să se activeze serviciul GPS, accesibil
din meniul lateral sau folosind combinația de taste Ctrl + 2 (se
selectează valoarea *On*).

![](images/genymotion_gps_01.png)

Alte informații care pot fi configurate sunt:

-   latitudinea - exprimată în grade;
-   longitudinea - exprimată în grade;
-   altitudinea - exprimată în metri;
-   acuratețea (nivelul de precizie) - exprimat în număr de metri cu
    care să se aproximeze locația exactă;
-   direcția - exprimată în grade.

![](images/genymotion_gps_02.png)

De asemenea, este implementată și funcționalitatea prin intermediul
căreia poate fi vizualizată poziția precizată în cadrul unei hărți
Google.

![](images/genymotion_gps_03.png)

#### AVD

Pentru accesarea funcționalităților legate de locație pe dispozitivul
virtual AVD este necesar ca în secțiunea de configurări corespunzătoare
(*Settings* → *Location access*) să se specifice următorii parametri:

-   *Access to my location*: *On* - permite aplicațiilor Android să
    acceseze locația curentă, pe baza informațiilor furnizate din
    sursele disponibile;
-   *GPS Sattelites*: activat - se utilizează sistemul de poziționare
    globală GPS pentru determinarea locației curente;
-   *Wi-Fi & mobile network location*: activat - se utilizează o
    estimare pentru locația curentă pe baza serviciilor oferite de
    Google; totodată, vor fi transmise informații anonime în acest sens.

![](images/avd_configuration.png)

Controlul poziției curente poate fi realizat prin intermediul
perspectivei *Android Debug Monitor* din Android Studio, unde, în
secțiunea *Emulator Control* → *Location Control* se stabilesc valorile
pentru latitudine și longitudine (în panoul *Manual*, în format decimal
sau sexagesimal), după care se apasă butonul *Send*. Informații cu
privire la locațiile disponibile pot fi precizate și sub forma unor
fișiere gpx sau kml, care pot fi încărcate.

<img src="/eim/laboratoare/laborator10/avd_emulator_control_new.png" class="align-center" alt="avd_emulator_control_new.png" />

## Gestiunea unei Hărți Google

Harta Google este implementată în SDK-ul Android:

-   prin intermediul unei componente grafice de tipul
    [MapView](https:*developer.android.com/reference/com/google/android/gms/maps/MapView.html),
    în acest caz fiind necesar ca metodele care controlează ciclul de
    viață al aplicației Android să propage evenimentele corespunzătoare
    și către acest element;
-   în cadrul unui fragment, de tipul
    [MapFragment](http:*developer.android.com/reference/com/google/android/gms/maps/MapFragment.html),
    acesta tratând și evenimentele corespunzătoare ciclului de viață al
    aplicației Android.

---
**Note**

Obiectele `MapView` și`MapFragment` sunt disponibile începând
cu nivelul de API 12, asigurarea compatibilității cu versiunile
anterioare fiind realizată prin intermediul bibliotecilor de
suport.\

---

Astfel, integrarea unei hărți Google se poate implementa prin
specificarea resursei aferente în fișierul XML care descrie interfața
grafică.

``` xml
<fragment
  android:id="@+id/google_map"
  android:layout_width="match_parent"
  android:layout_height="match_parent"
  class="com.google.android.gms.maps.MapFragment" />
```

Pe baza controalelor grafice `MapView` sau `MapFragment`, se poate
obține o instanță a unui obiect
[GoogleMap](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html),
prin intermediul căruia sunt invocate toate funcționalitățile pentru
operații legate de localizarea pe hartă.

De regulă, inițializarea este realizată pe una dintre metodele
`onStart()` sau `onResume()`, după ce în prealabil au fost încărcate
toate controalele grafice pentru interacțiunea cu utilizatorul.

---
**Note**

Se recomandă să se folosească metoda asincronă
[getMapAsync(OnMapReadyCallback)](http:*developer.android.com/reference/com/google/android/gms/maps/MapFragment.html#getMapAsync%28com.google.android.gms.maps.OnMapReadyCallback%29)
care garantează faptul că obiectul furnizat este nenul. Metoda
`onMapReady()` a clasei ascultător nu va fi apelată în situația în care
serviciul Google Play Services nu este disponibil pe dispozitivul mobil
sau obiectul este distrus imediat după ce a fost creat.\

---

---
**Note**

Orice operație care implică un obiect de tipul
`GoogleMap` trebuie realizată pe firul de execuție al interfeței grafice
(principal), în caz contrar generându-se o excepție.\

---

``` java
GoogleMap googleMap = null;

* ...

if (googleMap == null) {
  ((MapFragment)getFragmentManager().findFragmentById(R.id.google_map)).getMapAsync(new OnMapReadyCallback() {
    @Override
    public void onMapReady(GoogleMap readyGoogleMap) {
      googleMap = readyGoogleMap;
    }
  });
}
```

Funcționalitățile pe care le pune la dispoziție un obiect de tipul
`GoogleMap` sunt:

**1.** gestiunea reperelor de pe harta Google, prin intermediul
elementelor
[MarkerOptions](http:*developer.android.com/reference/com/google/android/gms/maps/model/MarkerOptions.html),
pentru care se pot preciza următoarele informații:

-   coordonatele GPS, sub forma unui obiect
    [LatLng](http:*developer.android.com/reference/com/google/android/gms/maps/model/LatLng.html)
    (care încapsulează informații precum latitudinea și longitudinea, de
    tip `double`), prin metoda
    [position(LatLng)](http:*developer.android.com/reference/com/google/android/gms/maps/model/MarkerOptions.html#position%28com.google.android.gms.maps.model.LatLng%29)
    `marker.position(new LatLng(
      Double.parseDouble(latitudeContent), 
      Double.parseDouble(longitudeContent)
      )
    );
    `
-   titlul, prin metoda
    [title(String)](http:*developer.android.com/reference/com/google/android/gms/maps/model/MarkerOptions.html#title%28java.lang.String%29);
    `marker.title(nameContent);
    `
-   pictograma, prin metoda
    [icon(BitmapDescriptor)](http:*developer.android.com/reference/com/google/android/gms/maps/model/MarkerOptions.html#icon%28com.google.android.gms.maps.model.BitmapDescriptor%29),
    putând fi obținută prin intermediul clasei
    [BitmapDescriptorFactory](https:*developer.android.com/reference/com/google/android/gms/maps/model/BitmapDescriptorFactory.html):
    -   în formatul standard, disponibil în mai multe culori (metoda
        [defaultMarker(float)](https:*developer.android.com/reference/com/google/android/gms/maps/model/BitmapDescriptorFactory.html#defaultMarker%28float%29));
        `marker.icon(BitmapDescriptorFactory.defaultMarker(Utilities.getDefaultMarker(markerTypeSpinner.getSelectedItemPosition())));
        `
    -   într-un format definit de utilizator, în funcție de resursele
        disponibile în cadrul aplicației Android:
        -   [fromAsset(String)](https:*developer.android.com/reference/com/google/android/gms/maps/model/BitmapDescriptorFactory.html#fromAsset%28java.lang.String%29) -
            în directorul `assets`, ce conține resurse externe;
        -   [fromBitmap(Bitmap)](https:*developer.android.com/reference/com/google/android/gms/maps/model/BitmapDescriptorFactory.html#fromBitmap%28android.graphics.Bitmap%29) -
            dintr-o imagine;
        -   [fromFile(String)](https:*developer.android.com/reference/com/google/android/gms/maps/model/BitmapDescriptorFactory.html#fromFile%28java.lang.String%29) -
            dintr-un fișier aflat la o cale relativă;
        -   [fromPath(String)](https:*developer.android.com/reference/com/google/android/gms/maps/model/BitmapDescriptorFactory.html#fromPath%28java.lang.String%29) -
            dintr-un fișier aflat la o cale absolută;
        -   [fromResource(int)](https:*developer.android.com/reference/com/google/android/gms/maps/model/BitmapDescriptorFactory.html#fromResource%28int%29) -
            în directorul `drawable`, ce conține resurse care pot fi
            desenate.
-   descrierea, prin metoda
    [snippet(String)](http:*developer.android.com/reference/com/google/android/gms/maps/model/MarkerOptions.html#snippet%28java.lang.String%29);
    `marker.snippet(descriptionContent);
    `
-   vizibilitatea, prin metoda
    [visible(boolean)](http:*developer.android.com/reference/com/google/android/gms/maps/model/MarkerOptions.html#visible%28boolean%29).
    `marker.visible(true);
    `

Un astfel de obiect este atașat unei hărți Google prin intermediul
metodei
[addMarker(MarkerOptions)](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html#addMarker%28com.google.android.gms.maps.model.MarkerOptions%29).
`googleMap.addMarker(marker);
`

Alte elemente grafice care pot fi vizualizate sunt:

-   [CircleOptions](https:*developer.android.com/reference/com/google/android/gms/maps/model/CircleOptions.html) -
    formă geometrică de tip cerc;
-   [GroundOverlayOptions](https:*developer.android.com/reference/com/google/android/gms/maps/model/GroundOverlayOptions.html) -
    suprapunerea unei alte imagini;
-   [PolygonOptions](https:*developer.android.com/reference/com/google/android/gms/maps/model/PolygonOptions.html) -
    formă geometrică de tip poligon;
-   [PolylineOptions](https:*developer.android.com/reference/com/google/android/gms/maps/model/PolylineOptions.html) -
    formă geometrică de tip polinie;
-   [TileOverlay](https:*developer.android.com/reference/com/google/android/gms/maps/model/TileOverlayOptions.html) -
    suprapunerea unei alte imagini, pentru o anumită porțiune.

Toate aceste controale pot fi înlăturate în momentul în care este
folosită metoda
[clear()](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html#clear%28%29).

**2.** poziționarea la anumite coordonate GPS (latitudine, longitudine)
este realizată prin actualizarea locației la care se găsește camera prin
care este vizualizată harta Google, funcționalitate implementată de
clasa
[CameraUpdate](https:*developer.android.com/reference/com/google/android/gms/maps/CameraUpdate.html);
un astfel de obiect este obținut de regulă prin metoda statică
[newCameraPosition(CameraPosition)](https:*developer.android.com/reference/com/google/android/gms/maps/CameraUpdateFactory.html#newCameraPosition%28com.google.android.gms.maps.model.CameraPosition%29)
din clasa fabrică `CameraUpdateFactory`, prin care pot fi controlate și
alte proprietăți (nivelul de detaliere, vizualizarea unui anumit areal
geografic); metoda
[animateCamera(CameraUpdate)](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html#animateCamera%28com.google.android.gms.maps.CameraUpdate%29)
realizează transferul dintre coordonatele vechi și coordonatele noi prin
intermediul unei animații.

``` java
CameraPosition cameraPosition = new CameraPosition.Builder().target(new LatLng(latitude, longitude))
  .build();
googleMap.animateCamera(CameraUpdateFactory.newCameraPosition(cameraPosition)); 
```

Metoda `animateCamera()` este supraîncărcată, astfel încât să se poată
preciza:

-   durata propriu-zisă a animației (exprimată în milisecunde);
-   un obiect ascultător (de tipul
    [GoogleMap.CancelableCallback](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.CancelableCallback.html))
    care indică momentul în care animația a fost terminată
    (`onFinish()`) sau a fost întreruptă (`onCancel()`).

În situația în care este în desfășurare o animație, aceasta poate fi
oprită printr-un apel al metodei
[stopAnimation()](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html#stopAnimation%28%29).

**3.** marcarea locației curente este realizată prin intermediul metodei
[setMyLocationEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html#setMyLocationEnabled%28boolean%29);
de asemenea, este disponibil un control prin intermediul căruia
utilizatorul poate activa sau dezactiva această funcționalitate;

**4.** vizualizarea unor informații suplimentare:

-   [setBuildingsEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html#setBuildingsEnabled%28boolean%29) -
    vizualizarea exterioarelor de clădiri în format 3D;
-   [setContentDescription(String)](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html#setContentDescription%28java.lang.String%29) -
    descriere;
-   [setIndoorEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html#setIndoorEnabled%28boolean%29) -
    vizualizarea configurațiilor interioarelor de clădiri;
-   [setTrafficEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html#setTrafficEnabled%28boolean%29) -
    traficul la momentul de timp curent;

Tipurile de hărți Google implementate sunt:

-   `GoogleMap.MAP_TYPE_NORMAL` - harta politică;
-   `GoogleMap.MAP_TYPE_TERRAIN` - harta fizică (nu include și drumuri);
-   `GoogleMap.MAP_TYPE_SATELLITE` - vedere din satelit;
-   `GoogleMap.MAP_TYPE_HYBRID` - combinație hibridă.

Specificarea unui tip de hartă se realizează prin intermediul metodei
[setMapType()](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html#setMapType%28int%29).

Gestiunea unei hărți Google sub formă de imagine este realizată prin
intermediul metodei
[snapshot(GoogleMap.SnapshotReadyCallback](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html#snapshot%28com.google.android.gms.maps.GoogleMap.SnapshotReadyCallback%29),
al cărui obiect ascultător furnizează resursa grafică (în format
`Bitmap`) în momentul în care este disponibilă (se apelează automat
metoda `onSnapshotReady(Bitmap)`.

Funcționalitatea pe care o oferă harta Google utilizatorului poate fi
controlată și prin intermediul obiectului asociat de tip
[UiSettings](https:*developer.android.com/reference/com/google/android/gms/maps/UiSettings.html),
obținut prin apelul metodei
[getUiSettings()](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.html#getUiSettings%28%29):

-   [setAllGesturesEnables(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/UiSettings.html#setAllGesturesEnabled%28boolean%29) -
    permite sau nu toate tipurile de operații care pot fi realizate prin
    intermediul hărții Google;
-   [setCompassEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/UiSettings.html#setCompassEnabled%28boolean%29) -
    activează sau dezactivează busola;
-   [setIndoorLevelPickerEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/UiSettings.html#setIndoorLevelPickerEnabled%28boolean%29) -
    stabilește permisiunile de selectare a unui nivel în cazul unor
    hărți de interior;
-   [setMapToolbarEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/UiSettings.html#setMapToolbarEnabled%28boolean%29) -
    indică configurările de vizualizare pentru bara de unelte;
-   [setMyLocationButtonEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/UiSettings.html#setMyLocationButtonEnabled%28boolean%29) -
    referă vizualizarea controlului grafic pentru centrarea hărții
    Google în funcție de locația curentă;
-   [setRotateGesturesEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/UiSettings.html#setRotateGesturesEnabled%28boolean%29) -
    precizează dreptul de utilizare al gesturilor legate de rotirea
    camerei pentru perspectiva de vizualizare;
-   [setScrollGesturesEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/UiSettings.html#setScrollGesturesEnabled%28boolean%29) -
    determină posibilitatea de folosire a gesturilor pentru derulare,
    folosind un deget;
-   [setTiltGesturesEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/UiSettings.html#setTiltGesturesEnabled%28boolean%29) -
    instaurează politica referitoare la gesturile de derulare, folosind
    două degete;
-   [setZoomControlsEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/UiSettings.html#setZoomControlsEnabled%28boolean%29) -
    desemnează vizualizarea sau nu a unor controale grafice pentru
    gradul de detaliere a hărții Google;
-   [setZoomGesturesEnabled(boolean)](https:*developer.android.com/reference/com/google/android/gms/maps/UiSettings.html#setZoomGesturesEnabled%28boolean%29) -
    controlează utilizarea gesturilor pentru vizualizarea hărții Google
    folosind un anumit grad de detaliere.

Pentru interacțiunea cu utilizatorul au fost definite mai multe clase
ascultător, ale căror metode semnalează declanșarea unor evenimente
specifice:

-   [GoogleMap.OnCameraChangeListener](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.OnCameraChangeListener.html) -
    modificarea poziției camerei prin care este vizualizată harta
    Google;
-   [GoogleMap.OnIndoorStateChangeListener](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.OnIndoorStateChangeListener.html) -
    schimbarea stării legate de vizualizarea la nivel de interior al
    clădirii (clădirea curentă, etajul la care se găsește utilizatorul);
-   [GoogleMap.OnInfoWindowClickListener](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.OnInfoWindowClickListener.html) -
    evenimente legate de fereastra ce conține informații suplimentare cu
    privire la o locație;
-   [GoogleMap.OnMapClickListener](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.OnMapClickListener.html) -
    acțiune de tipul apăsare scurtă a unei poziții de pe harta Google;
-   [GoogleMap.OnMapLoadedCallback](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.OnMapLoadedCallback.html) -
    marcarea momentului în care sunt vizibile toate componentele
    necesare la un moment dat;
-   [GoogleMap.OnMapLongClickListener](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.OnMapLongClickListener.html) -
    acțiune de tipul apăsare lungă a unei poziții de pe harta Google;
-   [GoogleMap.OnMarkerClickListener](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.OnMarkerClickListener.html) -
    descrie interacțiunea de tip apăsare a unui reper de pe harta
    Google;
-   [GoogleMap.OnMarkerDragListener](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.OnMarkerDragListener.html) -
    descrie interacțiunea de tip mutare a unui reper de pe harta Google;
-   [GoogleMap.OnMyLocationButtonClickListener](https:*developer.android.com/reference/com/google/android/gms/maps/GoogleMap.OnMyLocationButtonClickListener.html) -
    accesarea butonului pentru centrarea hărții în funcție de locația
    curentă.

## Gestiunea Locației Curente printr-un Client Google API

API-ul Android pune la dispoziția utilizatorilor un [furnizor integrat
de servicii de
localizare](http:*developer.android.com/reference/com/google/android/gms/location/FusedLocationProviderApi.html),
prin care aceștia pot specifica anumiți parametrii de configurare, cum
ar fi nivelul de precizie și gradul de utilizare al bateriei.

Funcționalitatea legată de gestiunea locației curente (ca de altfel
toate funcționalitățile legate de biblioteca Google Play Services) este
disponibilă prin intermediul unui obiect de tip
[GoogleApiClient](http:*developer.android.com/reference/com/google/android/gms/common/api/GoogleApiClient.html),
a cărui instanță este obținută de regulă pe metoda `onCreate()` a
aplicației Android, eliberarea resurselor corespunzătoare acesteia fiind
făcută pe metoda `onDestroy()`.

![](images/clientul_google_api.png)

``` java
@Override
protected void onCreate(Bundle savedInstanceState) {
  super.onCreate(savedInstanceState);

  * ...

  googleApiClient = new GoogleApiClient.Builder(this)
    .addConnectionCallbacks(this)
    .addOnConnectionFailedListener(this)
    .addApi(LocationServices.API)
    .build();
}

@Override
protected void onDestroy() {

  * ...

  googleApiClient = null;
  super.onDestroy();
}
```

Pentru clientul Google API, s-a indicat funcționalitatea pentru care va
fi accesat (`LocationServices.API`) prin intermediul metodei `addApi()`,
precum și clasele ascultător pentru evenimentele care pot fi generate
legat de acesta (metodele corespunzătoare fiind asincrone):

-   [GoogleApiClient.ConnectionCallbacks](http:*developer.android.com/reference/com/google/android/gms/common/api/GoogleApiClient.ConnectionCallbacks.html)
    gestionează operațiile de tip conectare / deconectare la serviciu,
    metodele implementate fiind:
    -   `onConnected(Bundle)` - apelată în momentul în care clientul
        Google API s-a conectat cu succes la funcționalitatea dorită;
    -   `onConnectionSuspended(int)` - apelată în momentul în care
        clientul Google API este deconectat (temporar) de la
        funcționalitatea solicitată, indicându-se și motivul care a
        generat un astfel de comportament:
        -   `CAUSE_NETWORK_LOST` - deconectare de la Internet;
        -   `CAUSE_SERVICE_DISCONNECTED` - oprirea serviciului
            corespunzător.
-   [GoogleApiClient.OnConnectionFailedListener](http:*developer.android.com/reference/com/google/android/gms/common/api/GoogleApiClient.OnConnectionFailedListener.html)
    controlează situațiile în care nu este posibilă realizarea unei
    legături, metoda aferentă, `onConnectionFailed(ConnectionResult)`,
    specificând rezultatul ce conține codul de eroare.

---
**Note**

Este recomandat ca metodele ascultător care controlează
starea conexiunii clientului Google API la serviciul de localizare să
fie implementate în aceeași clasă cu activitatea principală, aceasta
implementând interfețele necesare.\

---

Operațiile de conectare / deconectare a clientului Google API la
serviciu trebuie realizate în contextul metodelor care controlează
ciclul de viață al aplicației Android, astfel:

-   metoda `connect()` se apelează în cadrul metodei `onStart()`;
-   metoda `disconnect()` se apelează în cadrul metodei `onStop()`.

``` java
@Override
protected void onStart() {
  super.onStart();
  googleApiClient.connect();
  
  * ...

}

@Override
protected void onStop() {

  * ...

  if (googleApiClient != null && googleApiClient.isConnected()) {
    googleApiClient.disconnect();
  }
  super.onStop();
}
```

Momentul în care sunt disponibile informațiile cu privire la **cea mai
recentă locație a dispozitivului mobil** este determinat de conectarea
cu succes a clientului Google API, motiv pentru care se obișnuiește ca
aceste date să fie interogate pe metoda `onConnected(Bundle)` a
intefeței `GoogleApiClient.ConnectionCallbacks`, apelată în mod automat
la producerea evenimentului respectiv. În acest sens, se apelează metoda
[getLastLocation(GoogleApiClient)](http:*developer.android.com/reference/com/google/android/gms/location/FusedLocationProviderApi.html#getLastLocation%28com.google.android.gms.common.api.GoogleApiClient%29)
din clasa
[FusedLocationProviderApi](http:*developer.android.com/reference/com/google/android/gms/location/FusedLocationProviderApi.html).

\<note>Se furnizează o locație al cărui grad de precizie este determinat
în funcție de permisiunile pe care le deține aplicația Android.\

---

``` java
@Override
public void onConnected(Bundle connectionHint) {
  Log.i(Constants.TAG, "onConnected() callback method has been invoked");
  lastLocation = LocationServices.FusedLocationApi.getLastLocation(googleApiClient);
  
  * ...

}
```

Informațiile referitoare la locația curentă sunt descrise sub forma unui
obiect
[Location](http:*developer.android.com/reference/android/location/Location.html),
care conține mai multe informații, precum:

-   acuratețea (exprimată în metri);
-   altitudinea (exprimată în metri, având drept referință elipsoidul
    WGS 84);
-   palierul (exprimat în grade);
-   latitudine și longitudine (exprimată în grade);
-   furnizor;
-   viteză (exprimată în m/s);
-   momentul de timp (exprimat în milisecunde, raportat la 1 ianuarie
    1970).

De asemenea, pentru acest tip de obiect pot fi asociate informații
suplimentare, sub forma unui `Bundle`, în câmpul `extras`.

Totodată, pot fi obținute **actualizări periodice** cu privire la
locația curentă, pe baza furnizorilor disponibili (transfer de date în
rețeaua GSM / fără fir, sistemul global de poziționare GPS)
funcționalitate utilă în momentul în care se dorește să se identifice
activitatea pe care o desfășoară utilizatorul pentru a contextualiza
conținutul oferit în funcție de aceasta.

Acuratețea datelor generate poate fi controlată și prin intermediul
configurațiilor conținute în solicitarea corespunzătoare, exprimată prin
intermediul unui obiect de tip
[LocationRequest](http:*developer.android.com/reference/com/google/android/gms/location/LocationRequest.html):

-   [setExpiration(long)](http:*developer.android.com/reference/com/google/android/gms/location/LocationRequest.html#setExpirationDuration%28long%29) -
    durata solicitării (exprimată în milisecunde), după care nu mai sunt
    furnizate actualizări cu privire la locația curentă (momentul de
    timp la care sunt raportate este cel în care este apelată metoda, nu
    cel în care este realizată solicitarea propriu-zisă);
-   [setExpirationTime(long)](http:*developer.android.com/reference/com/google/android/gms/location/LocationRequest.html#setExpirationTime%28long%29) -
    momentul de timp după care nu mai sunt furnizate actualizări cu
    privire la locația curentă, exprimat în milisecunde raportat la
    perioada în care dispozitivul mobil a fost pornit;
-   [setInterval(long)](http:*developer.android.com/reference/com/google/android/gms/location/LocationRequest.html#setInterval%28long%29) -
    indică intervalul de timp (exprimat în milisecunde) la care se
    dorește să se primească actualizările cu privire la locația curentă;
    acesta poate fi însă:
    -   mai mic, dacă dispozitivul mobil are probleme legate de
        conectivitate;
    -   mai mare, dacă există alte aplicații care au stabilit alte rate
        de transfer.
-   [setFastestInterval(long)](http:*developer.android.com/reference/com/google/android/gms/location/LocationRequest.html#setFastestInterval%28long%29) -
    precizează intervalul la care aplicația Android poate să gestioneze
    actualizările cu privire la locația curentă, în situația în care
    există și alte aplicații care au specificat alte rate de transfer,
    pentru a preîntâmpina situații cum ar fi imposibilitatea de
    actualizare corespunzătoare a interfeței grafice sau lipsa de spațiu
    de stocare disponibil pentru informațiile respective;

---
**Note**

Frecvența cu care sunt transmise actualizările periodice cu
privire la modificarea locației curentă este dată de cea mai rapidă rată
de transfer specificată de toate aplicațiile care accesează o astfel de
funcționalitate.\

---

---
**Note**

În situația în care aplicația Android realizează procesări
complexe, care implică o perioadă de timp considerabilă, este recomandat
ca valoarea transmisă metodei `setFastestInterval()` să fie
corespunzătoare, astfel încât să nu fie furnizate valori care nu pot fi
utilizate.\

---

-   [setMaxWaitTime(long)](http:*developer.android.com/reference/com/google/android/gms/location/LocationRequest.html#setMaxWaitTime%28long%29) -
    specifică perioada de așteptare maximă pentru transmiterea
    actualizărilor periodice referitoare la locația curentă; astfel, mai
    multe informații de acest tip pot fi livrate împreună, cu frecvența
    indicată de acest interval, optimizând consumul de baterie
    (actualizările periodice sunt primite la intervale de maxWaitTime,
    numărul de seturi de date fiind maxWaitTime / interval);
-   [setNumUpdates(int)](http:*developer.android.com/reference/com/google/android/gms/location/LocationRequest.html#setNumUpdates%28int%29) -
    determină numărul de actualizări necesare, în caz contrar fiind
    furnizate valori de acest tip continuu, între apelurile metodelor
    `requestLocationUpdates()` și `removeLocationUpdates()`;
-   [setPriority()](http:*developer.android.com/reference/com/google/android/gms/location/LocationRequest.html#setPriority%28int%29) -
    stabilește prioritatea solicitării, oferind informații cu privire la
    furnizorul de servicii care va fi utilizat:
    -   `PRIORITY_BALANCED_POWER_ACCURACY` - gradul de acuratețe este
        relativ (aproximativ 100 de metri), consumul de energie fiind
        moderat;
    -   `PRIORITY_HIGH_ACCURACY` - gradul de acuratețe este ridicat
        (aproximativ 10 metri), pe baza informațiilor provenite de la
        sistemul global de poziționare (GPS), cu un consum mare de
        energie;
    -   `PRIORITY_LOW_POWER` - gradul de acuratețe este scăzut
        (aproximativ 10 kilometri), sursele folosite fiind rețeaua
        mobilă / fără fir, cu un consum mic de energie;
    -   `PRIORITY_NO_POWER` - utilizat atunci când se dorește
        transmiterea de actualizări periodice cu privire la locația
        curentă, fără un impact semnificativ asupra consumului de
        energie (de regulă, astfel de informații sunt preluate de la
        alte aplicații);
-   [setSmallestDisplacement(int)](http:*developer.android.com/reference/com/google/android/gms/location/LocationRequest.html#setSmallestDisplacement%28float%29) -
    indică distanța minimă dintre locații pentru care se primește
    actualizare periodică (implicit, are valoarea 0).

De regulă, instanțierea unui obiect de tip `LocationRequest` precum și
precizarea parametrilor ce caracterizează solicitările cu privire la
actualizările periodice sunt realizate o singură dată, în momentul în
care aplicația Android este pornită (pe metoda `onCreate()`), urmând ca
eliberarea resurselor să fie realizată atunci când aplicația Android
este oprită (pe metoda `onDestroy()`).

``` java
locationRequest = new LocationRequest();
locationRequest.setInterval(Constants.LOCATION_REQUEST_INTERVAL);
locationRequest.setFastestInterval(Constants.LOCATION_REQUEST_FASTEST_INTERVAL);
locationRequest.setPriority(LocationRequest.PRIORITY_HIGH_ACCURACY);
```

O aplicație Android primește actualizări periodice cu privire la locația
curentă între momentele de timp la care specifică explicit acest lucru,
prin apelul metodelor corespunzătoare:

-   [requestLocationUpdates(GoogleApiClient, LocationRequest,
    LocationListener)](http:*developer.android.com/reference/com/google/android/gms/location/FusedLocationProviderApi.html#requestLocationUpdates%28com.google.android.gms.common.api.GoogleApiClient,%20com.google.android.gms.location.LocationRequest,%20com.google.android.gms.location.LocationListener%29) -
    pornește transmitersa actualizărilor periodice;
-   [removeLocationUpdates(GoogleApiClient,
    LocationListener)](http:*developer.android.com/reference/com/google/android/gms/location/FusedLocationProviderApi.html#removeLocationUpdates%28com.google.android.gms.common.api.GoogleApiClient,%20com.google.android.gms.location.LocationListener%29) -
    oprește transmiterea actualizărilor periodice.

Întrucât aceste metode primesc un parametru de tip `GoogleApiClient`,
este necesar ca acesta să fie nenul și să fie conectat. Din acest motiv,
o practică curentă vizează realizarea suplimentară a acestor verificări
anterior invocării lor propriu-zise.

``` java
protected void startLocationUpdates() {
  LocationServices.FusedLocationApi.requestLocationUpdates(
    googleApiClient,
    locationRequest,
    this
  );
  locationUpdatesStatus = true;
  googleMap.setMyLocationEnabled(true);
  if (lastLocation != null) {
    navigateToLocation(lastLocation);
  }
  
  * ...
  
}
    
protected void stopLocationUpdates() {
  LocationServices.FusedLocationApi.removeLocationUpdates(
    googleApiClient,
    this
  );
  locationUpdatesStatus = false;
  googleMap.setMyLocationEnabled(false);

  * ...

}
```

Pentru ca impactul asupra consumului de energie să fie optim, se
recomandă ca pe metodele care controlează ciclul de viață al unei
aplicații Android să se gestioneze corespunzător starea transmiterii de
actualizări periodice, în intervalele de timp în care aceasta nu este
activă / vizibilă.

``` java
@Override
protected void onStart() {
  super.onStart();

  * ...
  
  if (googleApiClient != null && googleApiClient.isConnected() && locationUpdatesStatus) {
    startLocationUpdates();
  }
}
    
@Override
protected void onStop() {
  stopLocationUpdates();
        
  * ...
  
  super.onStop();
}
```

Metodele care gestionează starea transmiterii de actualizări periodice
cu privire la locația curentă primesc ca parametru și un obiect
ascultător de tip
[LocationListener](http:*developer.android.com/reference/com/google/android/gms/location/LocationListener.html)
care notifică utilizatorul în momentul în care sunt disponibile
informațiile propriu-zise: metoda `onLocationChanged(Location)`, apelată
în mod automat, oferă informații cu privire la poziția din momentul de
timp respectiv.

``` java
@Override
public void onLocationChanged(Location location) {
  lastLocation = location;
  navigateToLocation(lastLocation);
}
```

Aplicația Android trebuie să aibă un comportament consistent în situația
în care se produc modificări de configurație, astfel încât diferiții
parametrii trebuie salvați și încărcați pe metodele corespunzătoare
(`onSaveInstanceState(Bundle)`, respectiv
`onRestoreInstanceState(Bundle)`):

``` java
@Override
public void onSaveInstanceState(Bundle savedInstanceState) {
  saveValues(savedInstanceState);
  super.onSaveInstanceState(savedInstanceState);
}
    
protected void saveValues(Bundle state) {
  state.putBoolean(Constants.LOCATION_UPDATES_STATUS, locationUpdatesStatus);
  state.putParcelable(Constants.LAST_LOCATION, lastLocation);
}
    
@Override
public void onRestoreInstanceState(Bundle savedInstanceState) {
  super.onRestoreInstanceState(savedInstanceState);
  restoreValues(savedInstanceState);
}
    
protected void restoreValues(Bundle state) {
  if (state.keySet().contains(Constants.LAST_LOCATION)) {
    lastLocation = state.getParcelable(Constants.LAST_LOCATION);
  }
  if (state.keySet().contains(Constants.LOCATION_UPDATES_STATUS)) {
    locationUpdatesStatus = state.getBoolean(Constants.LOCATION_UPDATES_STATUS);
  }
}
```

Informațiile de interes sunt starea referitoare la transmiterea
actualizărilor periodice, respectiv la cea mai recentă locație.

## Codificare Geografică Inversă (Geocoding), opțional

Acest exercițiu este opțional, cere activarea facturării (Billing) în
contul google pentru care activati Geocoding API. \<spoiler> În Android,
clasa
[Geocoder](http:*developer.android.com/reference/android/location/Geocoder.html)
permite realizarea de conversii dintre coordonate GPS (latitudine /
longitudine) și adresa poștală, operație denumită codificare geografică
inversă.

Metodele `getFromLocation()` / `getFromLocationName()`, disponibile în
mai multe forme, furnizează o listă de obiecte de tip
[Address](http:*developer.android.com/reference/android/location/Address.html),
care încapsulează, pe lângă datele propriu-zise, dispuse sub formă de
rânduri distincte și alte informații precum latitudine, longitudine,
localitate, cod poștal, telefon, URL, împrejurimi:

-   [getFromLocation(double, double,
    int)](http:*developer.android.com/reference/android/location/Geocoder.html#getFromLocation%28double,%20double,%20int%29) -
    primește ca parametrii coordonatele GPS (latitudinea /
    longitudinea);
-   [getFromLocationName(String, int, double, double, double,
    double)](http:*developer.android.com/reference/android/location/Geocoder.html#getFromLocationName%28java.lang.String,%20int,%20double,%20double,%20double,%20double%29) -
    primește ca parametrii o descriere a locației precum și o zonă
    geografică descrisă prin coordonatele GPS (latitudine / longitudine)
    ale punctelor stânga sus - dreapta jos;
-   [getFromLocationName(String,
    int)](http:*developer.android.com/reference/android/location/Geocoder.html#getFromLocationName%28java.lang.String,%20int%29) -
    primește ca parametru o descriere a locației.

---
**Note**

Toate aceste metode primesc un parametru care indică numărul
de rezultate care se doresc a fi furnizate. De regulă, acesta are
valoarea 1.\

---

Metodele care realizează codificarea geografică inversă sunt sincrone,
iar procesările pe care le realizează pot să dureze un interval de timp
considerabil. Din acest motiv, este recomandat ca invocarea acestora să
nu se facă pe firul de execuție al interfeței grafice (principal)
întrucât poate afecta experiența utilizatorului, ci pe un fir de
execuție care rulează în fundal, de tip
[IntentService](http:*developer.android.com/reference/android/app/IntentService.html)
(utilizarea clasei `AsyncTask` nu este indicată în această situație
întrucât comportamentul său în cazul producerii unor întreruperi nu
corespunde funcționalității dorite). Un astfel de obiect pornește în
momentul în care este necesar să se realizeze o operație (fiind invocat
prin intermediul unei intenții, la care pot fi atașate informații
suplimentare), realizată pe un fir de execuție dedicat, fiind oprit în
momentul în care nu mai este necesar să realizeze alte procesări.

Acest serviciu asociat unei intenții trebuie să fie specificat în
fișierul `AndroidManifest.xml`, în secțiunea
`<application> ... </application>`:

``` xml
<manifest ...>
  <!-- other elements -->
  <application ...>
    <!-- other elements -->
    <service
      android:name=".service.GetLocationAddressIntentService"
      android:exported="false"/>
   </application>
</manifest>
```

Nu este necesar să se specifice și un filtru de intenții, de vreme ce
serviciul va fi lansat în execuție explicit, prin transmiterea în cadrul
intenției corespunzătoare a denumirii clasei care îl implementează.

Obiectele care vor fi transmise serviciului prin intermediul intenției
sunt:

-   un obiect de tip
    [ResultReceiver](http:*developer.android.com/reference/android/os/ResultReceiver.html),
    prin intermediul căruia este furnizat rezultatul, atunci când acesta
    este disponibil;
    `private class AddressResultReceiver extends ResultReceiver {
      public AddressResultReceiver(Handler handler) {
        super(handler);
      }

      @Override
      protected void onReceiveResult(int resultCode, Bundle bundle) {
        String address = bundle.getString(Constants.RESULT);
        addressTextView.setText(address);

        switch(resultCode) {
          case Constants.RESULT_SUCCESS:
            Toast.makeText(GoogleMapsActivity.this, "An address was found", Toast.LENGTH_SHORT).show();
        break;
          case Constants.RESULT_FAILURE:
            Toast.makeText(GoogleMapsActivity.this, "An address was not found", Toast.LENGTH_SHORT).show();
        break;                  
        }

        getAddressLocationStatus = false;
        getLocationAddressButton.setEnabled(true);
      }
    }
    ` Se observă că atunci când rezultatul este disponibil, se apelează
    în mod automat metoda `onReceiveResult()` care primește ca
    parametrii un cod de rezultat numeric (succes sau eșec, definit de
    utilizator) și un obiect de tip `Bundle` în care sunt plasate
    informații suplimentare (adresa propriu-zisă sau mesajul de eroare -
    în funcție de rezultat -, vizualizată într-un control grafic).
-   locația care se dorește a fi rezolvată (obiect de tip `Location`,
    incluzând informații de tip latitudine și longitudine).

Mecanismul prin care se pornește un serviciu prin intermediul unei
intenții este similar cu cel prin care se pornește o activitate prin
intermediul unei intenții:

1.  se instanțiază un obiect de tip `Intent` specificând clasa
    corespunzătoare serviciului care se dorește a fi lansat în execuție;
2.  se plasează informațiile în obiectul `Bundle` disponibil în
    secțiunea `extra`.

``` java
Intent intent = new Intent(this, GetLocationAddressIntentService.class);
intent.putExtra(Constants.RESULT_RECEIVER, addressResultReceiver);
intent.putExtra(Constants.LOCATION, lastLocation);
startService(intent);
```

Procesarea pe care o realizează serviciul lansat în execuție prin
intermediul unei intenții este plasată în cadrul metodei
`onHandleIntent(Intent)`, apelată în mod automat.

``` java
@Override
protected void onHandleIntent(Intent intent) {
  String errorMessage = null;
        
  resultReceiver = intent.getParcelableExtra(Constants.RESULT_RECEIVER);
  if (resultReceiver == null) {
    errorMessage = "No result receiver was provided to handle the information";
    Log.e(Constants.TAG, "An exception has occurred: " + errorMessage);
    return;
  }
        
  Location location = intent.getParcelableExtra(Constants.LOCATION);
  if (location == null) {
    errorMessage = "No location data was provided";
    Log.e(Constants.TAG, "An exception has occurred: " + errorMessage);
    handleResult(Constants.RESULT_FAILURE, errorMessage);
    return;
  }
        
  Geocoder geocoder = new Geocoder(this, Locale.getDefault());
        
  List<Address> addressList = null;
        
  try {
    addressList = geocoder.getFromLocation(
      location.getLatitude(),
      location.getLongitude(),
      Constants.NUMBER_OF_ADDRESSES);
  } catch (IOException ioException) {
    errorMessage = "The background geocoding service is not available";
    Log.e(Constants.TAG, "An exception has occurred: " + ioException.getMessage());
  } catch (IllegalArgumentException illegalArgumentException) {
    errorMessage = "The latitude / longitude values that were provided are invalid " + location.getLatitude() + " / " + location.getLongitude();
    Log.e(Constants.TAG, "An exception has occurred: " + illegalArgumentException.getMessage());
  }

  if (errorMessage != null && !errorMessage.isEmpty()) {
    handleResult(Constants.RESULT_FAILURE, errorMessage);
    return;
  }

  if (addressList == null || addressList.isEmpty()) {
    errorMessage = "The geocoder could not find an address for the given latitude / longitude";
    Log.e(Constants.TAG, "An exception has occurred: " + errorMessage);
    handleResult(Constants.RESULT_FAILURE, errorMessage);
    return;
  }
        
  StringBuffer result = new StringBuffer();
        
  for (Address address: addressList) {
    for (int k = 0; k < address.getMaxAddressLineIndex(); k++) {
      result.append(address.getAddressLine(k) + System.getProperty("line.separator"));
    }
    result.append(System.getProperty("line.separator"));
  }
  handleResult(Constants.RESULT_SUCCESS, result.toString());
}
```

Operațiile realizate de serviciu, pe firul de execuție separat, sunt:

1.  preluarea informațiilor necesare (obiect de tip `ResultReceiver`,
    locația care se dorește a fi rezolvată) printr-un obiect `Bundle`,
    din cadrul secțiunii `extra` a intenției prin care a fost invocat;
    în situația în care acestea nu pot fi obținute, se generează un
    mesaj de eroare;
2.  instanțierea unui obiect de tip `Geocoder`, folosind contextul
    (serviciul) și un obiect
    [Locale](http:*developer.android.com/reference/java/util/Locale.html),
    care conține informații cu privire la modul de prezentare a unor
    informații în funcție de zona geografică;
3.  invocarea metodelor `getFromLocation()` / `getFromLocationName()`
    (furnizând informațiile necesare ca parametri) și gestionând
    corespunzător tipurile de eroare ce pot fi generate:
    1.  serviciul Geocoding nu este disponibil (se aruncă o excepție de
        tip `IOException`);
    2.  informațiile cu privire la coordonatele GPS (latitudine /
        longitudine) nu sunt corecte (se aruncă o excepție de tipul
        `IllegalArgumentException`);
4.  se semnalează situația în care nu a putut fi identificată nici o
    adresă poștală asociată datelor specificate;
5.  pentru fiecare adresă poștală furnizată, se concatenează rândurile
    distincte:
    1.  numărul de rânduri conținute este întors de metoda
        [getMaxAddressLineIndex()](http:*developer.android.com/reference/android/location/Address.html#getMaxAddressLineIndex%28%29);
    2.  un rând de la o anumită poziție este dat de metoda
        [getAddressLine(int)](http:*developer.android.com/reference/android/location/Address.html#getAddressLine%28int%29);
6.  se transmite codul de rezultat (numeric - succes sau eșec) precum și
    rezultatul propriu-zis (adresa sau mesajul de eroare) către obiectul
    de tip `ResultReceiver`, prin intermediul metodei [send(int,
    Bundle)](http:*developer.android.com/reference/android/os/ResultReceiver.html#send%28int,%20android.os.Bundle%29)
    care face ca la nivelul acestui obiect să se apeleze în mod automat
    metoda `onReceiveResult()`; informațiile vor fi plasate în cadrul
    unui obiect `Bundle`, ca pereche (cheie, valoare):
    `private void handleResult(int resultCode, String message) {
      Bundle bundle = new Bundle();
      bundle.putString(Constants.RESULT, message);
      resultReceiver.send(resultCode, bundle);
    }
    `

\</spoiler>

## Implementarea Zonelor de Restricție Geografică (Geofencing)

În Android, în contextul transmiterii de actualizări periodice cu
privire la locația curentă, există posibilitatea ca un utilizator să fie
notificat cu privire la acțiunile legate de o anumită zonă de restricție
geografică, definită ca arie circulară, caracterizată printr-un centru,
dat de coordonate GPS (latitudine / longitudine) și de o rază.

Este impusă restricția de a gestiona simultan maxim 100 de zone de
restricție geografică active la un moment dat (fiecare restricție
geografică are o perioadă de valabilitate).

Evenimentele generate în legătură cu o zonă de restricție geografică
sunt legate de intrare, respectiv de ieșirea utilizatorului din acest
spațiu, însă notificările pot fi temporizate o anumită perioadă. Acestea
trebuie procesate pe un fir de execuție dedicat, a cărui execuție
trebuie să fie limitată la procesările legate de un anumit tip de
eceniment. În acest sens, va fi utilizat un obiect de tip
`IntentService`, instanțiat în momentul în care aplicația Android este
creată (pe metoda `onCreate()`), resursele aferente fiind eliberate în
momentul în care aplicația Android este distrusă (pe metoda
`onDestroy()`). Acesta va fi reutilizat atât pentru operația de tip
adăugare cât și pentru operația de tip ștergere a unei zone de
restricție geografică.

``` java
Intent intent = new Intent(this, GeofenceTrackerIntentService.class);
geofenceTrackerPendingIntent = PendingIntent.getService(this, 0, intent, PendingIntent.FLAG_UPDATE_CURRENT);
```

Disponibilitatea unui serviciu care să realizeze procesări legate de
zonele de restricție geografică trebuie menționată în cadrul fișierului
`AndroidManifest.xml`:

``` xml
<manifest ...>
  <!-- other elements -->
  <application ...>
    <!-- other elements -->
    <service
      android:name=".service.GeofenceTrackerIntentService"
      android:exported="false"/>
   </application>
</manifest>
```

Metoda `onHandleIntent(Intent)` a serviciului lansat în execuție prin
intermediul unei intenții va procesa evenimentul legat de zona de
restricție geografică
([GeofencingEvent](https:*developer.android.com/reference/com/google/android/gms/location/GeofencingEvent.html))
care îi este transmis:

1.  se verifică situația în care evenimentul legat de zona de restricție
    geografică conține o eroare (informație furnizată de metoda
    [hasError()](https:*developer.android.com/reference/com/google/android/gms/location/GeofencingEvent.html#hasError%28%29)),
    aceasta fiind procesată în mod corespunzător (codul de eroare este
    furnizat de metoda
    [getErrorCode()](https:*developer.android.com/reference/com/google/android/gms/location/GeofencingEvent.html#getErrorCode%28%29):
    1.  `GeofenceStatusCodes.GEOFENCE_NOT_AVAILABLE` - serviciul de
        restricționare geografică nu este disponibil;
    2.  `GEOFENCE_TOO_MANY_GEOFENCES` - au fost definite mai multe zone
        de restricție geografică (restricționate la maxim 100);
    3.  `GEOFENCE_TOO_MANY_PENDING_INTENTS` - există mai multe servicii
        care procesează evenimente legate de restricționarea geografică;
    4.  alt tip de eroare.
2.  este obținut tipul de tranziție, prin intermediul metodei
    [getGeofenceTransition()](https:*developer.android.com/reference/com/google/android/gms/location/GeofencingEvent.html#getGeofenceTransition%28%29)
    1.  `Geofence.GEOFENCE_TRANSITION_ENTER` - utilizatorul a intrat în
        zona de restricție geografică;
    2.  `Geofence.GEOFENCE_TRANSITION_EXIT` - utilizatorul a ieșit din
        zona de restricție geografică.
3.  se obține lista cu zonele de restricție geografică care au
    determinat declanșarea evenimentelor respective, prin apelarea
    metodei
    [getTriggeringGeofences()](https:*developer.android.com/reference/com/google/android/gms/location/GeofencingEvent.html#getTriggeringGeofences%28%29);
    pentru fiecare obiect `Geofence` implicat, se obține identificatorul
    (generat de regulă aleator), concatenându-se la mesajul ce conține
    detaliile tranziției;
4.  este creată o notificare, la accesarea căreia se va lansa o
    activitate Android în care va putea fi vizualizat mesajul cu
    detaliile tranziției.

``` java
@Override
protected void onHandleIntent(Intent intent) {
  GeofencingEvent geofencingEvent = GeofencingEvent.fromIntent(intent);
  if (geofencingEvent.hasError()) {
    String errorMessage = null;
    switch(geofencingEvent.getErrorCode()) {
      case GeofenceStatusCodes.GEOFENCE_NOT_AVAILABLE:
        errorMessage = Constants.GEOFENCE_NOT_AVAILABLE_ERROR;
        break;
      case GeofenceStatusCodes.GEOFENCE_TOO_MANY_GEOFENCES:
    errorMessage = Constants.GEOFENCE_TOO_MANY_GEOFENCES_ERROR;
        break;
      case GeofenceStatusCodes.GEOFENCE_TOO_MANY_PENDING_INTENTS:
    errorMessage = Constants.GEOFENCE_TOO_MANY_PENDING_INTENTS_ERROR;
        break;
      default:
    errorMessage = Constants.GEOFENCE_UNKNOWN_ERROR;
        break;
    }
    Log.e(Constants.TAG, "An exception has occurred: " + errorMessage);
    return;
  }
  int geofenceTransition = geofencingEvent.getGeofenceTransition();
  if (geofenceTransition == Geofence.GEOFENCE_TRANSITION_ENTER ||
    geofenceTransition == Geofence.GEOFENCE_TRANSITION_EXIT) {
    List<Geofence> triggeringGeofences = geofencingEvent.getTriggeringGeofences();
    StringBuffer transitionStringDetails = null;
    switch(geofenceTransition) {
      case Geofence.GEOFENCE_TRANSITION_ENTER:
        transitionStringDetails = new StringBuffer(Constants.GEOFENCE_TRANSITION_ENTER);
    break;
      case Geofence.GEOFENCE_TRANSITION_EXIT:
    transitionStringDetails = new StringBuffer(Constants.GEOFENCE_TRANSITION_EXIT);
    break;
      default:
        transitionStringDetails = new StringBuffer(Constants.GEOFENCE_TRANSITION_UNKNOWN);
    break;
    }
    transitionStringDetails.append(": ");
    for (Geofence geofence: triggeringGeofences) {
      transitionStringDetails.append(geofence.getRequestId() + ", ");
    }
    String transitionString = transitionStringDetails.toString();
    if (transitionString.endsWith(", ")) {
      transitionString = transitionString.substring(0, transitionString.length() - 2);
    }
    sendNotification(transitionString);
    Log.i(Constants.TAG, "The geofence tansaction has been processed: " + transitionString);
  } else {
    Log.e(Constants.TAG, "An exception has occurred: " + Constants.GEOFENCE_TRANSITION_UNKNOWN + " " + geofenceTransition);
  }
}
```

Transmiterea propriu-zisă a notificării implică invocarea unei
activități prin intermediul unui obiect de tip `PendingIntent`. Aceasta
este atașată unei ierarhii, fiind transmisă prin plasarea sa pe stiva de
activități.

``` xml
<manifest ...>
  <!-- other elements -->
  <application ...>
    <!-- other elements -->
    <activity
      android:name=".graphicuserinterface.GoogleMapsGeofenceEventActivity"
      android:parentActivityName=".graphicuserinterface.GoogleMapsActivity">
      <metadata
        android:name="android.support.PARENT_ACTIVITY"
        android:value=".graphicuserinterface.GoogleMapsActivity"/>
    </activity>
  </application>
</manifest>
```

``` java
private void sendNotification(String notificationDetails) {
  Intent notificationIntent = new Intent(getApplicationContext(), GoogleMapsGeofenceEventActivity.class);
  notificationIntent.putExtra(Constants.NOTIFICATION_DETAILS, notificationDetails);
        
  TaskStackBuilder stackBuilder = TaskStackBuilder.create(this);
  stackBuilder.addParentStack(GoogleMapsGeofenceEventActivity.class);
  stackBuilder.addNextIntent(notificationIntent);

  PendingIntent notificationPendingIntent = stackBuilder.getPendingIntent(0, PendingIntent.FLAG_UPDATE_CURRENT);

  NotificationCompat.Builder builder = new NotificationCompat.Builder(this);
  builder.setSmallIcon(R.drawable.ic_launcher)
    .setLargeIcon(BitmapFactory.decodeResource(getResources(), R.drawable.ic_launcher))
    .setColor(Color.RED)
    .setContentTitle(Constants.GEOFENCE_TRANSITION_EVENT)
    .setContentText(notificationDetails)
    .setContentIntent(notificationPendingIntent);
  builder.setAutoCancel(true);

  NotificationManager notificationManager = (NotificationManager) getSystemService(Context.NOTIFICATION_SERVICE);
  notificationManager.notify(0, builder.build());
}
```

Operațiile care pot fi realizate legate de o zonă de restricție
geografică sunt:

**1.** adăugarea unei zone de restricție geografică.

O zonă de restricție geografică este construit prin intermediul unei
clase
[Geofence.Builder](https:*developer.android.com/reference/com/google/android/gms/location/Geofence.Builder.html),
în care se specifică parametrii acesteia:

-   [setCircularRegion(double, double,
    float)](https:*developer.android.com/reference/com/google/android/gms/location/Geofence.Builder.html#setCircularRegion%28double,%20double,%20float%29) -
    se indică coordonatele zonei de restricție geografice:
    -   centru - latitudine + longitudine;
    -   raza;
-   [setExpirationDuration(long)](https:*developer.android.com/reference/com/google/android/gms/location/Geofence.Builder.html#setExpirationDuration%28long%29) -
    se precizează durata de timp (exprimată în milisecunde) după care
    zona de restricția geografică nu va mai fi activă;
-   [setLoiteringDelay(int)](https:*developer.android.com/reference/com/google/android/gms/location/Geofence.Builder.html#setLoiteringDelay%28int%29) -
    se exprimă o durată de timp (exprimată în milisecunde) în care este
    temporizată transmiterea de notificări, în situația în care se
    produc evenimente legate de zona de restricție geografică, cu durata
    mai mică decât cea indicată;
-   [setNotificationResponsiveness(int)](https:*developer.android.com/reference/com/google/android/gms/location/Geofence.Builder.html#setNotificationResponsiveness%28int%29) -
    se stabilește durata de timp (exprimată în milisecunde) după care va
    fi transmisă notificarea;
-   [setRequestId(String)](https:*developer.android.com/reference/com/google/android/gms/location/Geofence.Builder.html#setRequestId%28java.lang.String%29) -
    se asociază un identificator unic, prin care zona de restricție
    geografică va putea fi referită în cadrul aplicației Android;
-   [setTransitionTypes(int)](https:*developer.android.com/reference/com/google/android/gms/location/Geofence.Builder.html#setTransitionTypes%28int%29) -
    se asociază tipurile de tranziții pentru care se vor transmite
    notificări (de regulă, `Geofence.GEOFENCE_TRANSITION_ENTER` și
    `Geofence.GEOFENCE_TRANSITION_EXIT`).

O solicitare legată de o zonă de restricție geografică, conținută de un
obiect
[GeofencingRequest](http:*developer.android.com/reference/com/google/android/gms/location/GeofencingRequest.html),
este construită prin apelul metodelor `addGeofence(Geofence)` /
`addGeofences(List<Geofence>)`, respectiv `build()` din cadrul clasei
ajutătoare
[GeofencingRequest.Builder](http:*developer.android.com/reference/com/google/android/gms/location/GeofencingRequest.Builder.html).

Operația de adăugare este realizată prin apelul metodei
[addGeofences(GoogleApiClient, GeofencingRequest,
PendingIntent)](http:*developer.android.com/reference/com/google/android/gms/location/GeofencingApi.html#addGeofences%28com.google.android.gms.common.api.GoogleApiClient,%20com.google.android.gms.location.GeofencingRequest,%20android.app.PendingIntent%29)
din clasa
[GeofencingApi](http:*developer.android.com/reference/com/google/android/gms/location/GeofencingApi.html).
Rezultatul acestei operații este furnizat prin intermediul unei clase
ascultător
[ResultCallback\<T>](http:*developer.android.com/reference/com/google/android/gms/common/api/ResultCallback.html),
pentru care se implementează metoda `onResult(T)`. Aceasta trebuie
precizată explicit prin metoda
[setREsultCallback(ResultCallback\<T>)](http:*developer.android.com/reference/com/google/android/gms/common/api/PendingResult.html#setResultCallback%28com.google.android.gms.common.api.ResultCallback%3CR%3E%29),
aplicabilă obiectului de tip
[PendingResult](http:*developer.android.com/reference/com/google/android/gms/common/api/PendingResult.html),
construit anterior.

``` java
private void addGeofence(String latitude, String longitude, String radius) {
  if (googleApiClient == null || !googleApiClient.isConnected()) {
    Toast.makeText(
      GoogleMapsActivity.this,
      "Google API Client is null or not connected!",
      Toast.LENGTH_SHORT
    ).show();
    return;
  }
  if (latitude == null || latitude.isEmpty() ||
    longitude == null || longitude.isEmpty() ||
    radius == null || radius.isEmpty()) {
    Toast.makeText(
      GoogleMapsActivity.this,
      "All fields (gps coordinates, radius) should be filled!",
      Toast.LENGTH_SHORT
    ).show();
    return;
  }
  geofenceList.add(new Geofence.Builder()
    .setRequestId(Utilities.generateGeofenceIdentifier(Constants.GEOFENCE_IDENTIFIER_LENGTH))
    .setCircularRegion(
      Double.parseDouble(latitude),
      Double.parseDouble(longitude),
      Float.parseFloat(radius)
    )
    .setExpirationDuration(Constants.GEOFENCE_EXPIRATION_IN_MILLISECONDS)
    .setTransitionTypes(
      Geofence.GEOFENCE_TRANSITION_ENTER |
      Geofence.GEOFENCE_TRANSITION_EXIT
    )
    .build());
  GeofencingRequest.Builder builder = new GeofencingRequest.Builder();
  builder.setInitialTrigger(GeofencingRequest.INITIAL_TRIGGER_ENTER);
  builder.addGeofences(geofenceList);
  GeofencingRequest geofencingRequest = builder.build();
  LocationServices.GeofencingApi.addGeofences(
    googleApiClient,
    geofencingRequest,
    geofenceTrackerPendingIntent
  ).setResultCallback(GoogleMapsActivity.this);
}
```

**2.** ștergerea unei zone de restricție geografică:

Operația de ștergere este realizată prin apelul metodei
[removeGeofences(GoogleApiClient,
PendingIntent)](https:*developer.android.com/reference/com/google/android/gms/location/GeofencingApi.html#removeGeofences%28com.google.android.gms.common.api.GoogleApiClient,%20android.app.PendingIntent%29)
din clasa
[GeofencingApi](http:*developer.android.com/reference/com/google/android/gms/location/GeofencingApi.html),
aceasta referindu-se la toate zonele de restricție geografică.
Rezultatul acestei operații este furnizat prin intermediul unei clase
ascultător
[ResultCallback\<T>](http:*developer.android.com/reference/com/google/android/gms/common/api/ResultCallback.html),
pentru care se implementează metoda `onResult(T)`. Aceasta trebuie
precizată explicit prin metoda
[setREsultCallback(ResultCallback\<T>)](http:*developer.android.com/reference/com/google/android/gms/common/api/PendingResult.html#setResultCallback%28com.google.android.gms.common.api.ResultCallback%3CR%3E%29),
aplicabilă obiectului de tip
[PendingResult](http:*developer.android.com/reference/com/google/android/gms/common/api/PendingResult.html),
construit anterior.

``` java
private void removeGeofence() {
  if (googleApiClient == null || !googleApiClient.isConnected()) {
    Toast.makeText(
      GoogleMapsActivity.this,
      "Google API Client is null or not connected!",
      Toast.LENGTH_SHORT
    ).show();
    return;
  }
  latitudeEditText.setText(new String());
  longitudeEditText.setText(new String());
  radiusEditText.setText(new String());
  geofenceList.clear();
  LocationServices.GeofencingApi.removeGeofences(
    googleApiClient,
    geofenceTrackerPendingIntent
  ).setResultCallback(GoogleMapsActivity.this);
}
```

Se poate observa faptul că ambele operații au nevoie de un client Google
API nenul și care să fie conectat, motiv pentru care anterior sunt
realizate verificările de rigoare, cu semnalarea eventualelor erori.

Zonele de restricție geografică sunt menținute în cadrul unei liste,
actualizată corespunzător pentru fiecare dintre operațiile de adăugare /
ștergere.

Metoda `onResult(Status)`, care furnizează rezultatul operațiilor de
adăugare / ștergere a unei zone de restricție geografică, conține
informații suplimentare cu privire la situația curentă:

1.  `isSuccess()` - operația a fost realizată cu success sau cu eșec;
2.  `getStatusCode()` - codul de stare, în situația în care s-a produs o
    eroare.

``` java
@Override
public void onResult(Status status) {
  if (status.isSuccess()) {
    geofenceStatus = !geofenceStatus;
  } else {
    String errorMessage = null;
    switch(status.getStatusCode()) {
      case GeofenceStatusCodes.GEOFENCE_NOT_AVAILABLE:
        errorMessage = Constants.GEOFENCE_NOT_AVAILABLE_ERROR;
        break;
      case GeofenceStatusCodes.GEOFENCE_TOO_MANY_GEOFENCES:
        errorMessage = Constants.GEOFENCE_TOO_MANY_GEOFENCES_ERROR;
        break;
      case GeofenceStatusCodes.GEOFENCE_TOO_MANY_PENDING_INTENTS:
        errorMessage = Constants.GEOFENCE_TOO_MANY_PENDING_INTENTS_ERROR;
        break;
      default:
    errorMessage = Constants.GEOFENCE_UNKNOWN_ERROR;
        break;
    }
    Log.e(Constants.TAG, "An exception has occurred while turning the geofencing on/off: " + status.getStatusCode() + " " + errorMessage);
  }
}
```

În situația în care aplicația este întreruptă, informațiile legate de
zonele geografice trebuie gestionate corespunzător, fiind recomandat ca
persistența să fie realizată prin intermediul unui obiect de tip
`SharedPreferences`.

1.  atunci când aplicația Android nu mai este vizibilă, se salvează
    datele și sunt șterse toate zonele de restricție geografică, astfel
    încât să nu mai fie transmise notificări;
2.  atunci când aplicația Android este vizibilă, se încarcă datele și
    sunt adăugate toate zonele de restricție geografică, în cazul în
    care acestea au fost definite anterior.

## Activitate de Laborator

**1.** Să se acceseze [Google Developer's
Console](https:*console.developers.google.com), după ce a fost
realizată autentificarea cu datele contului Google (nume de utilizator,
parolă):

-   se obține un număr de proiect (dacă această operație nu a fost
    realizată anterior);
-   se activează serviciul *Google Maps Android API*;
-   se generează o semnătură digitală de tip SHA-1 folosind utilitarul
    Java `keytool`;
-   se creează o cheie publică pentru transmiterea de mesaje provenind
    de la un dispozitiv mobil, pe baza semnăturii digitale și a
    pachetului care identifică în mod unic aplicația respectivă.

---
**Note**

Pentru toate aplicațiile Android va trebui completată
cheia publică în fișierul `AndroidManifest.xml`.\

---

Mai multe detalii pot fi obținute în secțiunea
[Configurare](/eim/laboratoare/laborator10#configurare).

**2.** În contul Github personal, să se creeze un depozit denumit
'Laborator10'. Inițial, acesta trebuie să fie gol (nu trebuie să bifați
nici adăugarea unui fișier `README.md`, nici a fișierului `.gitignore`
sau a a fișierului `LICENSE`).

**3.** Să se cloneze în directorul de pe discul local conținutul
depozitului la distanță de la
[](https:*www.github.com/eim-lab/Laborator10).

În urma acestei operații, directorul Laborator10 va trebui să se conțină
directoarele `labtasks` și `solutions`.

    student@eg-106:~$ git clone https:*github.com/eim-lab/Laborator10.git

**4.** Să se încarce conținutul descărcat în cadrul depozitului
'Laborator10' de pe contul Github personal.
`student@eg-106:~$ cd Laborator10
student@eg-106:~/Laborator10$ git remote add Laborator10_perfectstudent https:*github.com/perfectstudent/Laborator10
student@eg-106:~/Laborator10$ git push Laborator10_perfectstudent master
`

**5.** Să se configureaze mașina pe care va rula aplicația:

-   în cazul în care se utilizează un emulator, se configurează astfel
    încât acesta să aibă instalat Google Play Services;
-   în cazul în care se utilizează un dispozitiv fizic, acesta trebuie
    să ruleze un sistem de operare Android cu o versiune ulterioară 2.2,
    având asociat un cont Google.

**6.** Să se importe în mediul integrat de dezvoltare Android Studio
proiectul `GoogleMapsPlaces` din directorul `labtasks`.

Se dorește să se implementeze o aplicație care să navigheze către o
locație specificată prin intermediul coordonatelor GPS (latitudine /
longitudine) și pentru care se dorește plasarea unui reper pe hartă,
însoțit de o denumire.

![](images/google_maps_places.png)

Reperele vor fi stocate în cadrul unei liste (obiect de tip `Spinner`),
astfel încât la selecția unui element din cadrul acesteia, se va
vizualiza obiectivul geografic marcat anterior.

Se cere să se implementeze funcționalitățile pentru adăugarea unui reper
și ștergerea tuturor reperelor de pe hartă:

**a)** pentru adăugarea unui reper:

1.  se obțin informațiile legate de latitudine, longitudine și denumire,
    din câmpurile text corespunzătoare și se verifică să fie completate
    (în caz contrar generându-se un mesaj de eroare);
2.  se realizează navigarea către locația respectivă;
3.  se instanțiază un obiect de tip `MarkerOptions`, desemnând reperul
    care va fi plasat pe harta Google;
    `MarkerOptions marker = new MarkerOptions()
      .position(new LatLng(
        Double.parseDouble(latitudeContent), 
        Double.parseDouble(longitudeContent)
      ))
      .title(nameContent);
    marker.icon(BitmapDescriptorFactory.defaultMarker(Utilities.getDefaultMarker(markerTypeSpinner.getSelectedItemPosition())));
    `
4.  se adaugă reperul pe harta Google;
5.  se adaugă reperul în lista de locații (`places`), notificându-se și
    adaptorul corespunzător obiectului de tip `Spinner`
    (`placesAdapter`) de această modificare, astfel încât acesta să fie
    actualizat corespunzător.

**b)** pentru ștergerea tuturor reperelor de pe hartă:

1.  se verifică să fie completate repere pe harta Google (în caz contrar
    generându-se un mesaj de eroare);
2.  se șterg toate reperele pe harta Google;
3.  se șterg toate reperele din lista de locații (`places`),
    notificându-se și adaptorul corespunzător obiectului de tip
    `Spinner` (`placesAdapter`) de această modificare, astfel încât
    acesta să fie actualizat corespunzător.

**7.** Să se importe în mediul integrat de dezvoltare Android Studio
proiectul `GoogleMapsLocationUpdate` din directorul `labtasks`.

Se dorește să se implementeze o aplicație pentru care să se implementeze
posibilitatea de actualizare periodică a poziției curente pe hartă, în
funcție de starea unui buton, prin care se controlează pornirea /
oprirea acestui serviciu.

1.  când serviciul este activat, se vizualizează pe hartă doar locația
    curentă, completându-se în mod automat informații precum latitudinea
    și longitudinea, actualizându-se corespunzător poziția;
2.  când serviciul este dezactivat, utilizatorul are posibilitatea de a
    controla poziția care se vizualizează pe hartă.

De asemenea, se dorește să se poată selecta tipul de hartă care să fie
afișat.

![](images/google_maps_location_update_01.png)

![](images/google_maps_location_update_02.png)

Se cere să se implementeze metodele pentru pornirea și oprirea
serviciului de actualizare periodică a locației de pe hartă:

**a)** metoda `startLocationUpdates()` din clasa `GoogleMapsActivity`:

1.  se apelează metoda `requestLocationUpdates()` din clasa
    `FusedLocationProviderApi`
    `LocationServices.FusedLocationApi.requestLocationUpdates(
      googleApiClient,
      locationRequest,
      this
    );
    `
2.  se actualizează starea serviciului de transmitere periodice a
    locației curente (`locationUpdatesStatus`);
3.  se vizualizează poziția curentă pe harta Google (se apelează metoda
    `setMyLocationEnabled(true)`);
4.  se modifică textul și culoarea butonului
    `locationUpdateStatusButton`;
5.  se navighează la locația curentă;
6.  se dezactivează controalele grafice `latitudeEditText`,
    `longitudeEditText`, `navigateToLocationButton`.

**b)** metoda `stopLocationUpdates()` din clasa `GoogleMapsActivity`

1.  se apelează metoda `removeLocationUpdates()` din clasa
    `FusedLocationProviderApi`
    `LocationServices.FusedLocationApi.removeLocationUpdates(
      googleApiClient,
      this
    );
    `
2.  se actualizează starea serviciului de transmitere periodice a
    locației curente (`locationUpdatesStatus`);
3.  nu se vizualizează poziția curentă pe harta Google (se apelează
    metoda `setMyLocationEnabled(false)`);
4.  se modifică textul și culoarea butonului
    `locationUpdateStatusButton`;
5.  se activează controalele grafice `latitudeEditText`,
    `longitudeEditText`, `navigateToLocationButton`, acestea având un
    conținut vid.

**8.** (opțional - necesită Billing pentru Geocoding API) \<spoiler> Să
se importe în mediul integrat de dezvoltare Android Studio proiectul
`GoogleMapsGeocoding` din directorul `labtasks`.

Se dorește să se implementeze o aplicație care să realizeze procesul de
codificare geografică inversă: dându-se un set de coordonate GPS, se
dorește să se determine adresa poștală corespunzătoare.

![](images/google_maps_geocoding.png)

Se cere să se implementeze procesul de conversie propriu-zis, în cadrul
serviciului `GetLocationAddressIntentService`, pe metoda
`onHandleIntent()`.

1.  se instanțiază un obiect de tip `Geocoder`
    `Geocoder geocoder = new Geocoder(this, Locale.getDefault());
    `
2.  se obține lista de adrese prin invocarea metodei `getFromLocation()`
    care primește ca parametri:
    1.  latitudinea;
    2.  longitudinea;
    3.  numărul de adrese întoarse (`Constants.NUMBER_OF_ADDRESSES`);
3.  se tratează corespunzător tipurile de execepții ce pot fi generate
    (`IOException`, `IllegalArgumentException`) precum și situația în
    care nu este furnizat nici un rezultat;
4.  se parcurge lista de adrese: pentru fiecare adresă în parte se
    concatenează rândurile distincte, concatenându-se toate rezultatele
    obținute;
    1.  numărul de linii dintr-o adresă este furnizat de metoda
        `getMaxAddressLineIndex()`;
    2.  un rând de la o anumită poziție se obține prin intermediul
        metodei `getAddressLine()`;
5.  se transmite rezultatul către activitatea principală (se apelează
    metoda `handleResult()` cu codul numeric de rezultat
    (`Constants.RESULT_SUCCESS`, `Constants.RESULT_FAILURE`) și
    rezultatul obținut, respectiv mesajul de eroare, după caz.

\</spoiler>

**9.** Să se importe în mediul integrat de dezvoltare Android Studio
proiectul `GoogleMapsGeofencing` din directorul `labtasks`.

Se dorește să se implementeze o aplicație care să monitorizeze
activitatea unui dispozitiv mobil raportat la o zonă de restricție
geografică.

Serviciul referitor la monitorizarea unei anumite locații poate fi
activat sau dezactivat, specificându-se de fiecare dată coordonatele
zonei față de care sunt realizate comparațiile.

Aplicația va afișa pe hartă în permanență locația curentă prin
actualizările periodice care sunt transmise.

![](images/google_maps_geofencing_01.png)

Notificările vor fi generate:

1.  când utilizatorul intră în zona de restricție geografică  
      
    <img src="/eim/laboratoare/laborator10/google_maps_geofencing_02.png" width="300" alt="google_maps_geofencing_02.png" />
    <img src="/eim/laboratoare/laborator10/google_maps_geofencing_03.png" width="300" alt="google_maps_geofencing_03.png" />
2.  când utilizatorul iese din zona de restricție geografică  
      
    <img src="/eim/laboratoare/laborator10/google_maps_geofencing_04.png" width="300" alt="google_maps_geofencing_04.png" />
    <img src="/eim/laboratoare/laborator10/google_maps_geofencing_05.png" width="300" alt="google_maps_geofencing_05.png" />

Detaliile cu privire la evenimentul produs vor putea fi vizualizate în
cadrul unei activități dedicate.

Se cere să se analizeze evenimentul legat de zona de restricție
geografică în cadrul serviciului `GeofenceTrackerIntentService`, pe
metoda `onHandleIntent()`.

1.  se obține evenimentul legat de zona de restricție geografică, din
    cadrul intenției cu care a fost lansat în execuție serviciul
    `GeofencingEvent geofencingEvent = GeofencingEvent.fromIntent(intent);
    `
2.  se verifică dacă evenimentul legat de zona de restricție geografică
    conține vreo eroare (prin apelul metodei `hasError()`), aceasta
    fiind tratată corespunzător (se jurnalizează eroarea și metoda se
    termină):
    1.  `GeofenceStatusCodes.GEOFENCE_NOT_AVAILABLE`
    2.  `GeofenceStatusCodes.GEOFENCE_TOO_MANY_GEOFENCES`
    3.  `GeofenceStatusCodes.GEOFENCE_TOO_MANY_PENDING_INTENTS`.
3.  se obține tipul de tranziție geografică
    `int geofenceTransition = geofencingEvent.getGeofenceTransition();
    `
4.  se construiește un mesaj explicativ conținând
    1.  tipul tranziției: `Geofence.GEOFENCE_TRANSITION_ENTER` /
        `Geofence.GEOFENCE_TRANSITION_EXIT`;
    2.  identificatorii restricțiilor legate de poziționarea geografică:
        1.  se obține lista tuturor restricțiilor legate de poziționarea
            geografică
            `List<Geofence> triggeringGeofences = geofencingEvent.getTriggeringGeofences();
            `
        2.  se parcurge lista și pentru fiecare obiect se obține
            identificatorul unic (`getRequestId()`);
5.  se transmite mesajul explicativ prin intermediul unei notificări (ca
    parametru al metodei `sendNotification()`).

**10.** Să se încarce modificările realizate în cadrul depozitului
'Laborator10' de pe contul Github personal, folosind un mesaj sugestiv.
`student@eg-106:~/Laborator10$ git add *
student@eg-106:~/Laborator10$ git commit -m "implemented taks for laboratory 10"
student@eg-106:~/Laborator10$ git push Laborator10_perfectstudent master
`

## Resurse Utile

[Location &
Places](http:*developer.android.com/google/play-services/location.html)  
[Google Maps Android API
v2](https:*developers.google.com/maps/documentation/android/)  
[Tutorial: Making your Application
Location-Aware](http:*developer.android.com/training/location/index.html)  
[Wei Meng LEE, Beginning Android 4 Application Development, Wiley,
2012](http:*eu.wiley.com/WileyCDA/WileyTitle/productCd-1118199545.html) -
capitolul 9, *Location-Based Services*  
[Reto MEIER, Professional Android for Application Development, John
Wiley & Sons,
2012](http:*www.amazon.com/Professional-Android-4-Application-Development/dp/1118102274) -
capitolul 13 *Maps, Geocoding and Location-Based Services*  
[Satya KOMATINENI, Dave MACLEAN, Pro Android 4, Apress,
2012](http:*www.apress.com/9781430239307) - capitolul 22, *Exploring
Maps and Location-based Services*  
[Ronan SCHWARZ, Phil DUTSON, James STEELE, Nelson TO, Android
Developer's Cookbook, Building Applications with the Android SDK, 2nd
Edition, Addison Wesley,
2013](http:*books.google.ro/books/about/The_Android_Developer_s_Cookbook.html?id=Y4JR2yI2Fo0C&redir_esc=y) -
capitolul 12, *Location-Based Services*  
[Bill PHILLIPS, Brian HARDY, Android Programming. The Big Nerd Ranch
Guide, Pearson Technology Group,
2013](http:*www.bignerdranch.com/we-write/android-programming/) -
capitolul 33, *Tracking the Device's Location*  
[Package
com.google.android.gms.location](http:*developer.android.com/reference/com/google/android/gms/location/package-summary.html)  
[Android Working with Google Maps
v2](http:*www.androidhive.info/2013/08/android-working-with-google-maps-v2/)  
[Android Get Address with Street Name, City for Location with
Geocoding](http:*javapapers.com/android/android-get-address-with-street-name-city-for-location-with-geocoding/)  
[Setting up Google Play Services in Android
Studio](https:*developers.google.com/android/guides/setup#add_google_play_services_to_your_project)
