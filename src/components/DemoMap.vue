<template>
    <v-card style="height: 100%; width: 100%; margin: 0">
    <l-map 
      ref="map"
      :zoom="zoom" 
      :center="center" 
      style="z-index: 1"
      v-bind:style="{cursor: cursor}"
      v-on:update:center="showCenter($event)"
      v-on:update:zoom="showZoom($event)"
      v-on:mousemove="previewObject($event)"
      v-on:keypress="done($event)"
      v-on:click="addPoint($event)">
      <l-polyline
        ref="polyline"
        :lat-lngs="polyline"
      >
      </l-polyline>
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
      >
        <v-icon>mdi-vector-square</v-icon>
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
      polyline: [],
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
      this.cursor = 'crosshair'
      this.drawpolyline = true
      this.polyline = []
    },
    showCenter (event) {
      console.log('moved -> ' + event) // eslint-disable-line no-console
    },
    showZoom (event) {
      console.log('zoomed -> ' + event) // eslint-disable-line no-console
    },
    // showMouse (event) {
      // console.log('my mouse -> ' + event.latlng + ' -- ' + this.$refs.map.zoom) // eslint-disable-line no-console
    // },
    addPoint (event) {
      if (this.drawpolyline) {
        this.polyline.push(event.latlng)
      }

      this.preview = false
    },
    /**
     * Zeichnet das Objekt als Vorschau. Bei einem
     * Polygon die Strecke vom letzten Punkt zur Maus.
     */
    previewObject (event) {

      // Preview für den Polygon Modus
      if (this.drawpolyline && this.preview) {
        this.polyline.pop()
        this.polyline.push(event.latlng)
      } else if(this.drawpolyline) {
        this.preview = true
        this.polyline.push(event.latlng)
      }
    },
    remove () {
      this.polyline = []
    },
    done (event) {
      if(event.originalEvent.key === 'Enter') {
        if(this.drawpolyline && this.preview) {
          this.polyline.pop()
          this.drawpolyline = false
          this.preview = false
        }

        this.drawing = false
        this.cursor = 'all-scroll'
      } 
    }
  }
  
}
</script>
