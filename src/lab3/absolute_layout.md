### AbsoluteLayout

Într-o interfață grafică dezvoltată prin intermediul `AbsoluteLayout`,
poziția fiecărei componente trebuie specificată prin coordonatele sale
absolute, indicate prin intermediul proprietăților `layout_x` și
`layout_y`. De asemenea, dimensiunile acestora vor fi indicate prin
atributele `layout_width` și `layout_height`.

---
**Note**

Întrucât acest mecanism de poziționare nu scalează
corespunzător pentru dispozitive având alte rezoluții decât cea pentru
care a fost proiectată aplicația, utilizarea sa nu mai este recomandată
începând cu Android 1.5. Deși este încă suportat în versiunile curente,
există posibilitatea de a fi eliminat, astfel încât aplicațiile care îl
utilizează să nu mai ruleze pe dispozitivele implementând noile API. De
aceea, este bine ca acest tip de layout să fie evitat pe cât
posibil.\

---
