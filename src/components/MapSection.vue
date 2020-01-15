<template>
  <div class="map-container">
    <MglMap id="map" :accessToken="accessToken" :mapStyle="mapStyle" :center="latlng">
      <MglMarker v-if="latlng" :coordinates="latlng" color="red"/>
      <div v-if="!latlng">
        <!-- <div v-for="(country, index) in countries" :key="index">
          <MglMarker :latlng="country.latlng" color="red"/>
        </div>-->
      </div>
    </MglMap>
  </div>
</template>

<script>
import Mapbox from "mapbox-gl";
import { MglMap, MglMarker } from "vue-mapbox";

export default {
  components: {
    MglMap,
    MglMarker
  },
  props: {
    latlng: Array,
    countries: Array
  },
  data: () => ({
    accessToken:
      "pk.eyJ1IjoiY2FybG9zd2lyYW1hIiwiYSI6ImNqczF2NTY5dTBndW0zeW84b2FkOXoycjUifQ.dk9hEA-DiCXpgWiNuVg1ag",
    mapStyle: "mapbox://styles/carloswirama/ck5fhyako0wl81iob0awvig0m"
  }),

  created() {
    // We need to set mapbox-gl library here in order to use it in template
    this.mapbox = Mapbox;
  }
};
</script>
<style scoped>
#map {
  position: absolute;
  top: 0;
  bottom: 0;
  width: 100%;
  flex: 1;
}
.map-container {
  position: relative;
  display: flex;
  flex-direction: column;
  padding: 4px 0;
}
</style>
