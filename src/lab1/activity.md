# Activitate de Laborator 

- Să se instaleze toate instrumentele necesare pentru a putea dezvolta o aplicație Android.
  - kit de dezvoltare pentru limbajul de programare Java (JDK)
  - Android Studio (include Android SDK + AVD))
  - emulator Genymotion în care se configurează un dispozitiv virtual Phone - 7.0 - API 24 - 960x540;

- Să se acceseze [GitHub](http://www.github.com) și să se creeze un cont.

- Să se realizeze configurațiile globale, specificând informații precum **user.name**, **user.email**
   ```Bash
   student@eim-lab:~$ git config --global user.name "Perfect Student"
   student@eim-lab:~$ git config --global user.email "perfect_student@cti.pub.ro"
   ```

- Să se creeze un repo pe contul Github creat, denumit 'Laborator01'. Inițial, acesta trebuie să fie gol (nu trebuie să bifați nici adăugarea unui fișier **README.md**, nici a fișierului **.gitignore** sau a a fișierului **LICENSE**).

- Să se cloneze în directorul de pe discul local conținutul depozitului la
distanță de la
[www.github.com/eim-lab/Laborator01](https://www.github.com/eim-lab/Laborator01).
În urma acestei operații, directorul Laborator01 va trebui să se conțină un
director **labtaks** care conține proiectele AndroidStudio denumite
**MyFirstAndroidApplication**, fișierele **README.md** și **LICENSE** și un
fișier **.gitignore** care indică tipurile de fișiere (extensiile) ignorate.
student@eim-lab:~$ git clone
[https://www.github.com/eim-lab/Laborator01.git](https://www.github.com/eim-lab/Laborator01.git)

- Să se încarce conținutul descărcat în cadrul depozitului 'Laborator01' de pe contul Github personal.
  ```Bash
  student@eim-lab:~$ cd Laborator01
  student@eim-lab:~/Laborator01$ git remote add my_origin https://github.com/perfectstudent/Laborator01
  student@eim-lab:~/Laborator01$ git push my_origin master
  ```

- Să se ruleze aplicația schelet:
  - în Android Studio: *Open an existing Android Studio project* și se indică directorul Laborator01/labtasks/androidstudio;
  
- În fișierul **MainActivity.java** din pachetul **ro.pub.cs.systems.eim.lab01**
(directorul **src**), să se modifice metoda **onClick** a clasei interne
**ButtonClickListener** astfel încât:

  - mesajul afișat să includă numele utilizatorului, așa cum apare în widget-ul de tip **EditBox**;

       ```java
       greetingTextView.setText(greetingTextView.getText().toString().replace("xxx", "\n"+userNameEditText.getText()));
       ```
  - să se aplice un efect de fade, astfel încât mesajul afișat să dispară treptat în decurs de **TRANSPARENCY_EFFECT_DURATION** milisecunde.

      ```java
      AlphaAnimation fadeEffect = new AlphaAnimation(1.0f, 0.0f);
      fadeEffect.setDuration(TRANSPARENCY_EFFECT_DURATION);
      fadeEffect.setFillAfter(true);
      greetingTextView.setAnimation(fadeEffect);
      ```

- Să se încarce modificările realizate în cadrul depozitului 'Laborator01' de pe contul Github personal, folosind un mesaj sugestiv.

   ```bash
   student@eim-lab:~/Laborator01$ git add MyFirstAndroidApplication/src/ro/pub/cs/systems/eim/lab01.MainActivity.java
   student@eim-lab:~/Laborator01$ git commit -m "implemented functionality for customized message and fade effect"
   student@eim-lab:~/Laborator01$ git push my_origin master
   ```

- Să se ruleze un exemplu de proiect Android, dintre cele disponibile, folosind dispozivitul virtual instalat în cadrul emulatorului Genymotion. Să se simuleze un eveniment de tipul rotirea ecranului și să se observe modul în care se comportă aplicația.

- în Android Studio, **AccelerometerPlay** , din cadrul categoriei *Getting Started*. (sau [AccelerometerPlay](https://github.com/googlearchive/android-AccelerometerPlay)
