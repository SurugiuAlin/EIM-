#### Coordonarea Activităților

\<spoiler> În situația în care o activitate nouă este pornită în timp ce
o activitate veche este în execuție, fiind necesară transmiterea de
informații dintre acestea, este util să se cunoască ordinea în care sunt
apelate metodele care gestionează ciclul de viață al celor două
activități, astfel încât comunicarea dintre acestea să se realizeze în
mod corect:

1.  se apelează metoda `onPause()` a activității vechi - aici trebuie
    realizată partea de scriere a informațiilor care trebuie să fie
    trimise;
2.  se apelează metodele `onCreate()`, `onStart()` și `onResume()` ale
    activității noi - aici trebuie realizată partea de citire a
    informațiilor care trebuie să fie primite;
3.  se apelează metoda `onStop()` a activității vechi;
4.  în situația în care necesarul de memorie nu este satisfăcut, este
    posibil să se apeleze metoda `onDestroy()` a activității vechi.

![](images/coordonare_activitati.png)
\</spoiler>

