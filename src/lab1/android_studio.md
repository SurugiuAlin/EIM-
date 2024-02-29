### Crearea unei aplicații Android în Android Studio 

In cadrul laboratoarelor vom folosi Android Studio. Android Studio este un IDE de Java/Kotlin bazat pe IntelliJ special modificat pentru dezvoltarea aplicatilor Android. [Aici](https://developer.android.com/studio/install) gasiti instructiunile de instalare si un link de download. 


> In timpul instalarii Android Studio, vom instala si Software Development Kit-ul (SDK) de Android. Va trebui sa spelectati optiunea de a instala Android SDK din timpul instalarii.


#### Crearea unui proiect nou
1. Deschideți Android Studio.
2. În dialogul Welcome to Android Studio, faceți clic pe **Start a new Android Studio project**.

<img src="https://developer.android.com/static/codelabs/build-your-first-android-app/img/c7c8a5cc4c9029b_1440.png" alt="" style="height: 800px; width:800px;"/>

3. Selectați Activitate de bază (nu implicit). Faceți clic pe Next.


<img src="https://developer.android.com/static/codelabs/build-your-first-android-app/img/73e63b490a2f4ae6_1440.png" alt="" style="height: 800px; width:800px;"/>

4. Denumiți-vă aplicația cu un nume precum My First app


<img src="https://developer.android.com/static/codelabs/build-your-first-android-app/img/3ffb3ca42472b4f6_1440.png" alt="" style="height: 800px; width:800px;"/>

5. Asigurați-vă că Languages este setată la Java.

6. Apasati Finish


După acești pași, Android Studio va face urmatoarele lucruri:
* Creează un dosar pentru proiectul dvs. Android Studio numit MyFirstApp. Acesta se află de obicei într-un dosar numit AndroidStudioProjects sub directorul dvs. principal.
* Construiește proiectul (acest lucru poate dura câteva momente). Android Studio folosește **Gradle** ca sistem de build. Puteți urmări progresul build-ului în partea de jos a ferestrei Android Studio.


### Structura proiectului

<img src="https://developer.android.com/static/codelabs/build-your-first-android-app/img/ecabcf48b6f7b9a1_1440.png" alt="" style="height: 800px; width:800px;"/>

Pe baza selectării de către tine a **Basic Activity** pentru proiectul tău, Android Studio a configurat un număr de fișiere pentru tine. Poți privi ierarhia fișierelor pentru aplicația ta în multiple moduri, unul dintre acestea este în **Project view**. Project view îți arată fișierele și folderele structurate într-un mod convenabil pentru lucrul cu un proiect Android. (Aceasta nu corespunde întotdeauna cu ierarhia fișierelor! Pentru a vedea ierarhia fișierelor, alege Project files view făcând click pe (3).)

1. Dublu-click pe folderul **app (1)** pentru a extinde ierarhia fișierelor app. (Vezi (1) în captura de ecran.)
2. Dacă faci click pe **Project (2)**, poți ascunde sau afișa **Project view**. S-ar putea să fie necesar să selectezi **View > Tool Windows** pentru a vedea această opțiune.
3. Selecția curentă Project view (3) este **Project > Android**.

În **Project > Android** view vezi trei sau patru foldere la nivelul cel mai înalt sub folderul tău app: manifests, java, java (generated) și res. Este posibil să nu vezi java (generated) imediat.

1. Extinde folderul **manifests**.

Acest folder conține `AndroidManifest.xml`. Acest fișier descrie toate componentele aplicației tale Android și este citit de sistemul de rulare Android atunci când aplicația ta este executată. 2. Extinde folderul **java**. Toate fișierele tale în limbaj Java sunt organizate aici. Folderul java conține trei subfoldere:

**com.example.myfirstapp**: Acest folder conține fișierele sursă Java pentru aplicația ta.

**com.example.myfirstapp (androidTest)**: Acest folder este locul unde ai pune testele instrumentate, care sunt testele care rulează pe un dispozitiv Android. Începe cu un fișier de test schelet.

**com.example.myfirstapp (test)**: Acest folder este locul unde ai pune testele unitare. Testele unitare nu necesită un dispozitiv Android pentru a rula. Începe cu un fișier de test unitar schelet. 3. Extinde folderul res. Acest folder conține toate resursele pentru aplicația ta, inclusiv imagini, fișiere de layout, șiruri, icoane și stilizare. Include aceste subfoldere:

**drawable**: Toate imaginile aplicației tale vor fi stocate în acest folder.

**layout**: Acest folder conține fișierele de layout UI pentru activitățile tale. În prezent, aplicația ta are o activitate care are un fișier de layout numit activity_main.xml. De asemenea, conține content_main.xml, fragment_first.xml și fragment_second.xml.

**menu**: Acest folder conține fișiere XML care descriu orice meniuri din aplicația ta.

**mipmap**: Acest folder conține icoanele de lansare pentru aplicația ta.

**navigation**: Acest folder conține graficul de navigare, care îi spune Android Studio cum să navigheze între diferite părți ale aplicației tale.

**values**: Acest folder conține resurse, cum ar fi șiruri și culori, utilizate în aplicația ta.
