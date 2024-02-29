### Activity

**O activitate in android reprezinta o fereastra vizibila dintr-o aplicatie.**
O aplicație Android este formată din una sau mai multe activități (slab
cuplate între ele). Există întotdeauna o activitate principală care este
afișată atunci când aplicația Android este lansată în execuție inițial.

<img src="https://miro.medium.com/v2/resize:fit:640/format:webp/1*yd1E59p-wPXEgTOnYsyE-A.png" alt=""/>

O activitate poate invoca o altă activitate pentru a realiza diferite
sarcini, prin intermediul unui obiect de tip **intent**.

O activitate este formata din doua parti, partea de cod Java care
defineste ce se va intampla cand utilizatorul interactioneaza cu activitatea:

```java
 public class Activity extends ApplicationContext {
     ...
 }
```

Si un cod cod `xml` care este folosit pentru design-ul vizual al activitatii.
