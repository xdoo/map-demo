<template>
    <div style="height: 100%; width: 100%; margin: 0">
    <l-map 
      :zoom="zoom" 
      :center="center" 
      style="z-index: 1"
      v-on:update:center="showCenter($event)"
      v-on:update:zoom="showZoom($event)">
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
    </l-map>
  </div>
</template>
<script>
export default {
  name: 'demoMap',
  data() {
    return {
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
