# Activitatea

O activitate este punctul de intrare (entrypoint) pentru interacțiunea cu utilizatorul.
**Practic este fereastra pe care o vedem pe telefon.**
Aceasta reprezintă un singur ecran cu o interfață de utilizator. De exemplu, o
aplicație de email ar putea avea o *activitate* care arată o listă de emailuri noi,
o altă activity pentru a compune un email și o altă *activitate* pentru citirea
emailurilor. 

Deși activities lucrează împreună pentru a forma o experiență de
utilizare coerentă în aplicația de email, **fiecare activitate este independentă de
celelalte**. O aplicație diferită poate porni oricare dintre aceste activitati
dacă aplicația de email permite acest lucru. De exemplu, o aplicație de cameră
ar putea porni activity-ul din aplicația de email pentru compunerea unui nou
email pentru a permite utilizatorului să partajeze o fotografie. 

Pentru noi, o activitate va fi o subclas a clasei **Activity**. 
