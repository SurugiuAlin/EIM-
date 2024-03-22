# Tipuri de Servicii

În programarea Android, există două tipuri de servicii:

1.  servicii **pornite explicit** (*eng.* started), lansate în execuție
    prin intermediul metodei
    [startService()](http:*developer.android.com/reference/android/content/Context.html#startService%28android.content.Intent%29),
    invocată din contextul unei componente (activitate, serviciu,
    ascultător al unor mesaje cu difuzare); astfel de servicii nu
    furnizează un rezultat (către componenta care l-a apelat), fiind
    utilizate pentru a realiza o anumită operație la finalizarea căreia,
    de regulă, sunt terminate (apelându-se, în rutina lor, metoda
    [stopSelf()](http:*developer.android.com/reference/android/app/Service.html#stopSelf%28int%29));
    există posibilitatea ca o altă componentă să îl oprească explicit
    prin metoda
    [stopService()](http:*developer.android.com/reference/android/content/Context.html#stopService%28android.content.Intent%29);
    **un serviciu de tip started continuă să ruleze chiar și în situația
    în care componenta care l-a invocat nu mai există**;
2.  servicii **atașate unei (unor) componente** (*eng.* bounded) sunt
    lansate în execuție prin intermediul metodei
    [bindService()](http:*developer.android.com/reference/android/content/Context.html#bindService%28android.content.Intent,%20android.content.ServiceConnection,%20int%29),
    invocată din contextul unei componente (activitate, serviciu,
    ascultător al unor mesaje cu difuzare) care interacționează cu
    acesta prin funcționalități pe care le expune; la un moment dat, pot
    exista mai multe componente atașate aceluiași serviciu; detașarea
    unei componente la un serviciu se realizează prin intermediul
    metodei
    [unbindService()](http:*developer.android.com/reference/android/content/Context.html#unbindService%28android.content.ServiceConnection%29);
    **atunci când nu mai există nici o componentă asociată serviciului,
    acesta se consideră încheiat**.

Un serviciu poate avea, în același timp, ambele tipuri (started și
bounded). Acesta va putea rula o perioadă de timp nedefinită (până în
momentul în care procesarea pe care o realizează este încheiată),
permițând totodată componentelor unei aplicații Android să
interacționeze cu el prin intermediul unor metode pe care le expune.

Indiferent de modul în care este folosit un serviciu, invocarea sa este
realizată, ca pentru orice componentă Android, prin intermediul unei
intenții. În cazul serviciilor, se preferă să se utilizeze intenții
explicite, în detrimentul intențiilor implicite, din motive de
securitate.

Categoria în care se încadrează un anumit serviciu este determinată de
metodele pe care acesta le implementează:

1.  pentru un serviciu de tip started, va fi implementată metoda
    [onStartCommand()](http:*developer.android.com/reference/android/app/Service.html#onStartCommand%28android.content.Intent,%20int,%20int%29),
    apelată în mod automat în momentul în care serviciul este pornit
    prin intermediul metodei `startService()`;
2.  pentru un serviciu de tip bounded, vor fi implementate metodele:
    -   [onBind()](http:*developer.android.com/reference/android/app/Service.html#onBind%28android.content.Intent%29),
        apelată în mod automat în momentul în care o componentă este
        atașată serviciului, prin intermediul metodei `bindService()`;
    -   [onUnbind()](http:*developer.android.com/reference/android/app/Service.html#onUnbind%28android.content.Intent%29),
        apelată în mod automat în momentul în care o componentă este
        detașată de la serviciu, prin intermediul metodei
        `unbindService()`.