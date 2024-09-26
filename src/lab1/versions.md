### Versiuni Android

Pentru identificarea versiunilor se folosesc, de regulă, trei sisteme:

- un număr, ce respectă formatul major.minor[.build], desemnând dacă
modificările aduse sunt substanțiale sau reprezintă ajustări ale unor probleme
identificate anterior; versiunea curentă este 10, lansată la sfârșitul anului
2019;
- un nivel de API (același putând grupa un număr de mai multe versiuni), prin
care se indică funcționalitățile expuse către programatori; versiunea curentă
are nivelul de API 29;
- o denumire, având un nume de cod inspirat din lumea dulciurilor; termenii
respectivi încep cu inițiale care respectă ordinea alfabetică; versiunea curentă
este Q.

În momentul în care se ia decizia cu privire la versiunea pentru care se
dezvoltă o aplicație Android, trebuie avute în vedere și cotele de piață ale
dispozitivelor mobile. Dezvoltarea unei aplicații Android pentru cea mai nouă
versiune are avantajul de a se putea utiliza cele mai noi funcționalități expuse
prin API. Dezvoltarea unei aplicații Android pentru cea mai veche versiune are
avantajul unei adresabilități pe scară largă. Un compromis în acest sens poate
fi obținut prin intermediul **bibliotecilor de suport**, dezvoltate pentru
fiecare versiune, prin intermediul cărora pot fi utilizate la niveluri de API
mai mici funcționalități din niveluri de API mai mari (în limita capabilităților
dispozitivului mobil respectiv). Utilizarea acestora reprezintă o practică
recomandată în dezvoltarea aplicațiilor Android.


<html>

<div id="main-table" class="table-responsive">
<table class="full-width">
  <tr>
    <th style="min-width: 6.5em">Version</th>
    <th>SDK / API level</th>
    <th><a href="https://developer.android.com/reference/kotlin/android/os/Build.VERSION_CODES">Version code</a></th>
    <th>Codename</th>
    <th>
      Cumulative<br>usage
      <sup id="fnref:1"><a href="#fn:1" class="footnote">1</a></sup>
    </th>
    <th>
      Year
      <sup id="fnref:4"><a href="#fn:4" class="footnote">4</a></sup>
    </th>
  </tr>
  <tr>
    <td>
      <b><a href="https://developer.android.com/about/versions/15">Android 15</a></b>
    </td>
    <td>Level 35</td>
    <td><code>VANILLA_ICE_CREAM</code></td>
    <td>
      Vanilla Ice Cream
      <sup id="fnref:2"><a href="#fn:2" class="footnote">2</a></sup>
    </td>
    <td>—</td>
    <td><i>TBD</i></td>
  </tr>
  <tr>
    <td rowspan="2">
      <b><a href="https://developer.android.com/about/versions/14">Android 14</a></b>
    </td>
    <td>Level 34</td>
    <td><code>UPSIDE_DOWN_CAKE</code></td>
    <td>
      Upside Down Cake
      <sup id="fnref:2"><a href="#fn:2" class="footnote">2</a></sup>
    </td> 
    <td> 30.9 %</td>
    <td rowspan="2">2023</td>
  </tr>
  <tr class="table-notes">
    <td colspan="3">
      <ul>
        <li><code>targetSdk</code> <a href="https://developer.android.com/google/play/requirements/target-sdk">will need to be 34+</a> for new apps and app updates by August 31, 2024.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td rowspan="2">
      <b><a href="https://developer.android.com/about/versions/13">Android 13</a></b>
    </td>
    <td>Level 33</td>
    <td><code>TIRAMISU</code></td>
    <td>
      Tiramisu
      <sup id="fnref:2"><a href="#fn:2" class="footnote">2</a></sup>
    </td>
    <td> 51.5 % </td>
    <td rowspan="3">2022</td>
  </tr>
  <tr class="table-notes">
    <td colspan="3">
      <ul>
        <li><code>targetSdk</code> <a href="https://developer.android.com/google/play/requirements/target-sdk">must be 33+</a> for new apps and app updates since August 31, 2023.</li>
      </ul>
    </td>
  </tr>
  <tr>
    <td rowspan="2">
      <b><a href="https://developer.android.com/about/versions/12">Android 12</a></b>
    </td>
    <td>
      Level 32
      <span class="subversion">Android 12L</span>
    </td>
    <td><code>S_V2</code></td>
    <td rowspan="2">
      Snow Cone
      <sup id="fnref:2"><a href="#fn:2" class="footnote">2</a></sup>
    </td>
    <td> 66.5 %</td>
    
  </tr>
  <tr>
    <td>Level 31 <span class="subversion">Android 12</span></td>
    <td><code>S</code></td>
    <td>2021</td>
  </tr>
  <tr>
    <td>
      <b><a href="https://developer.android.com/about/versions/11">Android 11</a></b>
    </td>
    <td>Level 30</td>
    <td><code>R</code></td>
    <td>
      Red Velvet Cake
      <sup id="fnref:2"><a href="#fn:2" class="footnote">2</a></sup>
    </td>
    <td> 79.8 %</td>  
    <td>2020</td>
  </tr>
  <tr>
    <td>
      <b><a href="https://developer.android.com/about/versions/10">Android 10</a></b>
    </td>
    <td>Level 29</td>
    <td><code>Q</code></td>
    <td>
      Quince Tart
      <sup id="fnref:2"><a href="#fn:2" class="footnote">2</a></sup>
    </td>
    <td> 87.1 %</td>    
    <td>2019</td>
  </tr>
  <tr>
    <td>
      <b><a href="https://developer.android.com/about/versions/pie">Android 9</a></b>
    </td>
    <td>Level 28</td>
    <td><code>P</code></td>
    <td>Pie</td>
    <td> 91.7 %</td>
    <td>2018</td>
  </tr>
  <tr>
    <td rowspan="2">
      <b><a href="https://developer.android.com/about/versions/oreo">Android 8</a></b>
    </td>
    <td>Level 27 <span class="subversion">Android 8.1</span></td>
    <td><code>O_MR1</code></td>
    <td rowspan="2">Oreo</td> 
    <td> 93.0 %</td>
    <td rowspan="2">2017</td>
  </tr>
  <tr>
    <td>Level 26 <span class="subversion">Android 8.0</span></td>
    <td><code>O</code></td>
    <td> 95.7 %</td>
  </tr>
  <tr>
    <td rowspan="2">
      <b><a href="https://developer.android.com/about/versions/nougat">Android 7</a></b>
    </td>
    <td>Level 25 <span class="subversion">Android 7.1</span></td>
    <td><code>N_MR1</code></td>
    <td rowspan="2">Nougat</td>
    <td> 96.0 %</td>
    <td rowspan="2">2016</td>
  </tr>
  <tr>
    <td>Level 24 <span class="subversion">Android 7.0</span></td>
    <td><code>N</code></td>
    <td> 97.2 %</td>
  </tr>
  <tr>
    <td>
      <b><a href="https://developer.android.com/about/versions/marshmallow">Android 6</a></b>
    </td>
    <td>Level 23</td>
    <td><code>M</code></td>
    <td>Marshmallow</td>
    <td> 98.6 %</td>
    <td rowspan="2">2015</td>
  </tr>
  <tr>
    <td rowspan="3">
      <b><a href="https://developer.android.com/about/versions/lollipop">Android 5</a></b>
    </td>
    <td>Level 22 <span class="subversion">Android 5.1</span></td>
    <td><code>LOLLIPOP_MR1</code></td>
    <td rowspan="2">Lollipop</td>
    <td> 99.1 %</td>
  </tr>
  <tr>
    <td>Level 21 <span class="subversion">Android 5.0</span></td>
    <td><code>LOLLIPOP</code>, <code>L</code></td>
    <td> 99.6 %</td>
    <td rowspan="3">2014</td>
  </tr>
  <tr class="table-notes"><td colspan="3">
    <ul>
      <li><a href="https://developer.android.com/jetpack">Jetpack</a>/<a href="https://developer.android.com/jetpack/androidx">AndroidX</a> libraries <a href="https://developer.android.com/jetpack/androidx/versions#version-table">require</a> a <code>minSdk</code> of 21 or higher since April 2024.</li>
      <li><a href="https://developer.android.com/jetpack/compose">Jetpack Compose</a> requires a <code>minSdk</code> of 21 or higher.</li>
      <li>Google Play services v23.30.99+ (August 2023) <a href="https://android-developers.googleblog.com/2023/07/google-play-services-discontinuing-updates-for-kitkat.html">drops support</a> for API levels below 21.</li>
    </ul>
  </td></tr>
  <tr>
    <td rowspan="10"><b>Android 4</b></td>
    <td>
      Level 20
      <span class="subversion">Android 4.4W</span> <sup id="fnref:3"><a href="#fn:3" class="footnote">3</a></sup>
    </td>
    <td><code>KITKAT_WATCH</code></td>
    <td rowspan="2">KitKat</td>
    <td> 99.7 %</td>
  </tr>
  <tr>
    <td>
      Level 19
      <span class="subversion">Android 4.4</span>
    </td>
    <td><code>KITKAT</code></td>
    <td rowspan="3">2013</td>
  </tr>
  <tr class="table-notes"><td colspan="3">
    <ul>
      <li><a href="https://developer.android.com/jetpack">Jetpack</a>/<a href="https://developer.android.com/jetpack/androidx">AndroidX</a> libraries <a href="https://android-developers.googleblog.com/2023/10/androidx-minsdkversion-19.html">require</a> a <code>minSdk</code> of 19 or higher since October 2023.</li>
      <li>Google Play services v21.33.56+ (July 2021) <a href="https://android-developers.googleblog.com/2021/07/google-play-services-discontinuing-jelly-bean.html">drops support</a> for API levels below 19.</li>
    </ul>
  </td></tr>
  <tr>
    <td>Level 18 <span class="subversion">Android 4.3</span></td>
    <td><code>JELLY_BEAN_MR2</code></td>
    <td rowspan="3">Jelly Bean</td>
    <td> 99.8 %</td>
  </tr>
  <tr>
    <td>Level 17 <span class="subversion">Android 4.2</span></td>
    <td><code>JELLY_BEAN_MR1</code></td>
    <td> 99.8 %</td>
    <td rowspan="3">2012</td>
  </tr>
  <tr>
    <td>Level 16 <span class="subversion">Android 4.1</span></td>
    <td><code>JELLY_BEAN</code></td>
    <td> 99.8 %</td>
  </tr>
  <tr class="table-notes"><td colspan="3">
    <ul>
      <li>Google Play services v14.8.39+ (December 2018) <a href="https://android-developers.googleblog.com/2018/12/google-play-services-discontinuing.html">drops support</a> for API levels below 16.</li>
    </ul>
  </td></tr>
  <tr>
    <td>Level 15 <span class="subversion">Android 4.0.3 – 4.0.4</span></td>
    <td><code>ICE_CREAM_SANDWICH_MR1</code></td>
    <td rowspan="2">Ice Cream Sandwich</td>
    <td> 99.8 %</td>
    <td rowspan="7">2011</td>
  </tr>
  <tr>
    <td>Level 14 <span class="subversion">Android 4.0.1 – 4.0.2</span></td>
    <td><code>ICE_CREAM_SANDWICH</code></td>
    <tr class="table-notes"><td colspan="3">
      <ul>
        <li>Earlier <a href="https://developer.android.com/jetpack">Jetpack</a>/<a href="https://developer.android.com/jetpack/androidx">AndroidX</a> libraries <a href="https://developer.android.com/topic/libraries/support-library#api-versions">required</a> a <code>minSdk</code> of 14 or higher.</li>
      </ul>
    </td></tr>
  </tr>
  <tr>
    <td rowspan="3"><b>Android 3</b></td>
    <td>Level 13 <span class="subversion">Android 3.2</span></td>
    <td><code>HONEYCOMB_MR2</code></td>
    <td rowspan="3">Honeycomb</td>
    <td rowspan="13"><i>No data</i></td>
  </tr>
  <tr>
    <td>Level 12 <span class="subversion">Android 3.1</span></td>
    <td><code>HONEYCOMB_MR1</code></td>
  </tr>
  <tr>
    <td>Level 11 <span class="subversion">Android 3.0</span></td>
    <td><code>HONEYCOMB</code></td>
  </tr>
  <tr>
    <td rowspan="6"><b>Android 2</b></td>
    <td>Level 10 <span class="subversion">Android 2.3.3 – 2.3.7</span></td>
    <td><code>GINGERBREAD_MR1</code></td>
    <td rowspan="2">Gingerbread</td>
  </tr>
  <tr>
    <td>Level 9 <span class="subversion">Android 2.3.0 – 2.3.2</span></td>
    <td><code>GINGERBREAD</code></td>
    <td rowspan="3">2010</td>
  </tr>
  <tr>
    <td>Level 8 <span class="subversion">Android 2.2</span></td>
    <td><code>FROYO</code></td>
    <td>Froyo</td>
  </tr>
  <tr>
    <td>Level 7 <span class="subversion">Android 2.1</span></td>
    <td><code>ECLAIR_MR1</code></td>
    <td rowspan="3">Eclair</td>
  </tr>
  <tr>
    <td>Level 6 <span class="subversion">Android 2.0.1</span></td>
    <td><code>ECLAIR_0_1</code></td>
    <td rowspan="5">2009</td>
  </tr>
  <tr>
    <td>Level 5 <span class="subversion">Android 2.0</span></td>
    <td><code>ECLAIR</code></td>
  </tr>
  <tr>
    <td rowspan="4"><b>Android 1</b></td>
    <td>Level 4 <span class="subversion">Android 1.6</span></td>
    <td><code>DONUT</code></td>
    <td>Donut</td>
  </tr>
  <tr>
    <td>Level 3 <span class="subversion">Android 1.5</span></td>
    <td><code>CUPCAKE</code></td>
    <td>Cupcake</td>
  </tr>
  <tr>
    <td>Level 2 <span class="subversion">Android 1.1</span></td>
    <td><code>BASE_1_1</code></td>
    <td>Petit Four</td>
  </tr>
  <tr>
    <td>Level 1 <span class="subversion">Android 1.0</span></td>
    <td><code>BASE</code></td>
    <td><i>None</i></td>
    <td>2008</td>
  </tr>
</table>
</div>
