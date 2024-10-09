# Broadcast Receiver

Un broadcast receiver este o componentă care permite sistemului să transmită
evenimente către aplicație în afara fluxului obișnuit al utilizatorului, astfel
încât aplicația să poată răspunde la anunțuri de broadcast la nivelul
întregului sistem. Este o forma de inter-process communication (IPC). Deoarece
broadcast receivers sunt un alt punct de intrare bine definit în aplicație,
sistemul poate transmite broadcast-uri chiar și către aplicații care nu rulează
în prezent.

De exemplu, o aplicație poate programa o alarmă pentru a posta o
notificare care să informeze utilizatorul despre un eveniment viitor. Deoarece
alarma este livrată unui BroadcastReceiver din aplicație, nu este necesar ca
aplicația să rămână în funcțiune până când alarma se declanșează.

Multe broadcast-uri provin din sistem, cum ar fi un broadcast care anunță că
ecranul este oprit, bateria este descărcată sau o fotografie a fost capturată.
De asemenea, aplicațiile pot iniția broadcast-uri, cum ar fi pentru a informa
alte aplicații că anumite date au fost descărcate pe dispozitiv și sunt
disponibile pentru a fi utilizate.
