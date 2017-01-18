**OpenLayers dan OverLay**

<p align ="center">
<img src="../../img/10.JPG" width="600px">
</p>

**LATAR BELAKANG**

Pada pertemuan ke 10 Sistem Informasi Geografi dibahas tentang OpenLayers dan OverLay. OpenLayers adalah sebuah library untuk menempatkan peta. Sementara OverLay proses penempatan grafis suatu peta. Di bab pembahasan akan dijelaskan tentang OpenLayers dan OverLay beserta contohnya.

**PEMBAHASAN**

OpenLayers

Merupakan sebuah library javascript yang berguna untuk menampilkan data dari peta, bersifat opensource. Jadi dengan kata lain, OpenLayers dapat menampilkan peta dari berbagai sumber seperti GoogleMap ataupun sumber lainnya. Open layers juga dapat diubah untuk mendapatkan sumber peta dari MapServer lainnya.

**OverLay**

Merupakan sebuah prosedur yang penting dalam Sistem Informasi Geografis. Overlay juga mampu menempatkan grafis suatu peta diatas grafis peta lainnya agar menghasilkan gabungan kedua peta yang memiliki informasi atribut dari kedua peta tersebut. Teknik overlay dalam sistem informasi geografis ada 2 yaitu gabungan (union) dan irisan (intersect).

**Contoh Overlay pada OpenLayers**

~~~
<!DOCTYPE html>
<html>
  <head>
    <title>Overlay</title>
    <link rel="stylesheet" href="https://openlayers.org/en/v3.20.1/css/ol.css" type="text/css">
    <!-- The line below is only needed for old environments like Internet Explorer and Android 4.x -->
    <script src="https://cdn.polyfill.io/v2/polyfill.min.js?features=requestAnimationFrame,Element.prototype.classList,URL"></script>
    <script src="https://openlayers.org/en/v3.20.1/build/ol.js"></script>
    <script src="https://code.jquery.com/jquery-2.2.3.min.js"></script>
    <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/css/bootstrap.min.css">
    <script src="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.6/js/bootstrap.min.js"></script>
    <style>
      #marker {
        width: 20px;
        height: 20px;
        border: 1px solid #088;
        border-radius: 10px;
        background-color: #FF3300;
        opacity: 0.5;
      }
      #marker2 {
        width: 20px;
        height: 20px;
        border: 1px solid #088;
        border-radius: 10px;
        background-color: #FF3300;
        opacity: 0.5;
      }
      #marker3 {
        width: 20px;
        height: 20px;
        border: 1px solid #088;
        border-radius: 10px;
        background-color: #FF3300;
        opacity: 0.5;
      }
      #marker4 {
        width: 20px;
        height: 20px;
        border: 1px solid #088;
        border-radius: 10px;
        background-color: #FF3300;
        opacity: 0.5;
      }
      #marker5 {
        width: 20px;
        height: 20px;
        border: 1px solid #088;
        border-radius: 10px;
        background-color: #FF3300;
        opacity: 0.5;
      }
      #bandung {
        text-decoration: none;
        color: black;
        font-size: 11pt;
        font-weight: bold;
        text-shadow: white 0.1em 0.1em 0.2em;
      }
      #meulaboh {
        text-decoration: none;
        color: black;
        font-size: 11pt;
        font-weight: bold;
        text-shadow: white 0.1em 0.1em 0.2em;
      }
      #tapaktuan {
        text-decoration: none;
        color: black;
        font-size: 11pt;
        font-weight: bold;
        text-shadow: white 0.1em 0.1em 0.2em;
      }
      #binjai {
        text-decoration: none;
        color: black;
        font-size: 11pt;
        font-weight: bold;
        text-shadow: white 0.1em 0.1em 0.2em;
      }
      #lhokseumawe {
        text-decoration: none;
        color: black;
        font-size: 11pt;
        font-weight: bold;
        text-shadow: white 0.1em 0.1em 0.2em;
      }
      .popover-content {
        min-width: 180px;
      }
    </style>
  </head>
  <body>
    <div id="map" class="map"></div>
    <div style="display: none;">
      <!-- Clickable label -->
      <a class="overlay" id="bandung" target="_blank" href="http://id.wikipedia.org/wiki/Kota_Bandung">Bandung</a>
      <div id="marker" title="Marker"></div>

      <a class="overlay" id="meulaboh" target="_blank" href="http://id.wikipedia.org/wiki/Meulaboh">Meulaboh</a>
      <div id="marker2" title="Marker"></div>

      <a class="overlay" id="tapaktuan" target="_blank" href="http://id.wikipedia.org/wiki/Tapak_Tuan,_Aceh_Selatan">Tapaktuan</a>
      <div id="marker3" title="Marker"></div>

      <a class="overlay" id="binjai" target="_blank" href="http://id.wikipedia.org/wiki/Binjai">Binjai</a>
      <div id="marker4" title="Marker"></div>

      <a class="overlay" id="lhokseumawe" target="_blank" href="http://id.wikipedia.org/wiki/Kota_Lhokseumawe">Lhokseumawe</a>
      <div id="marker5" title="Marker"></div>
      <!-- Popup -->
      <div id="popup" title="Welcome to ol3"></div>
    </div>
    <script>
      var layer = new ol.layer.Tile({
        source: new ol.source.OSM({
              url: 'https://map.vas.web.id/wmts/agm/webmercator/{z}/{x}/{y}.png'
            })
      });

      var map = new ol.Map({
        layers: [layer],
        target: 'map',
        view: new ol.View({
          center: ol.proj.transform([118.015776, -2.6000285], 'EPSG:4326', 'EPSG:3857'),
          zoom: 5
        })
      });

      var pos = ol.proj.fromLonLat([107.5731165, -6.9034443]);
      var pos2 = ol.proj.fromLonLat([96.1178939, 4.1583436]);
      var pos3 = ol.proj.fromLonLat([97.1659381, 3.2686167]);
      var pos4 = ol.proj.fromLonLat([98.4661842, 3.6223238]);
      var pos5 = ol.proj.fromLonLat([97.0375949, 5.1718862]);

      // marker
      var marker = new ol.Overlay({
        position: pos,
        positioning: 'center-center',
        element: document.getElementById('marker'),
        stopEvent: false
      });
      map.addOverlay(marker);

      var marker2 = new ol.Overlay({
        position: pos2,
        positioning: 'center-center',
        element: document.getElementById('marker2'),
        stopEvent: false
      });
      map.addOverlay(marker2);

      var marker3 = new ol.Overlay({
        position: pos3,
        positioning: 'center-center',
        element: document.getElementById('marker3'),
        stopEvent: false
      });
      map.addOverlay(marker3);

      var marker4 = new ol.Overlay({
        position: pos4,
        positioning: 'center-center',
        element: document.getElementById('marker4'),
        stopEvent: false
      });
      map.addOverlay(marker4);

      var marker5 = new ol.Overlay({
        position: pos5,
        positioning: 'center-center',
        element: document.getElementById('marker5'),
        stopEvent: false
      });
      map.addOverlay(marker5);

      // label
      var bandung = new ol.Overlay({
        position: pos,
        element: document.getElementById('bandung')
      });
      map.addOverlay(bandung);

      var meulaboh = new ol.Overlay({
        position: pos2,
        element: document.getElementById('meulaboh')
      });
      map.addOverlay(meulaboh);

      var tapaktuan = new ol.Overlay({
        position: pos3,
        element: document.getElementById('tapaktuan')
      });
      map.addOverlay(tapaktuan);

      var binjai = new ol.Overlay({
        position: pos4,
        element: document.getElementById('binjai')
      });
      map.addOverlay(binjai);

      var lhokseumawe = new ol.Overlay({
        position: pos5,
        element: document.getElementById('lhokseumawe')
      });
      map.addOverlay(lhokseumawe);

      // Popup showing the position the user clicked
      var popup = new ol.Overlay({
        element: document.getElementById('popup')
      });
      map.addOverlay(popup);

      map.on('click', function(evt) {
        var element = popup.getElement();
        var coordinate = evt.coordinate;
        var hdms = ol.coordinate.toStringHDMS(ol.proj.transform(
            coordinate, 'EPSG:3857', 'EPSG:4326'));

        $(element).popover('destroy');
        popup.setPosition(coordinate);
        // the keys are quoted to prevent renaming in ADVANCED mode.
        $(element).popover({
          'placement': 'top',
          'animation': false,
          'html': true,
          'content': '<p>The location you clicked was:</p><code>' + hdms + '</code>'
        });
        $(element).popover('show');
      });
    </script>
  </body>
</html>
~~~

HASILNYA:

<p align ="center">
<img src="../../img/10-1.png" width="600px">
</p>

**PENUTUP**

1. **Kesimpulan :** OpenLayers merupakan Library JavaScript untuk menempatkan peta dinamis di halaman web, dan Overlay merupakan proses penempatan grafis suatu peta diatas grafis peta lainnya agar menghasilkan gabungan kedua peta yang memiliki informasi atribut dari kedua peta tersebut.
2. **Saran :** Agar mencari sumber lain yang lebih lengkap dan lebih mendalam membahas tentang OpenLayers dan Overlay.

