#### Gradle

Android Studio folosește un mecanism automat pentru construirea
aplicației Android, denumit **Gradle**, responsabil cu aducerea
bibliotecilor referite de pe un depozit la distanță, cu definirea
proprietăților aplicației Android, cu compilarea și împachetarea tuturor
resurselor folosite, pentru rularea și instalarea aplicației astfel
rezultate.

Regulile pentru construiea aplicației Android sunt precizate în fișiere
`build.gradle`, care se definesc pentru fiecare modul și proiect
constituent.

Un fișier de configurare Gradle pentru o aplicație Android conține de
regulă două secțiuni:

-   `android` - conține proprietățile aplicației Android
    -   `compileSdkVersion` - reprezintă versiunea de SDK care va fi
        utilizată pentru compilarea proiectului Android
    -   `buildToolsVersion` - reprezintă versiunea de Android SDK Build
        Tools folosită pentru construirea fișierului care va fi instalat
        pe dispozitivul mobil
    -   defaultConfig - conține diferite configurări
        -   `applicationId` - pachetul care identifică **în mod unic**
            aplicația Android
        -   `midSdkVersion` - platforma minimă pe care se garantează că
            aplicația Android va rula; astfel, se vor folosi numai
            funcționalități definite la acest nivel sau funcționalități
            definite în API-uri superioare, dar care sunt disponibile la
            nivelul bibliotecilor de suport;
        -   `targetSdkVersion` - platforma maximă la care se garantează
            că aplicația Android va rula (de regulă, este versiunea cea
            mai recentă și este aceeași versiune folosită pentru
            compilarea codului sursă);
        -   `versionCode` - versiunea curentă a aplicației (număr
            întreg)
        -   `versionName` - versiunea curentă a aplicației, afișată
            către utilizator (format lizibil, de tip șir de caractere)
        -   `testInstrumentationRunner` - biblioteca folosită pentru
            testele aplicației Android
-   `dependencies` - reprezintă bibliotecile de care depinde aplicația
    Android pentru a putea fi compilată / rulată, precum și reguli de
    compilare
    -   `compile` - se precizează care fișiere sunt luate în considerare
        pentru classpath
        -   directiva `include` se folosește pentru a indica tipuri de
            fișiere care conțin diverse biblioteci);
        -   directiva `fileTree` este utilizată pentru a indica o
            structura de directoare
    -   `testCompile` și `androidTestCompile` - indică pachete care
        conțin biblioteci pentru teste unitare.

``` .gradle
apply plugin: 'com.android.application'

android {
    compileSdkVersion 25
    buildToolsVersion "25.0.2"
    defaultConfig {
        applicationId "ro.pub.systems.eim.lab02.activitylifecyclemonitor"
        minSdkVersion 16
        targetSdkVersion 25
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner "android.support.test.runner.AndroidJUnitRunner"
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
}
dependencies {
    compile fileTree(dir: 'libs', include: ['*.jar'])
    compile 'com.android.support:appcompat-v7:25.2.0'
}
```