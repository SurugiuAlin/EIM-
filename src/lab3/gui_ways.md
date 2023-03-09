## Mecanisme pentru construirea unei interfețe grafice

O interfață grafică poate fi construită în două moduri:

1.  prin definirea elementelor componente și a modului lor de dispunere
    în cadrul unui fișier .xml, asociat fiecarei activități (sau
    fragment) în parte, situație adecvată cazurilor în care interfața
    grafică este statică;
2.  programatic, prin instanțierea unor obiecte de tipul elementelor
    componente direct în codul sursă (cu stabilirea proprietăților
    respective) al activității (sau fragmentului), abordare potrivită
    pentru situațiile în care interfața grafică are o structură dinamică
    (este actualizată în funcție de unele condiții specifice
    identificate în momentul execuției).

De regulă, se preferă ca interfața grafică să fie definită în cadrul
unui fișier `.xml` pentru fiecare fereastră din cadrul aplicației
Android, întrucât acesta este mult mai ușor de întreținut, separând
sarcinile ce țin de proiectare propriu-zisă de cele care țin de
programare (putând fi realizate astfel de persoane diferite). Totuși,
pentru situațiile în care interfața grafică nu este cunoscută la
momentul compilării sau pentru cazul în care interfața grafică trebuie
modificată în funcție de anumite condiții identificate în momentul
compilării, pot fi utilizate metode programatice spre a obține o astfel
de funcționalitate.
