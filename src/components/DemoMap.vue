<template>
    <v-card style="height: 100%; width: 100%; margin: 0">
    <l-map 
      ref="map"
      :zoom="zoom" 
      :center="center" 
      style="z-index: 1"
      v-bind:style="{cursor: cursor}"
      v-on:mousemove="previewObject($event)"
      v-on:keypress="done($event)"
      v-on:click="addPoint($event)">
      <l-polyline
        ref="polyline"
        :lat-lngs="pointspolyline"
      >
      </l-polyline>
      <l-polygon
        ref="polygon"
        :lat-lngs="pointspolygon"
      >
      </l-polygon>
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
    </l-map>
    <v-speed-dial
      v-model="fab"
      fixed
      bottom
      right
    >
      <template v-slot:activator>
        <v-btn
          v-model="fab"
          color="blue darken-2"
          dark
          fab
        >
          <v-icon v-if="fab">mdi-close</v-icon>
          <v-icon v-else>mdi-lead-pencil</v-icon>
        </v-btn>
      </template>
      <v-btn
        fab
        :disabled="drawing"
        dark
        small
        color="indigo"
      >
        <v-icon>mdi-map-marker-plus</v-icon>
      </v-btn>
      <v-btn
        fab
        :disabled="drawing"
        dark
        small
        color="indigo"
        @click="addPolyLine()"
      >
        <v-icon>mdi-vector-polyline</v-icon>
      </v-btn>
      <v-btn
        fab
        :disabled="drawing"
        dark
        small
        color="indigo"
        @click="addPolygon()"
      >
        <v-icon>mdi-vector-polygon</v-icon>
      </v-btn>
      <v-btn
        fab
        :disabled="drawing"
        dark
        small
        color="green"
      >
        <v-icon>mdi-check-bold</v-icon>
      </v-btn>
      <v-btn
        fab
        :disabled="drawing"
        dark
        small
        color="red"
        @click="remove()"
      >
        <v-icon>mdi-delete</v-icon>
      </v-btn>
    </v-speed-dial>
  </v-card>
</template>
<script>
export default {
  name: 'demoMap',
  data() {
    return {
      cursor: 'all-scroll',
      drawing: false,
      preview: false,
      drawpolyline: false,
      drawpolygon: false,
      pointspolyline: [],
      pointspolygon: [],
      fab: false,
      zoom: 12,
      // hier muss dann die esri map referenziert werden
      url:'https://{s}.tile.openstreetmap.de/tiles/osmde/{z}/{x}/{y}.png',
      attribution:'&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      center: [48.1371181,11.5755711] // Marienplatz
    }
  },
  methods: {
    addPolyLine () {
      this.drawing = true
      this.cursor = 'pointer'
      this.drawpolyline = true
      this.pointspolyline = []
    },
    addPolygon () {
      this.drwaing = true
      this.cursor = 'pointer'
      this.drawpolygon = true
      this.pointspolygon = []
    },
    addPoint (event) {
      if (this.drawpolyline) {
        this.pointspolyline.push(event.latlng)
      }

      if (this.drawpolygon) {
        this.pointspolygon.push(event.latlng)
      }

      this.preview = false
    },
    /**
     * Zeichnet das Objekt als Vorschau. Bei einem
     * Polygon die Strecke vom letzten Punkt zur Maus.
     */
    previewObject (event) {

      // Preview für den Polyline Modus
      if (this.drawpolyline && this.preview) {
        this.pointspolyline.pop()
        this.pointspolyline.push(event.latlng)
      } else if(this.drawpolyline) {
        this.preview = true
        this.pointspolyline.push(event.latlng)
      }

      // Preview für den Polygon Modus
      if (this.drawpolygon && this.preview) {
        this.pointspolygon.pop()
        this.pointspolygon.push(event.latlng)
      } else if(this.drawpolygon) {
        this.preview = true
        this.pointspolygon.push(event.latlng)
      }
    },
    /**
     * Diese Methode löscht alle gemalten Punkte auf
     * der Karte. 
     */
    remove () {
      this.pointspolyline = []
      this.pointspolygon = []
    },
    /**
     * Tastendruck Enter zum Beenden des Malvorgangs.
     */
    enter (event) {
      if(event.originalEvent.key === 'Enter') {
        this.done()
      }
    },
    /**
     * Diese Methode löscht alle auf der Karte gesetzten Punkte.
     * Dabei ist es egal, ab es sich um eine Linie, ein Ploygon
     * oder nur einen einzelnen Punkt handelt.
     */
    done () {

        // Beendet den Malvorgang auf der Polyline
        if(this.drawpolyline && this.preview) {
          this.pointspolyline.pop()
          this.drawpolyline = false
          this.preview = false
        }

        // Beendet den Malvorgang auf dem Polygon
        if(this.drawpolygon && this.preview) {
          this.pointspolygon.pop()
          this.drawpolygon = false
          this.preview = false
        }

        this.drawing = false
        this.cursor = 'all-scroll'
    }
  }
  
}
</script>
