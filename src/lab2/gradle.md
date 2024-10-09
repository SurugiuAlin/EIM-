# Gradle

Sistemul de build compilează resursele aplicației și codul sursă și le împachetează în **Android Application Package (APK)** (formatul de distribuire al aplicatilor Android) sau Android App Bundles (AAB) pe care le poți testa, desfășura, semna și distribui. Pentru a realiza acest lucru, in ecosistemul Android se folosește Gradle.

Gradle este un sistem open-source de automatizare a build-urilor. Acesta are avantajul unui DSL bazat pe Groovy sau Kotlin și beneficiile Ant și Maven. Cu Gradle, poți manipula cu ușurință procesul de build și logica acestuia pentru a crea mai multe versiuni ale aplicației tale. Este mult mai ușor de utilizat și mult mai concis și flexibil în comparație cu Ant sau Maven folosite individual.

Regulile pentru construiea aplicației Android sunt precizate în fișiere
`build.gradle`, care se definesc pentru fiecare **modul** și **proiect**
constituent.

Un fișier de configurare Gradle pentru o aplicație Android conține de
regulă două secțiuni:

-   `android` - conține proprietățile aplicației Android
    -   `compileSdkVersion` - reprezintă versiunea de SDK care va fi
        utilizată pentru compilarea proiectului Android
    -   `defaultConfig` - conține diferite configurări
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

```
apply plugin: 'com.android.application'

android {
    compileSdkVersion 33
    defaultConfig {
        applicationId "ro.pub.systems.eim.lab02.activitylifecyclemonitor"
        minSdkVersion 24
        targetSdkVersion 33
        versionCode 1
        versionName "1.0"
        testInstrumentationRunner 'androidx.test.runner.AndroidJUnitRunner'
    }
    buildTypes {
        release {
            minifyEnabled false
            proguardFiles getDefaultProguardFile('proguard-android.txt'), 'proguard-rules.pro'
        }
    }
    compileOptions {
        sourceCompatibility JavaVersion.VERSION_1_8
        targetCompatibility JavaVersion.VERSION_1_8
    }
}

dependencies {
    implementation fileTree(dir: 'libs', include: ['*.jar'])
    implementation 'androidx.appcompat:appcompat:1.6.1'
}
```
