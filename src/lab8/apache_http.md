# Apache HTTP Components

[Apache HTTP Components](https://hc.apache.org/) este un proiect
open-source, dezvoltat sub licență Apache, punând la dispoziția
utilizatorilor o bibliotecă Java pentru accesarea de resurse prin
intermediul protocolului HTTP. Funcționalitatea poate fi utilizată în
cadrul oricărei mașini virtuale Java și era inclusă și în platforma
Android până în API Level 23 (Marshmellow) [când a fost
exclusă](http:*developer.android.com/about/versions/marshmallow/android-6.0-changes.html#behavior-apache-http-client),
fiind invocate probleme legate de compatibilitate pentru anumite
platforme precum și utilizarea excesivă a rețelei cu impact asupra
consumului de energie. În schimb, se recomandă utilizarea clasei
HttpURLConnection care asigură compresia datelor (în mod transparent
pentru utilizator!) precum și folosirea unui cache. Cu toate acestea,
proiectul Apache HTTP Components este în continuă dezvoltare și folosit
pe scară largă.

Componentele Apache HTTP Components sunt:

-   [HttpCore](https://hc.apache.org/httpcomponents-core-ga/index.html)
    este un set de componente de transport care pot fi utilizate pentru
    dezvoltarea de servicii robuste, la nivel de server și client; sunt
    implementate atât un model blocant pentru operații de intrare/ieșire
    (bazat pe `java.io`) cât și un model asincron, bazat pe evenimente
    (bazat pe `java.nio`);
-   [HttpClient](https:*hc.apache.org/httpcomponents-client-ga/index.html)
    este o implementare a unui agent compatibil cu HTTP/1.1 care oferă
    funcționalități pentru autentificare la nivel de client, pentru
    gestiunea stării și a conexiunii;
-   [HttpAsyncClient](https:*hc.apache.org/httpcomponents-asyncclient-dev/index.html)
    este un modul complementar destinat situațiilor în care se dorește
    să se ofere suport pentru un număr mare de conexiuni concurente,
    parametrii precum nivelul de transfer al datelor nu sunt foarte
    importante.

Pentru ca metodele din API-ul Apache HTTP Components să poată fi
utilizate într-o aplicație Android ce utilizează API Level este necesar
să se specifice utilizarea bibliotecii corespunzătoare, în fișierul
`build.gradle`:

``` gradle
...

android {
  compileSdkVersion 23
  buildToolsVersion "23.0.2"

  useLibrary 'org.apache.http.legacy'
}

...
```


**GET**. Urmatorul exemplu prezinta o cere simpla de tip GET.

``` java
try {
  HttpClient httpClient = new DefaultHttpClient();
  HttpGet httpGet = new HttpGet("http:*www.server.com");
  HttpResponse httpGetResponse = httpClient.execute(httpGet);
  HttpEntity httpGetEntity = httpGetResponse.getEntity();
  if (httpGetEntity != null) {  
    /* do something with the response */
    Log.i(Constants.TAG, EntityUtils.toString(httpGetEntity));
  }            
} catch (Exception exception) {
  Log.e(Constants.TAG, exception.getMessage());
  if (Constants.DEBUG) {
    exception.printStackTrace();
  }
}
```

Alternativ, poate fi utilizat un obiect de tip
[ResponseHandler](https:*hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/client/ResponseHandler.html)
(cu implementarea
[BasicResponseHandler](https:*hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/impl/client/BasicResponseHandler.html))
care va fi transmis ca parametru metodei `execute()`, astfel încât
rezultatul acesteia să fie un șir de caractere conținând resursa care se
dorește a fi descărcată.

``` java
* ...
ResponseHandler<String> responseHandler = new BasicResponseHandler();
String content = httpClient.execute(httpGet, responseHandler);
* ...
```

În situația în care se dorește transmiterea de parametri către serverul
web, aceștia trebuie incluși în URL (în clar), fără a se depăși limita
de 2048 de caractere și folosind numai caractere ASCII:

``` java
HttpGet httpGet = new HttpGet("http:*www.server.com?attribute1=value1&...&attributen=valuen");
```

**POST**. Urmatorul exemplu prezinta o cere simpla de tip POST.

``` java
try {
  HttpClient httpClient = new DefaultHttpClient();        
  HttpPost httpPost = new HttpPost("http://www.server.com");
  /* Lista de perechi tip (atribut, valoare) care vor contine
     informatiile transmise de client pe baza carora serverul
     va genera continutul, de exemplu (user, eim), (parola, 123)
  */  
  List<NameValuePair> params = new ArrayList<NameValuePair>();        
  params.add(new BasicNameValuePair("attribute1", "value1"));
  * ...
  params.add(new BasicNameValuePair("attributen", "valuen"));

  UrlEncodedFormEntity urlEncodedFormEntity = new UrlEncodedFormEntity(params, HTTP.UTF_8);
  httpPost.setEntity(urlEncodedFormEntity);
             
  HttpResponse httpPostResponse = httpClient.execute(httpPost);  
  HttpEntity httpPostEntity = httpPostResponse.getEntity();  
  if (httpPostEntity != null) {
    * do something with the response
    Log.i(Constants.TAG, EntityUtils.toString(httpPostEntity));
   }
} catch (Exception exception) {
  Log.e(Constants.TAG, exception.getMessage());
  if (Constants.DEBUG) {
    exception.printStackTrace();
  }
}
```

**Prelucrarea raspunsurilor**. Prelucrarea unui răspuns HTTP se poate realiza:

-   prin prelucrarea obiectului de tip
    [HttpEntity](https:*hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/client/entity/UrlEncodedFormEntity.html),
    utilizând fluxuri de intrare/ieșire:  
    ```java
    BufferedReader bufferedReader = null;
    StringBuilder result = new StringBuilder();
    try {
      * ...
      bufferedReader = new BufferedReader(new InputStreamReader(httpEntity.getContent()));
      int currentLineNumber = 0;
      String currentLineContent;
      while ((currentLineContent = bufferedReader.readLine()) != null) {
        currentLineNumber++;
        result.append(currentLineNumber).append(": ").append(currentLineContent).append("\n");
      }
      Log.i(Constants.TAG, result.toString());
    } catch (Exception exception) {
      Log.e(Constants.TAG, exception.getMessage());
      if (Constants.DEBUG) {
        exception.printStackTrace();
      }
    } finally {
      if(bufferedReader != null) {
        try {
          bufferedReader.close();
        } catch (IOException ioException) {
          Log.e(Constants.TAG, exception.getMessage());
          if (Constants.DEBUG) {
            ioException.printStackTrace();
          }
        }
      }
    }
    ```
-   utilizând un obiect de tip `ResponseHandler`, ce furnizează
    conținutul resursei solicitate, transmis ca parametru al metodei
    `execute()` a clasei `HttpClient` (pe lângă obiectul
    `HttpGet|HttpPost`)