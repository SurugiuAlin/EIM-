## Prelucrare JSON (JavaScript Object Notation)

Unele servicii web folosesc [formatul
JSON](http://en.wikipedia.org/wiki/JSON) pentru transferul de date
întrucât, spre diferență de XML care implică numeroase informații
suplimentare, acesta optimizează cantitatea de date implicate. De
asemenea, este foarte ușor pentru un utilizator uman să prelucreze
informațiile reprezentate într-un astfel de format.

Acest mecanism de reprezentare a datelor a fost utilizat inițial în
JavaScript, unde acesta descria literali sau obiecte anonime, folosite o
singură dată (fără posibilitatea de a fi reutilizate), informațiile
fiind transmise prin intermediul unor șiruri de caractere. Ulterior, a
fost preliat pe scară largă.

În principiu, informațiile reprezentate în format JSON au structura unei
colecții de perechi de tip (cheie, valoare), fiecare dintre acestea
fiind grupate într-o listă de obiecte ordonate. Nu se folosesc denumiri
de etichete, utilizându-se doar caracterele `"`, `,`, `{`, `}`, `[` și
`]`.

``` json
[
  {
    "attribute1": "valuem1",
    "attribute2": "valuem2",
    ...,
    "attributen": "valuemn"
  }  
]
```
Există [numeroase servicii
web](http://www.programmableweb.com/category/all/apis?data_format=21173)
care își expun funcționalitatea prin intermediul unor documente JSON:

-   [Google](https://developers.google.com/custom-search/json-api/v1/overview?csw=1);
-   [Yahoo](https://developer.yahoo.com/);
-   [Geonames](http://www.geonames.org/export/web-services.html);
-   [Twitter](https://dev.twitter.com/);
-   [Flickr](https://www.flickr.com/services/api/).

În Android, prelucrarea documentelor reprezentate în format JSON este
realizată prin intermediul clasei
[JSONObject](http://developer.android.com/reference/org/json/JSONObject.html)
care a fost integrată parțial (cu unele funcționalități lipsă), fără a
se specifica clar versiunea care este utilizată.

Vom studia utilizarea API-ului in practica prin parsarea raspunsului JSON
intors de catre o aplicatie de cutremure, [Geonames
Earthquakes](http://api.geonames.org/earthquakesJSON).

Detaliile care se doresc a fi vizualizate pentru fiecare cutremur în
parte sunt:

-   așezarea geografică (latitudinea și longitudinea);
-   magnitudinea;
-   adâncimea la care a avut loc;
-   sursa informației;
-   data și ora la care s-a înregistrat.

Rezultatele sunt furnizate în următorul format:

``` json
{
  "earthquakes":[
                  {
                    "eqid":"c0001xgp",
                    "magnitude":8.8,
                    "lng":142.369,
                    "src":"us",
                    "datetime":"2011-03-11 04:46:23",
                    "depth":24.4,
                    "lat":38.322
                  },
                  {
                    "eqid":"c000905e",
                    "magnitude":8.6,
                    "lng":93.0632,
                    "src":"us",
                    "datetime":"2012-04-11 06:38:37",
                    "depth":22.9,
                    "lat":2.311
                  },
                  ...
                ]
}
```

Astfel, informațiile care trebuie preluate din rezultat sunt:

| atribut JSON | tip de date | detaliu                                     |
|--------------|-------------|---------------------------------------------|
| `lat`        | `double`    | latitudine                                  |
| `lng`        | `double`    | longitudine                                 |
| `magnitude`  | `double`    | magnitudinea                                |
| `depth`      | `double`    | adâncimea                                   |
| `src`        | `String`    | sursa informației                           |
| `datetime`   | `String`    | data și ora la care s-au înregistrat datele |

Dupa ce realizam un HTTP GET pentru a primi in format JSON datele, vom parsa
astfel:

```java
final ArrayList<EarthquakeInformation> earthquakeInformationList = new ArrayList<EarthquakeInformation>();
JSONObject result = new JSONObject(content);
JSONArray jsonArray = result.getJSONArray(Constants.EARTHQUAKES);
for (int k = 0; k < jsonArray.length(); k++) {
    JSONObject jsonObject = jsonArray.getJSONObject(k);
    earthquakeInformationList.add(new EarthquakeInformation(
    jsonObject.getDouble(Constants.LATITUDE),
    jsonObject.getDouble(Constants.LONGITUDE),
    jsonObject.getDouble(Constants.MAGNITUDE),
    jsonObject.getDouble(Constants.DEPTH),
    jsonObject.getString(Constants.SOURCE),
    jsonObject.getString(Constants.DATETIME)
    ));
}
```