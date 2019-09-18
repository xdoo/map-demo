<template>
    <v-card style="height: 100%; width: 100%; margin: 0">
    <l-map 
      :zoom="zoom" 
      :center="center" 
      style="z-index: 1"
      v-on:update:center="showCenter($event)"
      v-on:update:zoom="showZoom($event)">
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
    </l-map>
    <v-speed-dial
      v-model="fab"
      fixed
      bottom
      right
      open-on-hover
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
        dark
        small
        color="green"
      >
        <v-icon>mdi-map-marker-plus</v-icon>
      </v-btn>
      <v-btn
        fab
        dark
        small
        color="indigo"
      >
        <v-icon>mdi-vector-line</v-icon>
      </v-btn>
      <v-btn
        fab
        dark
        small
        color="red"
      >
        <v-icon>mdi-vector-square</v-icon>
      </v-btn>
    </v-speed-dial>
  </v-card>
</template>
<script>
export default {
  name: 'demoMap',
  data() {
    return {
      fab: false,
      zoom: 12,
      // hier muss dann die esri map referenziert werden
      url:'https://{s}.tile.openstreetmap.de/tiles/osmde/{z}/{x}/{y}.png',
      attribution:'&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      center: [48.1371181,11.5755711] // Marienplatz
    }
  },
  methods: {
    showCenter (event) {
      console.log('moved -> ' + event) // eslint-disable-line no-console
    },
    showZoom (event) {
      console.log('zoomed -> ' + event) // eslint-disable-line no-console
    }
  }
  
}
</script>
