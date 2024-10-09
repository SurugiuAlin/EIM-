# Content Provider

Un content provider gestionează un set partajat de date ale aplicației pe care
le puteți stoca în sistemul de fișiere, într-o bază de date SQLite, pe web sau
în orice altă locație de stocare persistentă la care aplicația poate
accesa. Prin intermediul content provider-ului, alte aplicații pot interoga sau
modifica datele, dacă content provider-ul permite acest lucru.

De exemplu, sistemul Android oferă un content provider care gestionează
informațiile de contact ale utilizatorului. Orice aplicație cu permisiunile
adecvate poate interoga content provider-ul, cum ar fi utilizarea
*ContactsContract.Data*, pentru a citi și scrie informații despre o anumită
persoană.

Pentru sistem, un content provider este un punct de intrare într-o aplicație
pentru publicarea elementelor de date numite, identificate printr-o schemă URI.
Astfel, o aplicație poate decide cum dorește să mapeze datele pe care le
conține la un spațiu de nume URI, oferind aceste URI-uri altor entități care le
pot utiliza la rândul lor pentru a accesa datele.
