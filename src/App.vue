<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>LHM </span>
        <span class="font-weight-light">MAP DEMO</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <span>...</span>
    </v-toolbar>

    <v-content>
      <map-view/>
    </v-content>
  </v-app>
</template>

<script>
import MapView from './views/MapView'

export default {
  name: 'App',
  components: {
    MapView
  },
  data () {
    return {
      //
    }
  }
}
</script>
