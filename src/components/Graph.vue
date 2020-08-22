<template>
  <div class="container" ref="chartdiv">
    
  </div>
</template>

<script>

import * as am4core from "@amcharts/amcharts4/core";
import am4themes_animated from "@amcharts/amcharts4/themes/animated";
import * as am4plugins_forceDirected from "@amcharts/amcharts4/plugins/forceDirected";

am4core.useTheme(am4themes_animated);

export default {
  name: 'Graph',
  mounted() {
    let chart = am4core.create(this.$refs.chartdiv, am4plugins_forceDirected.ForceDirectedTree);
    let networkSeries = chart.series.push(new am4plugins_forceDirected.ForceDirectedSeries())

    let data = [
          {
            name: "Informática",
            children: [
              { name: "Matemáticas", value: 200 },
              { name: "Sociología", value: 250 },
              { name: "Historia", value: 100 },
              { name: "Psicología", value: 300 },
              { name: "Lingüistica", value: 250 },
              { name: "Arquitectura", value: 200 },
              { name: "Economía", value: 260 },
              { name: "Psicología", value: 250 },
              { 
                name: "Medicina",
                children: [
                  { name: "Epidemiología", value: 50 }
                ]
              },
              {
                name: "Biología", 
                children: [
                  { name: "Bioingeniería", value: 50 },
                  { name: "Bioinformática", value: 50 },
                  { name: "Biotecnología", value: 50 }
                ]
              },
              { name: "Educación", value: 100 }
            ]
          }
        ];

    chart.data = data;
    networkSeries.nodes.template.label.fill = am4core.color("#424242");

    networkSeries.fontSize = 15;
    networkSeries.minRadius = 55;
    networkSeries.dataFields.value = "value";
    networkSeries.dataFields.children = "children";

    networkSeries.nodes.template.label.text = "{name}";
    networkSeries.links.template.strokeWidth = 2;

    let hoverState = networkSeries.links.template.states.create("hover");
    hoverState.properties.strokeWidth = 3;
    hoverState.properties.strokeOpacity = 1;

    networkSeries.nodes.template.events.on("over", function(event) {
      event.target.dataItem.childLinks.each(function(link) {
        link.isHover = true;
      })
      if (event.target.dataItem.parentLink) {
        event.target.dataItem.parentLink.isHover = true;
      }
    })

    networkSeries.nodes.template.events.on("out", function(event) {
      event.target.dataItem.childLinks.each(function(link) {
        link.isHover = false;
      })
      
      if (event.target.dataItem.parentLink) {
        event.target.dataItem.parentLink.isHover = false;
      }
    })
  }
}
  
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.container {
  width: 100%;
  height: 700px;
}
</style>
