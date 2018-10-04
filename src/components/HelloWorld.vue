<template>
  <div class="content">
    <div class="sidepanel">
      <h1>{{ msg }}</h1>
      <h2>This is a test</h2>
      <canvas id="myChart"></canvas>
    </div>
    <div id="map" ref="mapElement">
    </div>
  </div>
</template>

<script>
import L from 'leaflet'
import Chart from 'chart.js'
/* export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'This is the SidePanel'
    }
  }
} */
export default {
  mounted () {
    var map = L.map(this.$refs['mapElement']).setView([-26.18887, 28.02767], 17)
    map.dragging.disable()
    map.touchZoom.disable()
    map.doubleClickZoom.disable()
    map.scrollWheelZoom.disable()
    map.boxZoom.disable()
    map.zoomControl.remove()
    map.keyboard.disable()

    var polygon = L.polygon([
      [-26.18887, 28.02767],
      [-26.18777, 28.02857],
      [-26.18667, 28.02547]
    ]).addTo(map)

    /* polygon.setStyle({
      color: 'blue'
    }) */
    polygon.bindPopup('I am a polygon.')

    map.createPane('labels')
    map.getPane('labels').style.zIndex = 650
    map.getPane('labels').style.pointerEvents = 'none'
    /* L.tileLayer('http://{s}.basemaps.cartocdn.com/light_nolabels/{z}/{x}/{y}.png', {
      attribution: '©OpenStreetMap, ©CartoDB' }).addTo(map)
    L.tileLayer('http://{s}.basemaps.cartocdn.com/light_only_labels/{z}/{x}/{y}.png', {
      attribution: '©OpenStreetMap, ©CartoDB', pane: 'labels' }).addTo(map)
    var geojson = L.geoJson(GeoJsonData, geoJsonOptions).addTo(map)
    geojson.eachLayer(function (layer) { layer.bindPopup(layer.feature.properties.name) })
    map.fitBounds(geojson.getBounds()) */
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
      attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors' }).addTo(map)

    var ctx = document.getElementById('myChart').getContext('2d')
    var myChart = new Chart(ctx, {
      type: 'bar',
      data: {
        labels: ['Red', 'Blue', 'Yellow', 'Green', 'Purple', 'Orange'],
        datasets: [{
          label: '# of Votes',
          data: [12, 19, 3, 5, 2, 3],
          backgroundColor: [ 'rgba(255, 99, 132, 0.2)',
            'rgba(54, 162, 235, 0.2)',
            'rgba(255, 206, 86, 0.2)',
            'rgba(75, 192, 192, 0.2)',
            'rgba(153, 102, 255, 0.2)',
            'rgba(255, 159, 64, 0.2)' ],
          borderColor: [ 'rgba(255,99,132,1)',
            'rgba(54, 162, 235, 1)',
            'rgba(255, 206, 86, 1)',
            'rgba(75, 192, 192, 1)',
            'rgba(153, 102, 255, 1)',
            'rgba(255, 159, 64, 1)' ],
          borderWidth: 1 }] },
      options: { scales: { yAxes: [{ ticks: { beginAtZero: true } }] } }})
    // myChart.data =
  }
}
</script>

<!--
 <script src="https://unpkg.com/leaflet@1.3.4/dist/leaflet.js"
   integrity="sha512-nMMmRyTVoLYqjP9hrbed9S+FzjZHW5gY1TWCHA5ckwXZBadntCNs8kEqAWdrb9O7rxbCaA4lKTIWjDXZxflOcA=="
   crossorigin=""></script>-->

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.content {
  display: grid;
  grid-template-columns: 30% 70%;
  background-color: #000000;
  height: 100%
}

.sidepanel {
  /* border: 1px solid black; */
  background-color: #A0A0A0;
}

#map {
  height: 100%
}
</style>
