# map-demo

![Map demo](/images/startseite.png)

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

## Deployment auf Heroku

Um die Anwendung vorführen zu können, muss sie entweder auf einem Rechner lokal ausgeführt werden (siehe oben), oder auf einem öffentlichen Server ausgebracht werden. Heroku eignet sich hierfür gut (ein kostenloses Image reicht vollkommen). Die Anwendung ist so konfiguriert, dass sie automatisch auf Heroku ausgeführt wird, sobald das Git Repository mit der Heroku App verbunden wurde.

## Funktionalität

Die Karte kann - wie man es beispielsweise von Google Maps kennt - durch drücken und festhalten der Maus bewegt werden. Durch scrollen mit dem Mausrad kann in die Karte herein oder aus der Karte heraus gezoomt werden. Zuätzlich kann über den Floating Action Button etwas auf der Karte eingezeichnet werden. 

### Punkt setzen

Über den Speeddial Floating Button "Punkt setzen" auswählen.

![Map demo](/images/speed_dial_offen_punkt.png)

Danach kann per Mausklick auf der Karte ein Punkt gesetzt werden. Der Bearbeitungsmodus wird mit setzen des Punktes automatisch beendet. D.h. es kann immer nur ein Punkt auf der Karte gesetzt werden (sollte die anforderung anders sein, dann können natürlich auch mehrere Punkte gesetzt werden). Will man den Punkt versetzen, so muss dieser erst gelöscht werden (Mülleimer im Seepdial Menü).

![Map demo](/images/punkt.png)


### Linie einzeichnen

Über den Speeddial Floating Button Linie auswählen. 

![Map demo](/images/speed_dial_offen_linie.png)

Danach kann man mit der Maus eine Linie auf der Karte ziehen. Der Malvorgang kann durch die Enter Taste beendet werden.

![Map demo](/images/linie.png)

### Polygon (geschlossen Fläche) einzeichnen

Über den Speeddial Floating Button Polygon auswählen. 

![Map demo](/images/speed_dial_offen_polygon.png)

Danach kann mit der Maus ein Polygon auf die Karte zeichnen. Dazu den ersten Punkt mit "Klick" markieren und die weiteren Punkte ebenfalls mit Klick setzen. Die Bearbeitung kann mit "Enter" beendet werden.

![Map demo](/images/polygon.png)


 
