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

var geojsonFeature = {
  type: "FeatureCollection",
  features: [
    {
      type: "Feature",
      properties: {
        name: "The Chamber of Mines Building",
        popupContent: "The Chamber of Mines Building",
        id: 0,
        styleid: 1
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.026670217514038, -26.19134352734578],
            [28.026729226112362, -26.191767125729683],
            [28.026643395423886, -26.191786380165073],
            [28.026697039604187, -26.19204150113358],
            [28.0270779132843, -26.19199336514455],
            [28.027067184448242, -26.19195485633902],
            [28.02739977836609, -26.19192116112372],
            [28.027292490005493, -26.191271322922137],
            [28.026670217514038, -26.19134352734578]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Flower Hall",
        popupContent: "Flower Hall - No Data",
        id: 1,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.025929927825928, -26.19151200416024],
            [28.025962114334106, -26.191950042737417],
            [28.026278614997864, -26.191901906710605],
            [28.026192784309387, -26.19148312243793],
            [28.025929927825928, -26.19151200416024]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "High Voltage Laboratory",
        popupContent: "High Voltage Laboratory - No Data",
        id: 2,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.025683164596558, -26.19152644501871],
            [28.025720715522766, -26.19174787129111],
            [28.02588164806366, -26.191738244070628],
            [28.02583336830139, -26.191492749679494],
            [28.025683164596558, -26.19152644501871]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Genmin Laboratories",
        popupContent: "Genmin Laboratories - No Data",
        id: 3,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.02561342716217, -26.191213559350995],
            [28.025650978088375, -26.191468681574094],
            [28.0263215303421, -26.191396477228018],
            [28.026278614997864, -26.191189491187913],
            [28.026214241981506, -26.191189491187913],
            [28.026198148727417, -26.191150982116604],
            [28.025978207588196, -26.191170236653846],
            [28.025988936424252, -26.191213559350995],
            [28.025903105735775, -26.191228000246475],
            [28.02589237689972, -26.191184677554684],
            [28.02561342716217, -26.191213559350995]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Wits Science Stadium",
        popupContent: "Wits Science Stadium",
        id: 4,
        styleid: 2
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.026541471481323, -26.190924741065615],
            [28.026509284973145, -26.190741822447844],
            [28.026552200317383, -26.19073219514421],
            [28.026536107063293, -26.190626294751766],
            [28.025693893432617, -26.19072256783979],
            [28.025693893432617, -26.19076107705271],
            [28.0256187915802, -26.19077070435395],
            [28.025559782981873, -26.190746636099355],
            [28.02549540996551, -26.190688872268023],
            [28.025463223457336, -26.19061185378171],
            [28.025457859039307, -26.19054927622407],
            [28.025484681129456, -26.19050113961841],
            [28.025543689727783, -26.190433748337043],
            [28.025318384170532, -26.190164182821754],
            [28.025200366973877, -26.190270083634285],
            [28.02512526512146, -26.190395239015906],
            [28.025087714195248, -26.190530021584195],
            [28.025087714195248, -26.19066480399652],
            [28.02513599395752, -26.1908284681447],
            [28.02524328231811, -26.19094880928342],
            [28.025447130203247, -26.191083591211207],
            [28.02550077438354, -26.19099213206293],
            [28.025559782981873, -26.1910162002668],
            [28.025699257850647, -26.191030641186746],
            [28.026541471481323, -26.190924741065615]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "TW Mathematical Sciences Building",
        popupContent: "TW Mathematical Sciences Building - No Data",
        id: 5,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.026745319366455, -26.190737008796116],
            [28.026986718177795, -26.190717754187272],
            [28.026933073997498, -26.1901064187016],
            [28.026552200317383, -26.19011604605695],
            [28.026525378227234, -26.19005346823297],
            [28.02684724330902, -26.19001014510436],
            [28.026820421218872, -26.189894616682658],
            [28.02633225917816, -26.189962008275906],
            [28.0263751745224, -26.190236387931648],
            [28.02660584449768, -26.19024601527626],
            [28.026745319366455, -26.190737008796116]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Wits Plus",
        popupContent: "Wits Plus - No Data",
        id: 6,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.026938438415527, -26.18987536193457],
            [28.026949167251587, -26.190005331422416],
            [28.02711009979248, -26.190043840872455],
            [28.027217388153073, -26.190024586149022],
            [28.027201294898987, -26.18987536193457],
            [28.027169108390808, -26.189841666117758],
            [28.026938438415527, -26.18987536193457]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Counselling Careers and Development Unit",
        popupContent: "Counselling Careers and Development Unit - No Data",
        id: 7,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.02656292915344, -26.19093918199691],
            [28.026573657989502, -26.191054709382666],
            [28.02709937095642, -26.190982504779996],
            [28.0270779132843, -26.190866977322614],
            [28.027238845825195, -26.190842909087916],
            [28.027195930480957, -26.190582971836204],
            [28.027029633522034, -26.190602226467337],
            [28.02705645561218, -26.19077070435395],
            [28.026777505874634, -26.190804399902042],
            [28.026782870292664, -26.190915113777123],
            [28.02656292915344, -26.19093918199691]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "FNB",
        popupContent: "FNB",
        id: 8,
        styleid: 3
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.025903105735775, -26.188378295527585],
            [28.025962114334106, -26.18885485573159],
            [28.02616596221924, -26.18883560081165],
            [28.026257157325745, -26.188955944009102],
            [28.026471734046936, -26.188994453806025],
            [28.02663266658783, -26.18889336556195],
            [28.026675581932068, -26.188792277230128],
            [28.02686870098114, -26.18875376736638],
            [28.02680432796478, -26.188267579241515],
            [28.02663266658783, -26.188291648008306],
            [28.026648759841915, -26.188407178019677],
            [28.026450276374817, -26.188431246757627],
            [28.026428818702698, -26.188262765487565],
            [28.026273250579834, -26.188277206748833],
            [28.026294708251953, -26.1884505017444],
            [28.02607476711273, -26.188469756728004],
            [28.026058673858643, -26.188359040528866],
            [28.025903105735775, -26.188378295527585]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "New Commerce Building",
        popupContent: "New Commerce Building - No Data",
        id: 9,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.026235699653622, -26.18969244166899],
            [28.026251792907715, -26.18977427445488],
            [28.026294708251953, -26.18977427445488],
            [28.0263215303421, -26.189909057741644],
            [28.027018904685974, -26.189827225050415],
            [28.026997447013855, -26.18969244166899],
            [28.027045726776123, -26.189687627973914],
            [28.027040362358093, -26.18962986361746],
            [28.026986718177795, -26.18962986361746],
            [28.026975989341732, -26.189538403327823],
            [28.026825785636902, -26.189552844430967],
            [28.026825785636902, -26.1895239622229],
            [28.026734590530396, -26.189538403327823],
            [28.026739954948425, -26.189562471832055],
            [28.026525378227234, -26.18959135403058],
            [28.026514649391174, -26.189557658131612],
            [28.026428818702698, -26.189562471832055],
            [28.026439547538757, -26.189596167729636],
            [28.026273250579834, -26.189615422523868],
            [28.026283979415894, -26.18968281427864],
            [28.026235699653622, -26.18969244166899]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "PIMD",
        popupContent: "PIMD - No Data",
        id: 10,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.023778796195984, -26.188455315490604],
            [28.02391290664673, -26.18946138408086],
            [28.024776577949524, -26.189350668824137],
            [28.02463173866272, -26.188349413028316],
            [28.023778796195984, -26.188455315490604]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "DJ Du Plesis",
        popupContent: "DJ Du Plesis - No Data",
        id: 11,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.02364468574524, -26.18813279405561],
            [28.023682236671444, -26.18844568799802],
            [28.024824857711792, -26.188286834255347],
            [28.024690747261047, -26.188118352776453],
            [28.024567365646362, -26.188055773879366],
            [28.02436888217926, -26.18798838118338],
            [28.02437961101532, -26.188041332590643],
            [28.02364468574524, -26.18813279405561]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "West Campus Village",
        popupContent: "West Campus Village - No Data",
        id: 12,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.023462295532227, -26.187415541693507],
            [28.02358567714691, -26.18777176153938],
            [28.024427890777584, -26.187762133990297],
            [28.024218678474426, -26.187352962418913],
            [28.023462295532227, -26.187415541693507]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Convocation Dining Hall",
        popupContent: "Convocation Dining Hall - No Data",
        id: 13,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.024073839187622, -26.187015996516397],
            [28.023982644081116, -26.187040065541755],
            [28.023982644081116, -26.18716041059395],
            [28.02436888217926, -26.187107458786308],
            [28.024315237998962, -26.18679937506443],
            [28.024052381515503, -26.186833071761185],
            [28.024073839187622, -26.187015996516397]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Barnato Hall",
        popupContent: "Barnato Hall - No Data",
        id: 14,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.024443984031677, -26.186780119804766],
            [28.02450835704803, -26.187232617565613],
            [28.024781942367554, -26.18720373478231],
            [28.024771213531494, -26.18713152779276],
            [28.025034070014954, -26.187112272587992],
            [28.025039434432983, -26.18718447958949],
            [28.025334477424618, -26.187145969194255],
            [28.025275468826294, -26.186683843458688],
            [28.024443984031677, -26.186780119804766]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Webster Hall",
        popupContent: "Webster Hall - No Data",
        id: 15,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.025650978088375, -26.186780119804766],
            [28.025699257850647, -26.187117086389488],
            [28.026643395423886, -26.186987113679404],
            [28.02658438682556, -26.18664533289799],
            [28.025650978088375, -26.186780119804766]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Hall 29",
        popupContent: "Hall 29 - No Data",
        id: 16,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.02558660507202, -26.186375758616645],
            [28.02561342716217, -26.186606822324553],
            [28.02659511566162, -26.18650091818198],
            [28.02655756473541, -26.18627466810033],
            [28.02558660507202, -26.186375758616645]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Olives and Plates",
        popupContent: "Olives and Plates - No Data",
        id: 17,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.02557051181793, -26.18572588948133],
            [28.025704622268677, -26.185889560568008],
            [28.026026487350464, -26.18570182018448],
            [28.025956749916077, -26.185629612264123],
            [28.02588701248169, -26.185697006324528],
            [28.025795817375183, -26.18560072908344],
            [28.02557051181793, -26.18572588948133]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "The Barns",
        popupContent: "The Barns - No Data",
        id: 18,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.02564024925232, -26.186168763655836],
            [28.02564024925232, -26.186265040427536],
            [28.025967478752136, -26.18621690205163],
            [28.026273250579834, -26.185985837570428],
            [28.02634298801422, -26.185817352763994],
            [28.026241064071655, -26.185774028060106],
            [28.026144504547116, -26.185976209873765],
            [28.025929927825928, -26.186125439082616],
            [28.02564024925232, -26.186168763655836]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Johannesburg Planetarium",
        popupContent: "Johannesburg Planetarium - No Data",
        id: 19,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.028123974800106, -26.188378295527585],
            [28.02810251712799, -26.188469756728004],
            [28.02814543247223, -26.188585286562738],
            [28.028231263160706, -26.18857084533966],
            [28.028231263160706, -26.188522707916484],
            [28.028258085250854, -26.188522707916484],
            [28.02829563617706, -26.188556404114806],
            [28.028365373611447, -26.18856121785662],
            [28.028429746627808, -26.18854196288814],
            [28.028467297554016, -26.188513080429455],
            [28.02854239940643, -26.18850345294163],
            [28.0285370349884, -26.188392736774528],
            [28.028467297554016, -26.188392736774528],
            [28.028419017791748, -26.188354226778692],
            [28.02835464477539, -26.188339785526967],
            [28.028274178504944, -26.188378295527585],
            [28.028247356414795, -26.188411991767662],
            [28.028220534324646, -26.188416805515455],
            [28.028204441070553, -26.1883734817782],
            [28.028123974800106, -26.188378295527585]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "William Cullen Library",
        popupContent: "William Cullen Library - No Data",
        id: 20,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.02913784980774, -26.19055890354282],
            [28.029186129570004, -26.19087179096896],
            [28.029604554176327, -26.1908284681447],
            [28.029550909996033, -26.190505953279867],
            [28.02913784980774, -26.19055890354282]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Wartenweilier Library",
        popupContent: "Wartenweilier Library - No Data",
        id: 21,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.03061306476593, -26.19089104555235],
            [28.030677437782284, -26.191362781851193],
            [28.031015396118164, -26.191329086464638],
            [28.030951023101807, -26.190857350029333],
            [28.03061306476593, -26.19089104555235]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Origins Centre",
        popupContent: "Origins Centre - No Data",
        id: 22,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.027957677841183, -26.19291275909642],
            [28.027979135513306, -26.192999403178433],
            [28.028016686439514, -26.192989776061385],
            [28.02804350852966, -26.193105301413368],
            [28.02814543247223, -26.19307160653088],
            [28.028182983398438, -26.193148623390822],
            [28.028258085250854, -26.19312455562756],
            [28.02829027175903, -26.193196758902424],
            [28.02859604358673, -26.19311011496721],
            [28.028478026390076, -26.192782792852533],
            [28.027957677841183, -26.19291275909642]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Senate House",
        popupContent: "Senate House - No Data",
        id: 23,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.029947876930237, -26.19243621549324],
            [28.030039072036743, -26.193061979419795],
            [28.030167818069458, -26.193042725195262],
            [28.03014636039734, -26.19292719978122],
            [28.03025901317596, -26.192917572658217],
            [28.030275106430054, -26.193018657410132],
            [28.030784726142883, -26.192965708265312],
            [28.030763268470764, -26.192879064158234],
            [28.03082764148712, -26.192864623467443],
            [28.03084909915924, -26.192956081145486],
            [28.030972480773926, -26.192946454024863],
            [28.03087592124939, -26.192330316649983],
            [28.03075790405273, -26.192344757407007],
            [28.030779361724854, -26.192498792037174],
            [28.030677437782284, -26.192513232773308],
            [28.030672073364254, -26.192421774747555],
            [28.030178546905514, -26.19246991055954],
            [28.030200004577637, -26.19257580927587],
            [28.030103445053097, -26.19259025000246],
            [28.03007662296295, -26.192421774747555],
            [28.029947876930237, -26.19243621549324]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Physics Building",
        popupContent: "Physics Building - No Data",
        id: 24,
        styleid: 0
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.03082764148712, -26.191531258637806],
            [28.03086519241333, -26.191834516239645],
            [28.031546473503113, -26.191762312120343],
            [28.03149819374084, -26.191468681574094],
            [28.03082764148712, -26.191531258637806]
          ]
        ]
      }
    },
    {
      type: "Feature",
      properties: {
        name: "Great Hall",
        popupContent: "Great Hall",
        id: 25,
        styleid: 4
      },
      geometry: {
        type: "Polygon",
        coordinates: [
          [
            [28.029845952987667, -26.191796007381587],
            [28.029921054840088, -26.192402520417197],
            [28.03089737892151, -26.192262926426867],
            [28.030790090560913, -26.191656412664408],
            [28.029845952987667, -26.191796007381587]
          ]
        ]
      }
    }
  ]
};
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

    var myStyle = [
      {
        color: "#555555",
        weight: 5,
        opacity: 0.65
      },
      {
        color: "#ff7800",
        weight: 5,
        opacity: 0.65
      },
      {
        color: "#ff0000",
        weight: 5,
        opacity: 0.65
      },
      {
        color: "#0000ff",
        weight: 5,
        opacity: 0.65
      },
      {
        color: "#ff00ff",
        weight: 5,
        opacity: 0.65
      }
    ];

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

    var LineLabels = [
      "00:00",
      "01:00",
      "02:00",
      "03:00",
      "04:00",
      "05:00",
      "06:00",
      "07:00",
      "08:00",
      "09:00",
      "10:00",
      "11:00",
      "12:00",
      "13:00",
      "14:00",
      "15:00",
      "16:00",
      "17:00",
      "18:00",
      "19:00",
      "20:00",
      "21:00",
      "22:00",
      "23:00",
      "24:00"
    ];
    //var APICall = [Name, Data, Labels],[Name,Data,Labels]
    var APICall = [
      {
        name: "Current Consumption",
        data: [
          1,
          2,
          3,
          4,
          5,
          6,
          7,
          8,
          9,
          10,
          11,
          12,
          12,
          12,
          11,
          10,
          9,
          8,
          7,
          6,
          5,
          2,
          1,
          1
        ]
      },
      {
        name: "Average Consumption",
        data: [
          1,
          2,
          3,
          3,
          3,
          3,
          4,
          5,
          6,
          7,
          10,
          12,
          12,
          12,
          11,
          10,
          9,
          8,
          7,
          6,
          3,
          2,
          1,
          1
        ]
      },
      {
        name: "Grid",
        data: [
          1,
          2,
          3,
          4,
          5,
          6,
          6,
          6,
          6,
          5,
          6,
          7,
          7,
          7,
          7,
          7,
          7,
          7,
          7,
          6,
          5,
          2,
          1,
          1
        ]
      },
      {
        name: "Solar",
        data: [
          0,
          0,
          0,
          0,
          0,
          0,
          1,
          2,
          3,
          5,
          5,
          5,
          5,
          5,
          4,
          3,
          2,
          1,
          0,
          0,
          0,
          0,
          0,
          0
        ]
      },
      { name: "Pie", data: [121, 41] }
    ];
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
