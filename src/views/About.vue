<template>
<div class="about">
  <div id="map"></div>
</div>
</template>

<script>
import Map from "ol/Map"
import View from "ol/View"
import TileLayer from "ol/layer/Tile"
import XYZ from "ol/source/XYZ"
import {
  Image as ImageLayer
} from 'ol/layer';
import {
  TileArcGISRest,
  ImageArcGISRest
} from 'ol/source';
import 'ol/ol.css'

export default {
  mounted() {
    this.initMap()
  },
  methods: {
    initMap() {
      new Map({
        target: "map",
        layers: [
          new TileLayer({
            source: new XYZ({
              // tilePixelRatio: 1,
              url: 'http://webst0{1-4}.is.autonavi.com/appmaptile?lang=zh_cn&size=1&scale=1&style=7&x={x}&y={y}&z={z}',

            }),
          }),
          new ImageLayer({
            source: new ImageArcGISRest({
              ratio: 1,
              params: {},
              url: 'http://59.110.28.240:6080/arcgis/rest/services/ceshi/yanhua/MapServer'
            })
          }),
          new TileLayer({
            extent: [-13884991, 2870341, -7455066, 6338219],
            source: new TileArcGISRest({
              url: 'https://sampleserver1.arcgisonline.com/ArcGIS/rest/services/Specialty/ESRI_StateCityHighway_USA/MapServer',
            })
          })
        ],
        view: new View({
          center: [11801491, 4685733],
          zoom: 4
        })
      });
    }
  }
}
</script>

<style lang="css">
.about {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
}

#map {
  width: 100%;
  height: auto;
  background-color: transparent;
  flex-grow: 1;
}
</style>
