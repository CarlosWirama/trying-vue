<template>
  <MglMap :accessToken="accessToken" :mapStyle="mapStyle"/>
</template>

<script>
import Mapbox from "mapbox-gl";
import { MglMap } from "vue-mapbox";

export default {
  components: {
    MglMap
  },
  props: {
    sources: Object
  },
  data: () => ({
    accessToken:
      "pk.eyJ1IjoiY2FybG9zd2lyYW1hIiwiYSI6ImNqczF2NTY5dTBndW0zeW84b2FkOXoycjUifQ.dk9hEA-DiCXpgWiNuVg1ag",
    mapStyle: {
      version: 8,
      name: "Mapbox Streets",
      sprite: "mapbox://sprites/mapbox/streets-v8",
      glyphs: "mapbox://fonts/mapbox/{fontstack}/{range}.pbf",
      sources: {
        "mapbox-streets": {
          type: "vector",
          url: "mapbox://mapbox.mapbox-streets-v6"
        }
      },
      layers: [
        {
          id: "water",
          source: "mapbox-streets",
          "source-layer": "water",
          type: "fill",
          paint: {
            "fill-color": "#00ffff"
          }
        }
      ]
    }
  }),

  created() {
    // We need to set mapbox-gl library here in order to use it in template
    this.mapbox = Mapbox;
  }
};
</script>
