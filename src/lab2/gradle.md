# Gradle

Sistemul de build compilează resursele aplicației și codul sursă și le împachetează în **Android Application Package (APK)** (formatul de distribuire al aplicatilor Android) sau Android App Bundles (AAB) pe care le poți testa, desfășura, semna și distribui. Pentru a realiza acest lucru, in ecosistemul Android se folosește Gradle.

Gradle este un sistem open-source de automatizare a build-urilor. Acesta are avantajul unui DSL bazat pe Groovy sau Kotlin și beneficiile Ant și Maven. Cu Gradle, poți manipula cu ușurință procesul de build și logica acestuia pentru a crea mai multe versiuni ale aplicației tale. Este mult mai ușor de utilizat și mult mai concis și flexibil în comparație cu Ant sau Maven folosite individual.

Regulile pentru construiea aplicației Android sunt precizate în fișiere
`build.gradle`, care se definesc pentru fiecare **modul** și **proiect**
constituent.

#### Project build.gradle
```json
// În blocul buildscript, definiți setările necesare pentru a construi proiectul.
buildscript {
    // În blocul repositories, adăugați numele depozitelor unde Gradle 
    // ar trebui să caute plugin-urile pe care le folosiți.
    repositories {
        google()
        mavenCentral()
    }
    // Blocul dependencies conține dependențele necesare pentru plugin-uri
    // în acest caz, plugin-urile Gradle și Kotlin. Nu puneți dependențele modulului
    // în acest bloc.
    dependencies {
        classpath "com.android.tools.build:gradle:8.2.2"
        classpath "org.jetbrains.kotlin:kotlin-gradle-plugin:1.9.20"
    }
}
// Structura blocului allprojects este similară cu cea a blocului buildscript,
// dar aici definiți depozitele pentru toate modulele voastre, nu pentru Gradle
// însuși. De obicei, nu definiți secțiunea dependencies pentru allprojects.
// Dependențele pentru fiecare modul sunt diferite și ar trebui să se afle în
// build.gradle la nivel de modul.
allprojects {
    repositories {
        google()
        mavenCentral()
    }
}
// Un task reprezintă o parte a muncii în procesul de construire. 
// Acesta curăță fișierele de build când este executat. 
tasks.register('clean', Delete) {
    delete rootProject.buildDir
}
```

#### Project build.gradle

```json
// Specifică o listă de plugin-uri necesare pentru a construi modulul. Plugin-ul
// com.android.application este necesar pentru a configura setările specifice
// Android ale procesului de build. Aici puteți folosi și com.android.library dacă
// creați un modul de bibliotecă. Plugin-ul kotlin-android vă permite să folosiți
// limbajul Kotlin în modulul vostru.
plugins {
    id "com.android.application"
    id "kotlin-android"
}

// În blocul android, plasați toate opțiunile specifice platformei pentru modul.
android {

    // Definirea unui namespace este necesară pentru lucruri precum accesul la
    // resurse. Aceasta se afla înainte în fișierul AndroidManifest.xml sub
    // proprietatea package, dar acum a fost mutată.
    namespace "com.kodeco.socializify"

    // Opțiunea compileSdk indică nivelul API cu care va fi compilată aplicația
    // voastră. Cu alte cuvinte, nu puteți folosi funcții dintr-un API mai înalt decât
    // această valoare. Aici, ați setat valoarea pentru a utiliza API-urile din
    // Android Tiramisu (Android 13). 
    compileSdk 34
 
    // Blocul defaultConfig conține opțiuni care vor fi aplicate implicit
    // tuturor versiunilor de build (de exemplu, debug, release, etc) ale aplicației
    defaultConfig {
        // applicationId este identificatorul aplicației voastre. Acesta ar trebui să fie
        // unic pentru a putea publica sau actualiza cu succes aplicația pe Google Play
        // Store. Dacă îl lăsați nedefinit, sistemul de build va folosi namespace ca
        // applicationId.
        applicationId "com.kodeco.socializify"

        // Pentru a seta cel mai scăzut nivel API suportat, folosiți minSdkVersion.
        // Aplicația voastră nu va fi disponibilă în Play Store pentru dispozitivele care
        // rulează pe niveluri API mai scăzute.
        minSdkVersion 23

        // Parametrul targetSdkVersion definește nivelul maxim API pe care aplicația
        // voastră a fost testată. Cu alte cuvinte, sunteți siguri că aplicația voastră
        // funcționează corect pe dispozitivele cu această versiune SDK și nu necesită
        // niciun comportament de compatibilitate înapoi. Cea mai bună abordare este să
        // testați temeinic o aplicație folosind cel mai recent API, păstrând valoarea
        // targetSdkVersion egală cu compileSdk.
        targetSdkVersion 34

        // versionCode este o valoare numerică pentru versiunea aplicației.
        versionCode 1
        // versionName este un șir de caractere ușor de înțeles pentru utilizatori, reprezentând versiunea aplicației.
        versionName "1.0"
    }
    // Blocul buildFeatures vă permite să activați anumite funcționalități, cum
    // ar fi View binding sau Compose. 
    buildFeatures {
        viewBinding true
    }
    // Gradle 8.2 suportă implicit JVM 17, deci forțați proiectul să folosească
    // Java 17 prin intermediul suportului pentru Java toolchain oferit de Gradle.
    kotlin {
        jvmToolchain(17)
    }
}
// Blocul dependencies conține toate dependențele necesare pentru acest modul.
dependencies {
    implementation fileTree(include: ["*.jar"], dir: "libs")
    implementation "androidx.appcompat:appcompat:1.6.1"
    implementation "com.google.android.material:material:1.9.0"
}
```
