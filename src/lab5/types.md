# Tipuri de Servicii

În programarea Android, există trei tipuri de servicii:

1. de tip **Foreground** - Un serviciu foreground efectuează operații care sunt vizibile pentru utilizator. De exemplu, o aplicație audio ar folosi un serviciu foreground pentru a reda o piesă audio. Serviciile foreground trebuie să afișeze o Notification. Serviciile foreground continuă să ruleze chiar și când utilizatorul nu interacționează cu aplicația.
Când folosești un serviciu foreground, trebuie să afișezi o notificare pentru ca utilizatorii să fie conștienți că serviciul rulează. Această notificare nu poate fi închisă decât dacă serviciul este oprit sau eliminat din foreground.
2. de tip **Background** - Un serviciu background efectuează o operație care nu este observată direct de utilizator. De exemplu, dacă o aplicație folosește un serviciu pentru a-și compacta spațiul de stocare, acesta ar fi de obicei un serviciu background.

3. de tip **Bound** - Un serviciu este bound când o componentă a aplicației se leagă de acesta prin apelarea bindService(). Un serviciu bound oferă o interfață client-server care permite componentelor să interacționeze cu serviciul, să trimită cereri, să primească rezultate și chiar să facă acest lucru între procese prin comunicare între procese (IPC). Un serviciu bound rulează doar atât timp cât o altă componentă a aplicației este legată de acesta. Mai multe componente se pot lega de serviciu simultan, dar când toate se dezleagă, serviciul este distrus.