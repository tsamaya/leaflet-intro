# Introduction à leafletjs
## Maptime Alpes 2015
Arnaud Ferrand

[![octocat](images/github.png)<!-- .element style="border: 0; box-shadow: none;" -->](https://github.com/tsamaya/)<!-- .element: target="_blank" -->[![octocat](images/twitter.png)<!-- .element style="border: 0; box-shadow: none;" -->](https://twitter.com/arferrand/)<!-- .element: target="_blank" -->

---

Vous pouvez suivre cette présentation en ligne

[tsamaya.github.io/leaflet-intro](http://tsamaya.github.io/leaflet-intro)<!-- .element: target="_blank" -->

---

Recommendations

- éditeur de texte : [atom.io](http://atom.io)<!-- .element: target="_blank" -->
- github / gist
- jsbin

---

#Leaflet Quick Start Guide

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
var circle = L.circle([51.508, -0.11], 500, {
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

### debug
<iframe id="aaaaiframedebug" src="demos/demo5.html" style="width:100%; height:350px;"></iframe>

dans l'`iframe aaaaiframedebug`

```JS
map.getCenter();
map.getBounds();
map.getZoom();
map.getPixelBounds();
```

---

### actions
<iframe id="aaaaiframeaction" src="demos/demo1.html" style="width:100%; height:350px;"></iframe>

dans l'`iframe aaaaiframeaction`

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

# Plugins

- heatmap : http://leaflet.github.io/Leaflet.heat/demo/
- markercluster
- un autre
- lien vers les Plugins

---

# Liens
- leafletjs : http://leafletjs.com<!-- .element: target="_blank" -->
- fonds de plan : http://leaflet-extras.github.io/leaflet-providers/preview/<!-- .element: target="_blank" -->

---

#Cool maps
- http://nimianlegends.com/empires/ <!-- .element: target="_blank" -->
- http://windyty.com/<!-- .element: target="_blank" -->
