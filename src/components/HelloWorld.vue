<template>
  <div class="content">
    <div class="sidepanel">
      <h1>{{ msg }}</h1>
      <h2>This is a test</h2>
      <canvas id="myChart"></canvas>
      <canvas id="PieChart"></canvas>
    </div>
    <div id="map" ref="mapElement">
    </div>
  </div>
</template>

<script>
import L from 'leaflet'
import Chart from 'chart.js'
import Vue from 'vue'
Vue.use(require('vue-resource'))
/* export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'This is the SidePanel'
    }
  }
} */

    var polygon = L.polygon([
      [-26.18887, 28.02767],
      [-26.18777, 28.02857],
      [-26.18667, 28.02547]
    ])
var someData = "Hello"
var onPolyClick = 
	function(event){
	 // GET /someUrl
	    Vue.http.get('http://127.0.0.1:5000/').then(response => {

	      // get body data
		console.log("Hello")
	        console.log(someData)
	        someData = response.bodyText;
		console.log(someData)
		polygon.bindPopup(someData)
	    }, response => {
	      // error callback
	    });
}
export default {
  mounted () {
	/*
	}*/
    var map = L.map(this.$refs['mapElement']).setView([-26.18887, 28.02767], 17)
    map.dragging.disable()
    map.touchZoom.disable()
    map.doubleClickZoom.disable()
    map.scrollWheelZoom.disable()
    map.boxZoom.disable()
    map.zoomControl.remove()
    map.keyboard.disable()

    polygon.on('click', onPolyClick)
    polygon.addTo(map)
    //polygon.bindPopup(someData)
	
    /* polygon.setStyle({
      color: 'blue'
    }) */


    //polygon.bindPopup(this.someData)

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
        labels: ['1900', '1950', '2000', '2050'],
        datasets: [{
          label: 'Current Consumption',
	  type: 'line',
	  borderColor: 'rgba(255, 99, 132, 1)',
          data: [12, 19, 3, 5],
	  fill: false
	}, {
	  label: 'Average Consumption',
	  type: 'line',
	  borderColor: 'rgba(75, 192, 192, 1)',
	  data: [11, 12, 13, 14],
	  fill: false
	}, {
	  label: 'Grid',
	  type: 'bar',
	  yAxisID: 'bar-stacked',
          backgroundColor: 'rgba(153, 102, 255, 1)',
	  data: [12, 19, 3, 5],
	}, {
	  label: 'Solar',
	  type: 'bar',
	  yAxisID: 'bar-stacked',
	  backgroundColor: 'rgba(255, 206, 86, 1)',
	  data: [7, 12, 1, 2]
	}]
     },
     options: {
	scales: {
		xAxes: [{ stacked: true}],
		yAxes: [{ stacked: false,
			ticks: { beginAtZero: true, min: 0, max: 20}},{
			id: 'bar-stacked',
			stacked: true,
			display: false,
			ticks: { beginAtZero: true, min: 0, max: 20}}]
	},
	title: {
		display: true,
		text: 'Load Profile of Building'
	},
	ticks: {
		beginAtZero: true,
		min: 0,
		max: 20
	},
	}
     })

	var ctx = document.getElementById('PieChart').getContext('2d')
    	var PieChart = new Chart(ctx, {
		type: 'pie',
		data: {
			labels: ['Grid','Solar'],
			datasets: [{
				label: 'Percentage Supply',
				backgroundColor: ['rgba(153, 102, 255, 1)','rgba(255, 206, 86, 1)'],
				data: [2000,200]
			}]

		},
		options: {
			title: {
				display: true,
				text: 'Comparison of energy supply'
			}
		}
	})
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
