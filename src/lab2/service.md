# Serviciul

Un service este un punct de intrare general pentru a menține o aplicație rulând
în fundal din diverse motive. Este o componentă care **rulează în fundal** pentru a
efectua operațiuni de lungă durată sau pentru a executa sarcini pentru procese
remote. 

> Un service nu oferă o interfață de utilizator. 

De exemplu, un service ar putea reda muzică în fundal în timp ce utilizatorul
se află într-o altă aplicație, sau ar putea prelua date prin rețea fără a bloca
interacțiunea utilizatorului cu o *activitate*. O altă componentă, cum ar fi o
*activitate*, poate porni service-ul și îl poate lăsa să ruleze sau se poate lega
de acesta pentru a interacționa cu el.

Pentru noi va fi o subclasa a **Service**.
