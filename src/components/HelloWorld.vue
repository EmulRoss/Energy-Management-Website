<template>
  <div class="content">
    <div class="sidepanel">
      <h1 id="h101">No Selection</h1>
      <br>
      <br>
      <canvas id="myChart" style="visibility:hidden"></canvas>
      <canvas id="PieChart" style="visibility:hidden"></canvas>
    </div>
    <div id="map" ref="mapElement">
    </div>
  </div>
</template>

<script>
import L from "leaflet";
import Chart from "chart.js";
import Vue from "vue";
Vue.use(require("vue-resource"));
/* export default {
  name: 'HelloWorld',
  data () {
    return {
      msg: 'This is the SidePanel'
    }
  }
} */

var onPolyClick = function(event) {
  // GET /someUrl
  Vue.http.get("http://127.0.0.1:5000/").then(
    response => {
      // get body data
      console.log("Hello");
      console.log(someData);
      someData = response.bodyText;
      console.log(someData);
      polygon.bindPopup(someData);
    },
    response => {
      // error callback
    }
  );
};

//var geojsonFeature = {
//	data: null
//}
export default {
  mounted() {
    /*
	}*/
    var map = L.map(this.$refs["mapElement"]).setView(
      [-26.18887, 28.02767],
      17
    );
    map.dragging.disable();
    map.touchZoom.disable();
    map.doubleClickZoom.disable();
    map.scrollWheelZoom.disable();
    map.boxZoom.disable();
    map.zoomControl.remove();
    map.keyboard.disable();

      

var geojsonFeature = null
Vue.http.get("http://127.0.0.1:5000/daily/heatmap/").then(
    response => {
      // get body data
return response.json()
//console.log(geojsonFeature);

	
    },
    response => {
      // error callback
      console.log(response.status);
    }).then (result => {console.log(result)


    geojsonLayer = L.geoJSON(result, {
      //style: myStyle},{
      onEachFeature: function(feature, layer) {
        // does this feature have a property named popupContent?
        if (feature.properties && feature.properties.popupContent) {
          layer.bindPopup(feature.properties.popupContent);
          layer.on("click", function(event) {
            // GET /someUrl
            //var CurrentID = arguments
	    var CurrentCheck = feature.properties.popupContent.split("-")
            if (CurrentCheck[1] == " No Data") {
              document.getElementById("h101").innerHTML =
                feature.properties.popupContent;
              document.getElementById("myChart").style.visibility = "hidden";
              document.getElementById("PieChart").style.visibility = "hidden";
            } else {
              document.getElementById("h101").innerHTML =
                feature.properties.name;



var geojsonFeature = null
Vue.http.get("http://127.0.0.1:5000/daily/" + feature.properties.id.toString()).then(
    response => {
      // get body data
return response.json()
//console.log(geojsonFeature);

	
    },
    response => {
      // error callback
      console.log(response.status);
    }).then (result => {console.log(result)


    var APICall = result.features

   var LineLabels = result.labels

    var CurrentData = APICall[0];
    var AverageData = APICall[1];
    var GridData = APICall[2];
    var SolarData = APICall[3];
    var PieData = APICall[4];

    var ctx = document.getElementById("myChart").getContext("2d");
    var myChart = new Chart(ctx, {
      type: "bar",
      data: {
        labels: LineLabels,
        datasets: [
          {
            label: CurrentData.name,
            type: "line",
            borderColor: "rgba(255, 206, 86, 1)",
            data: CurrentData.data,
            fill: false
          },
          {
            label: AverageData.name,
            type: "line",
            borderColor: "rgba(75, 192, 192, 1)",
            data: AverageData.data,
            fill: false
          },
          {
            label: SolarData.name,
            type: "bar",
            yAxisID: "bar-stacked",
            backgroundColor: "rgba(54, 162, 235, 1)",
            data: SolarData.data
          },
          {
            label: GridData.name,
            type: "bar",
            yAxisID: "bar-stacked",
            backgroundColor: "rgba(255, 159, 64, 1)",
            data: GridData.data
          }
        ]
      },
      options: {
        scales: {
          xAxes: [{ stacked: true }],
          yAxes: [
            {
              stacked: false,
              ticks: { beginAtZero: true, min: 0, max: 20 }
            },
            {
              id: "bar-stacked",
              stacked: true,
              display: false,
              ticks: { beginAtZero: true, min: 0, max: 20 }
            }
          ]
        },
        title: {
          display: true,
          text: "Load Profile of Building"
        },
        ticks: {
          beginAtZero: true,
          min: 0,
          max: 20
        }
      }
    });

    var ctx = document.getElementById("PieChart").getContext("2d");
    var PieChart = new Chart(ctx, {
      type: "pie",
      data: {
        labels: ["Grid", "Solar"],
        datasets: [
          {
            label: "Percentage Supply",
            backgroundColor: ["rgba(255, 159, 64, 1)", "rgba(54, 162, 235, 1)"],
            data: PieData.data
          }
        ]
      },
      options: {
        title: {
          display: true,
          text: "Comparison of energy supply"
        }
      }
    });




})

              document.getElementById("myChart").style.visibility = "visible";
              document.getElementById("PieChart").style.visibility = "visible";
            }
          });
          layer.setStyle(feature.properties.styleid);
        }
      }
    }).addTo(map);
})
console.log("TEST")

//while (geojsonFeature == null){
// console.log("waiting")
//}
console.log(geojsonFeature)

    var geojsonLayer = L.geoJSON(geojsonFeature, {
      //style: myStyle},{
      onEachFeature: function(feature, layer) {
        // does this feature have a property named popupContent?
        if (feature.properties && feature.properties.popupContent) {
          layer.bindPopup(feature.properties.popupContent);
          layer.on("click", function(event) {
            // GET /someUrl
            //var CurrentID = arguments
            if (feature.properties.styleid == 0) {
              document.getElementById("h101").innerHTML =
                feature.properties.popupContent;
              document.getElementById("myChart").style.visibility = "hidden";
              document.getElementById("PieChart").style.visibility = "hidden";
            } else {
              document.getElementById("h101").innerHTML =
                feature.properties.name;
              document.getElementById("myChart").style.visibility = "visible";
              document.getElementById("PieChart").style.visibility = "visible";
            }
          });
          layer.setStyle(myStyle[feature.properties.styleid]);
        }
      }
    }).addTo(map);

    geojsonLayer.eachLayer(function(featureLayer) {
      //propertyValue = featureLayer.feature.properties["Event data"]
      //var myFillColor =
      //featureLayer.setStyle(featureLayer.feature.properties.style)
    });

    //polygon.bindPopup(someData)

    /* polygon.setStyle({
      color: 'blue'
    }) */

    //polygon.bindPopup(this.someData)

    map.createPane("labels");
    map.getPane("labels").style.zIndex = 650;
    map.getPane("labels").style.pointerEvents = "none";
    /* L.tileLayer('http://{s}.basemaps.cartocdn.com/light_nolabels/{z}/{x}/{y}.png', {
      attribution: '©OpenStreetMap, ©CartoDB' }).addTo(map)
    L.tileLayer('http://{s}.basemaps.cartocdn.com/light_only_labels/{z}/{x}/{y}.png', {
      attribution: '©OpenStreetMap, ©CartoDB', pane: 'labels' }).addTo(map)
    var geojson = L.geoJson(GeoJsonData, geoJsonOptions).addTo(map)
    geojson.eachLayer(function (layer) { layer.bindPopup(layer.feature.properties.name) })
    map.fitBounds(geojson.getBounds()) */
    L.tileLayer("https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png", {
      attribution:
        '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);

    //var APICall = [Name, Data, Labels],[Name,Data,Labels]


  }
};
</script>

<!--
 <script src="https://unpkg.com/leaflet@1.3.4/dist/leaflet.js"
   integrity="sha512-nMMmRyTVoLYqjP9hrbed9S+FzjZHW5gY1TWCHA5ckwXZBadntCNs8kEqAWdrb9O7rxbCaA4lKTIWjDXZxflOcA=="
   crossorigin=""></script>-->

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1,
h2 {
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
  grid-template-columns: 40% 60%;
  background-color: #000000;
  height: 100%;
}

.sidepanel {
  /* border: 1px solid black; */
  background-color: #ffffff; /*#a0a0a0;*/
}

#map {
  height: 100%;
}
</style>
