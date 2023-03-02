### Activitatea

Activitatea reprezintă o componenta a aplicației Android ce oferă o
interfață grafică cu care utilizatorul poate să interacționeze. Cele mai
multe activități ocupă întreaga suprafață de afișare, însă acest lucru
nu este obligatoriu.

O aplicație Android este formată din una sau mai multe activități (slab
cuplate între ele). Există întotdeauna o activitate principală care este
afișată atunci când aplicația Android este lansată în execuție inițial.

O activitate poate invoca o altă activitate pentru a realiza diferite
sarcini, prin intermediul unei intenții. În acest moment, activitatea
veche este oprită și salvată pe stivă (*eng.* back stack), după care
este pornită activitatea nouă. Restaurarea și (re)începerea activității
vechi este realizată în momentul în care activitatea nouă (curentă) este
terminată. Un comportament similar are loc în momentul în care se
produce un eveniment (primirea unui apel telefonic, apăsarea tastelor
*Home* sau *Back*, lansarea altei aplicații).

---
**Note**

O activitate trebuie să își gestioneze corespunzător
comportamentul (inclusiv folosirea memoriei) în cazul producerii
diferitelor evenimente, salvând și restaurând starea de fiecare dată
când aplicația este oprită, respectiv (re)pornită.\

---