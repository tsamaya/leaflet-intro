# Introduction à leafletjs
## Maptime Alpes
### Décembre 2015

---

Vous pouvez suivre cette présentation en ligne

[tsamaya.github.io/leaflet-intro](http://tsamaya.github.io/leaflet-intro)<!-- .element: target="_blank" -->

---

Recommandations

- éditeur de texte : [atom.io](http://atom.io)<!-- .element: target="_blank" -->, [brackets](http://brackets.io/)<!-- .element: target="_blank" -->
- navigateur : [chrome](https://www.google.fr/chrome/browser/desktop/)<!-- .element: target="_blank" -->
- utiliser un serveur web
  - sinon avec un compte [github](http://github.com)<!-- .element: target="_blank" --> :
    - [jsbin](http://jsbin.com)<!-- .element: target="_blank" -->
    - [gist](http://gist.github.com)<!-- .element: target="_blank" --> et http://bl.ocks.org/USER<!-- .element: target="_blank" -->

---

#Leaflet Quick Start Guide

---

### template

```HTML
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8" />
  <meta name='viewport' content='width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no' />
  <style type="text/css">
    body {
      padding: 0;
      margin: 0;
    }

    html, body, #map {
      height: 100%;
      height: 100%;
    }
  </style>
  <link rel="stylesheet" href="http://cdn.leafletjs.com/leaflet/v0.7.7/leaflet.css" />
</head>
<body>
  <div id="map"></div>
  <script src="http://cdn.leafletjs.com/leaflet/v0.7.7/leaflet.js"></script>
  <script>
// ici
  </script>
</body>
</html>
```
- jsbin : [jsbin.com/fojeta](http://jsbin.com/fojeta/edit?html,css,js,output)<!-- .element: target="_blank" -->
- gist : [gist/593362928b8ee8c185de](https://gist.github.com/tsamaya/593362928b8ee8c185de)<!-- .element: target="_blank" -->
- bl.ocks.org [bl.ocks.org/593362928b8ee8c185de](http://bl.ocks.org/tsamaya/593362928b8ee8c185de)<!-- .element: target="_blank" -->

---

### Permière carte

<iframe id="thefirstmap" src="demos/demo1.html" style="width:100%; height:350px;"></iframe>

```JS
var map = L.map('map').setView([45.18478, 5.73134], 13);

L.tileLayer('http://{s}.tile.opentopomap.org/{z}/{x}/{y}.png', {
    maxZoom: 15,
    attribution: 'Map style: &copy; <a href="https://opentopomap.org">OpenTopoMap</a>'
}).addTo(map);

L.marker([45.18478, 5.73134]).addTo(map)
    .bindPopup('Coworking in Grenoble.')
    .openPopup();
```

---

### Gestion des événements
<iframe id="theclickmap" src="demos/demo2.html" style="width:100%; height:350px;"></iframe>
```JS
var popup = L.popup();

function onMapClick(e) {
    popup
        .setLatLng(e.latlng)
        .setContent("Vous avez cliqué la carte aux coordonnées " + e.latlng.toString())
        .openOn(map);
}

map.on('click', onMapClick);
```

---

### Cercle
<iframe id="thecirclemap" src="demos/demo3.html" style="width:100%; height:350px;"></iframe>
```JS
var circle = L.circle([45.18521, 5.75611], 500, {
    color: 'red',
    fillColor: '#f03',
    fillOpacity: 0.5
}).addTo(map);
```

---

### Polygone
<iframe id="thepolygonmap" src="demos/demo4.html" style="width:100%; height:350px;"></iframe>

```JS
var polygon = L.polygon([
    [45.20091, 5.65487],
    [45.18276, 5.68182],
    [45.17562, 5.65418]
  ]).addTo(map);
```

---

### Popups
<iframe id="thepopupsonmap" src="demos/demo5.html" style="width:100%; height:350px;"></iframe>
```JS
marker.bindPopup('<b>Hello from Cowork in Grenobe!</b><br>Je suis une popup.').openPopup();
circle.bindPopup('Je suis un cercle.');
polygon.bindPopup('Je suis un  polygone.');
```

---

### debug et inspection
<iframe id="aaaaiframedebug" src="demos/demo5.html" style="width:100%; height:350px;"></iframe>

Exécuter ce code dans la console pour l'`iframe aaaaiframedebug` (CTRL+SHIT+I) ou (CMD+ALT+I)

```JS
map.getCenter();
map.getZoom();
map.setView(circle.getLatLng());
map.setMaxBounds(polygon.getBounds());
polygon.openPopup();
map.setMaxBounds(null);
```

---

### actions
<iframe id="aaaaiframeaction" src="demos/demo1.html" style="width:100%; height:350px;"></iframe>

Exécuter ce code dans la console pour l'`iframe aaaaiframeaction`

```JS
map.setView(L.latLng(50, 2), 5);
var popup = L.popup().setLatLng([51.52145, -0.20312]);
popup.setContent('Je suis une pauvre popup solitaire loin de chez elle');
popup.openOn(map);
```

---

### Geojson
Ce que nous allons faire, utiliser des fichiers `geojson` et les afficher ainsi

<iframe width="700" height="400" src="http://data.beta.metropolegrenoble.fr/dataset/pistes-cyclables/resource/e03a8056-ad7f-4000-873a-a0b382d8650a/view/e374e2b4-b9bb-4176-a0ee-7c2c4113f929" frameBorder="0"></iframe>

Source de données pour ce soir : [data.metropolegrenoble.fr](http://data.metropolegrenoble.fr)<!-- .element: target="_blank" -->

---

### Utiliser une couche GeoJSON
<iframe id="thegeojsonsonmap" src="demos/demo6.html" style="width:100%; height:200px;"></iframe>

```JS
var geojsonFeature = {
    'type': 'Feature',
    'properties': {
        'name': 'Espace Vertical - ev3',
        'leisure': 'sports_center',
        'popupContent': 'Une salle fantastique !'
    },
    'geometry': {
        'type': 'Point',
        'coordinates': [5.7035638, 45.1844921]
    }
};
L.geoJson(geojsonFeature).addTo(map);
```

Vous noterez la différence Lon/Lat (ici) vs Lat/Lon (leaflet)

---

### Utiliser un fichier GeoJSON
<iframe id="thegeojsonsonmap" src="demos/demo7.html" style="width:100%; height:350px;"></iframe>

```HTML
<script src="//rawgit.com/calvinmetcalf/leaflet-ajax/master/dist/leaflet.ajax.min.js"></script>  
```

```JS
var geojsonLayer = new L.GeoJSON.AJAX('http://metromobilite.fr/data/Carto/Statique/velo.geojson').addTo(map);
```

---

# Plugins

- Nous venons d'utiliser [GeoJSON.ajax](https://github.com/calvinmetcalf/leaflet-ajax)<!-- .element: target="_blank" -->
- heatmap : [leaflet.github.io/Leaflet.heat/demo/](http://leaflet.github.io/Leaflet.heat/demo/)<!-- .element: target="_blank" -->
- markercluster : [Leaflet.markerclusterr](https://github.com/Leaflet/Leaflet.markercluster)<!-- .element: target="_blank" -->
- les [Plugins leaflet](http://leafletjs.com/plugins.html)<!-- .element: target="_blank" -->

---

### heatmap

<iframe id="theheatmap" src="demos/demo8.html" style="width:100%; height:350px;"></iframe>

```HTML
<script src="http://leaflet.github.io/Leaflet.heat/dist/leaflet-heat.js"></script>
```

```JS
var heat = L.heatLayer([], {
  radius : 10
}).addTo(map);

var geojsonLayer = new L.GeoJSON.AJAX('https://gist.githubusercontent.com/tsamaya/d5d9b55f45dff404d5e8/raw/80c514ebdf15db70e053a9df9175ee63616d206d/arceaux.geojson', {
  onEachFeature: function(f,l) {
      heat.addLatLng(l.getLatLng());
  }
});
```

---

### marker cluster

<iframe id="theMCmap" src="demos/demo9.html" style="width:100%; height:350px;"></iframe>

```HTML
<link rel="stylesheet" href="http://leaflet.github.io/Leaflet.markercluster/dist/MarkerCluster.css" />
<link rel="stylesheet" href="http://leaflet.github.io/Leaflet.markercluster/dist/MarkerCluster.Default.css" />

<script src="http://leaflet.github.io/Leaflet.markercluster/dist/leaflet.markercluster.js"></script>
```

```JS
var markers = new L.MarkerClusterGroup();

var geojsonLayer = new L.GeoJSON.AJAX('https://gist.githubusercontent.com/tsamaya/d5d9b55f45dff404d5e8/raw/80c514ebdf15db70e053a9df9175ee63616d206d/arceaux.geojson', {
  pointToLayer: function(feature, latlng) {
    var marker = L.marker(latlng);
    markers.addLayer(marker);
    return marker;
  }
});
map.addLayer(markers);
```

---

# Liens
- leaflet : [leafletjs.com](http://leafletjs.com)<!-- .element: target="_blank" -->
- fonds de plan : [leaflet-providers](http://leaflet-extras.github.io/leaflet-providers/preview/)<!-- .element: target="_blank" -->

---

#Cool maps
- [nimianlegends.com/empires](http://nimianlegends.com/empires/) <!-- .element: target="_blank" -->
- [windyty.com](http://windyty.com/)<!-- .element: target="_blank" -->

---

## Challenges

- leaflet bien sûr
- données : densité de population
- viz : chartjs et ou d3


[voir](./challenges/)<!-- .element: target="_blank" --> une solution
