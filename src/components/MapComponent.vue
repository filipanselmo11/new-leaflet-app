<template>
  <div id="map"></div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import "leaflet";
import "@geoman-io/leaflet-geoman-free";
import "@geoman-io/leaflet-geoman-free/dist/leaflet-geoman.css";

const L = window["L"];

delete L.Icon.Default.prototype._getIconUrl;
L.Icon.Default.mergeOptions({
  iconRetinaUrl: require("leaflet/dist/images/marker-icon-2x.png"),
  iconUrl: require("leaflet/dist/images/marker-icon.png"),
  shadowUrl: require("leaflet/dist/images/marker-shadow.png"),
});

export default {
  name: "MapComponent",
  data: () => ({
    map: null,
    tileLayer: null,
  }),
  mounted() {
    this.initMap();
  },
  methods: {
    initMap() {
      this.map = L.map("map").setView([-3.0775644689358153, -60.00820504065466], 13);
      this.tileLayer = L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
        maxZoom: 19,
        attribution:
          '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
      }).addTo(this.map);
    //   this.geomanToolbar();
    this.setDrawingTools();
    },

    setDrawingTools() {
      this.map.pm.addControls({
        position: "topright",
        drawMarker: true,
        drawCircleMarker: false,
        drawPolyline: false,
        drawRectangle: true,
        drawPolygon: true,
        drawCircle: true,
        drawText: false,
        editMode: true,
        dragMode: false,
        cutPolygon: false,
        removelMode: true,
        rotateMode: false,
        oneBlock: false,
        drawControls: true,
        editControls: true,
        customControls: true,
        optionsControls: true,
        pinningOption: true,
        snappingOption: true,
        splitMode: true,
        scaleMode: true,
      });
    },
    geomanToolbar() {
      // this.map.pm.controlsVisible(true);
      this.map.pm.toggleControls();
      //   this.map.pm.addControls({
      //     position: "topleft",
      //     drawCircle: true,
      //   });
      //   this.map.pm.removeControls();
    },
  },
};
</script>

<style scoped>
#map {
  height: 600px;
}
</style>
