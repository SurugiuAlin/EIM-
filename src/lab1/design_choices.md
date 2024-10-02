## Influențe asupra Design-ului Sistemului de Operare Mobil

Prin prisma constrangerilor aduse de catre hardware, sistemul de operare
Android a introdus o serie de optimizari fata de ce gasim pe desktops:

**Eficiența Energetică**:
   - Gestionarea agresivă a proceselor: Android suspendă sau termină rapid aplicațiile inactive pentru a conserva energia.
   - [Modul **Doze**](https://source.android.com/docs/core/power/platform_mgmt): Introdus pentru a limita procesele de fundal și accesul la rețea în timpul perioadelor de inactivitate ale dispozitivului.
   - Job Scheduler: Grupează sarcinile de fundal ale aplicațiilor pentru a optimiza utilizarea bateriei.

**Resurse Hardware Limitate**:
   - Componente software cu un set de functionalitati restranse: De exemplu, este folosita biblioteca standard de C [Bionic](https://android.googlesource.com/platform/bionic/) libc (spre deosebire de GLIBC) este optimizat pentru dispozitive încorporate.
   - Gestionarea eficientă a memoriei: Procesul Zygote permite partajarea memoriei între aplicații.
   - Compilarea Ahead of Time (AOT) a ART: Îmbunătățește performanța și reduce consumul de energie comparativ cu compilarea Just in Time (JIT).

**Mediul de stocare Flash**:
   - YAFFS2 și mai târziu F2FS: Concepute pentru memoria flash, luând în considerare uzura uniformă și operațiunile rapide de citire/scriere.
   - Lipsa memoriei swap, daca ai umplut memoria RAM, aplicatiile vor incepe sa fie inchise.

**Considerații de Conectivitate**:
   - Suport integrat pentru diverse tehnologii wireless (WiFi, Bluetooth, Celular).
   - Utilizarea eficientă a rețelei: Restricții pentru datele de fundal, mod de economisire a datelor.

**Interfața Utilizator**:
   - Design centrat pe touch: Componente UI optimizate pentru interacțiuni tactile.
   - Design responsiv: Asigurarea performanței fluide pe diverse dimensiuni și rezoluții de ecran.

**Securitate și Confidențialitate**:
   - Model de permisiuni: Control fin asupra accesului aplicațiilor la funcțiile dispozitivului și datele utilizatorului.
   - Izolarea datelor aplicațiilor: Fiecare aplicație rulează în propriul sandbox pentru securitate și gestionarea ușoară a datelor.
   - Procese de pornire securizată și pornire verificată, e.g. [Titan](https://blog.google/products/pixel/titan-m-makes-pixel-3-our-most-secure-phone-yet/)

**Mecanism de Actualizare**:
   - Actualizări de sistem bazate pe partiții: Permite actualizări OS fără a afecta datele utilizatorului.
   - Google Play Services: Permite actualizări ale funcționalităților de bază fără upgrade-uri complete ale OS-ului.

**Integrarea Senzorilor**:
   - API-uri bogate pentru diverși senzori (accelerometru, giroscop, GPS) comuni în dispozitivele mobile.
   - Procesarea eficientă a datelor senzorilor pentru a echilibra colectarea informațiilor și consumul de energie.
