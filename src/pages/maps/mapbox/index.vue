<template>
  <i-card class="mapbox" shadow :padding="5">
    <MapContainer @on-load="onMapLoad"></MapContainer>
  </i-card>
</template>

<script>
import MapContainer from './MapContainer'

export default {
  name: 'Mapbox',

  components: { MapContainer },

  filters: {},

  props: {},

  data() {
    return {}
  },

  computed: {},

  watch: {},

  created() {},

  mounted() {},

  updated() {},

  activated() {},

  deactivated() {},

  beforeDestroy() {},

  methods: {
    onMapLoad(map) {
      // console.log('map: ', map)
    }
  }
}
</script>

<style lang="less">
@import '~mapbox-gl/dist/mapbox-gl.css';
.mapbox {
  .map-container {
    height: 800px;
  }
}
</style>
