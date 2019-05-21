<template>
    <v-container
      fluid
      fill-height
      class="pa-0"
    >
      <demo-map></demo-map>
    </v-container>
</template>
<script>
import DemoMap from '@/components/DemoMap.vue'

export default {
  name: 'mapView',
  components: {
    DemoMap
  }  
}
</script>

