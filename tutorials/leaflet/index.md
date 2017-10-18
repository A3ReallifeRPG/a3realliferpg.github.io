# Arma Map via Leaflet

## Export

Die Map als Sattelitenkarte zu exportieren ist leider direkt nicht möglich, entweder hat man Zugriff auf die Original Satmap oder klebt die einzelnen Tiles die man in der Map findet zusammen.

Straßenkarte, Höhenlinien und Büsche etc sind einfach zu exportieren, dies geht via dem [Cheat Command](https://community.bistudio.com/wiki/ArmA:_Cheats#TOPOGRAPHY) `TOPOGRAPHY` oder `EXPORTNOGRID`, dazu müsst ihr beachten Arma (unter Windows) UAC Virtualisiert ("Als Administrator") gestartet zu haben damit es in euer Hauptverzeichnis ("C:") die Map als .emf exportieren kann.

Unten als Download findet ihr die EmfToPng.exe, diese ist nichtmehr in den Arma 3 Tools enthalten, ich habe diese Version von Killzonekid den ich als Vertrauenswürdig einstufen würde.

Jetzt kopiert ihr die .emf einfach irgendwo hin wo ihr ohne erhöhte Rechte schreiben könnt und zieht sie auf die EmfToPng.exe, so erhaltet ihr eine .png, die ihr bearbeiten könnt.

## Maptiles erstellen

Installiert euch die Python-toolbox GDAL2Tiles, mit dieser könnt ihr aus einer PNG/JPEG Datei die nötigen Preview/Layerbilder erzeugen damit Leaflet sie benutzen kann und euer Bild beim Zoomen nicht ewig lädt.

Bevor ihr das Script benutzen könnt müsst ihr euch entscheiden wieviel Zoom euere Map haben soll. Zoomstufen sind nur als 2er Potenz minimal 256 möglich.

 - Zoom 0: 256 px
 - Zoom 1: 512 px
 - Zoom 2: 1024 px
 - Zoom 3: 2048 px
 - Zoom 4: 4096 px
 - Zoom 5: 8192 px
 - Zoom 6: 16384 px
 - ...

Falls ihr die dafür nötige Auflösung unterschreitet habt ihr weiße Ränder bis zur nötigen Größe. Es sieht besser aus wenn ihr das Bild noch richtig rezised. Dafür könnt ihr das von GDAL gelieferte Tool gdal_translate benutzen.

`gdal_translate -of PNG -outsize 16384 16384 sat.png satrez.png`

So erhaltet ihr eine 16384*16384px png eures Bildes. Falls ihr keine Transparenz braucht und eure Map schneller laden soll könnt ihr auch hier einfach ein JPEG aus eurem Bild machen.

`gdal_translate -of JPG -outsize 16384 16384 sat.png satrez.jpg`

Als letzten Schritt tilen wir nun unser Bild mithilfe von gdal_tiles.

`gdal2tiles.py -p raster -z 0-6 -w none satrez.jpg sat`

 -p raster erstellt ein neues Raster da wir keine realen Koordinaten haben
 
 -z sind die zu verwendenden Zoomlevel 
 
Im Ordner /sat findet ihr nun die fertigen Tiles.
 
Die legt ihr jetzt auf einem Webserver bereit.
 
## Leaflet.js Konfiguration
 
Ladet leaflet.js und das nötige css.
 
Erstellt einen div mit Höhe und Breite.
 
`<div style="width: 1135px; height: 580px" id="map"></div>`
 
```javascript
var sat = L.tileLayer('https://webserver.shady.cc/sat/{z}/{x}/{y}.png', {
        minZoom: 1,
        maxZoom: 6,
        attribution: 'Eure Attribution',
        tms: true
    });

    var map = L.map('map', {
        layers: [sat]
    }).setView([0, 0], 1);

    var baseLayers = {
        "Satellit": sat
    };

    L.control.layers(baseLayers).addTo(map);

    var southWest = map.unproject([0, 16384], map.getMaxZoom()); //Original-Höhe
    var northEast = map.unproject([16384, 0], map.getMaxZoom()); //Original-Breite
    map.setMaxBounds(new L.LatLngBounds(southWest, northEast));
```

Fertig!

Für mehr Konfigurationsmöglichkeiten etc befragt die [leaflet-docs](http://leafletjs.com/reference-1.2.0.html).

###### Downloads

[EmfToPng.exe](https://github.com/A3ReallifeRPG/a3realliferpg.github.io/releases/download/EmfToPng.exe/EmfToPng.exe)

###### Quellen

https://community.bistudio.com/wiki/ArmA:_Cheats

https://build-failed.blogspot.de/2012/11/zoomable-image-with-leaflet.html

http://leafletjs.com/