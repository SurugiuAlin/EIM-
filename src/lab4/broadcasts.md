# Broadcast

Deseori o sa fim nevoiti sa trimitem date fie de la o aplicatie la alta. Pentru
acest lucru vom folosi notiunea de `Broadcast`. Acestea reprexzinta o alta
forma de IPC.

Aplicațiile Android pot trimite sau primi mesaje de emisie de la sistemul Android și alte aplicații Android, 
similar cu modelul de proiectare publică-abonare. Aceste emisiuni sunt trimise atunci când are loc un eveniment 
de interes. De exemplu, sistemul Android trimite emisiuni când apar diverse evenimente de sistem, cum ar fi 
atunci când sistemul pornește sau dispozitivul începe să se încarce. Aplicațiile pot trimite, de asemenea, 
emisiuni personalizate, de exemplu, pentru a notifica alte aplicații despre ceva care ar putea fi de interes 
pentru ele (de exemplu, s-au descărcat date noi).

Sistemul optimizează livrarea emisiunilor pentru a menține sănătatea optimă a sistemului. Prin urmare, nu se 
garantează timpurile de livrare a emisiunilor. Aplicațiile care necesită comunicare între procese cu latență 
scăzută ar trebui să ia în considerare serviciile legate.

Aplicațiile se pot înregistra pentru a primi emisiuni specifice. Atunci când este trimisă o emisiune, sistemul rută automat emisiunile către aplicațiile care s-au abonat să primească acel tip particular de emisiune.

În general, emisiunile pot fi folosite ca un sistem de mesagerie între aplicații și în afara fluxului normal al 
utilizatorului. Cu toate acestea, trebuie să fii atent să nu abuzezi de oportunitatea de a răspunde la emisiuni 
și de a rula sarcini în fundal care pot contribui la o performanță lentă a sistemului.