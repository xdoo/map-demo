# map-demo

## Project setup

Konsole öffnen in das Projektverzeichnis wechseln und `npm install` absetzen. Voraussetzung: npm muss installiert sein. 

### Compiles and hot-reloads for development

Um das Projekt lokal zu testen, Konsole öffnen und im Projektverzeichnis `npm run serve`absetzen. Die Anwendung ist nun unter http://localhost:8080 erreichbar.

## Pakete zur Kartendarstellung

Um die Karten in Vue.je einzubetten wurde leaflet (https://leafletjs.com/) in Verbindung mit Vue2Leaflet (https://korigan.github.io/Vue2Leaflet/#/) verwendet. Zusätzliches Kartenmaterial kann unter https://leaflet-extras.github.io/leaflet-providers/preview/ gefunden werden. Auch die Esri Karten (die dann natürlich auf einem öffentlichen Server liegen). Die Karten können dann in der Komponente '/components/DemoMap.vue' eingebunden werden. Das entsprechende Attribut habe ich im Code markiert:

```Javascript
  data() {
    return {
      zoom: 12,
      // hier muss dann die esri map referenziert werden
      url:'https://{s}.tile.openstreetmap.de/tiles/osmde/{z}/{x}/{y}.png',
      attribution:'&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      center: [48.1371181,11.5755711] // Marienplatz
    }
  }
```

## Weitere grafische Elemente

Um die Anwendung mit weiteren grafischen Elementen (z.B. Navigation links, Suchfeld, etc. ) anzureichern, sollte Vuetify (https://vuetifyjs.com/en/) verwendet werden. Unter 'Documentation' findet man die Komponenten. Unter https://vuetifyjs.com/en/framework/pre-made-layouts findet man auch schon komplette Layouts. Wichtig ist, dass die 'MapView' in der Datei 'App.vue' immer im Element `v-content` eingettet ist:

```
<v-content>
  <map-view/>
</v-content>
```

Die muss natürlich vorher importiert werden, wenn nicht der Router verwendet wird (Habe ich jetzt in diesem kleinen Demo nicht verwendet - wenn man einen Seitenwechsel zeigen will, dann benötigt man den aber.).

