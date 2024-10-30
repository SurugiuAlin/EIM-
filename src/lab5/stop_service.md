
# Oprirea unui Serviciu

Un serviciu poate fi oprit:

-   de către o componentă (aceeași care l-a pornit sau alta), printr-un
    apel al metodei `stopService()`, ce primește ca parametru un obiect
    de tip `Intent` care poate fi creat explicit sau implicit;

> Întrucât apelurile metodei `startService()` nu sunt
imbricate, invocarea metodei `stopService()` oprește numai serviciul
corespunzător (dacă se află în execuție).


-   chiar de el însuși, în momentul în care procesările pe care trebuie
    să le realizeze s-au terminat, printr-un apel al metodei
    `stopSelf()`, eliberând resursele pe care sistemul de operare le-ar
    fi folosit pentru a-l menține în execuție; metoda poate fi apelată:
    -   fără parametri, pentru a forța oprirea imediată;
    -   transmițând un parametru de tip întreg, reprezentând
        identificatorul instanței care rulează, pentru a se asigura
        faptul că procesarea a fost realizată pentru fiecare apel care a
        fost realizat; dacă între timp serviciul a mai fost invocat,
        identificatorul folosit nu va corespunde celui mai recent apel
        (transmis ca argument al metodei `onStartCommand()`) și metoda
        nu va avea nici un efect.

Pentru oprirea unui serviciu este suficient un singur apel al uneia
dintre metodele `stopSelf()` sau `stopService()`.
