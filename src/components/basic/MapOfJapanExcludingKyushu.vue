<template>
  <div id="chartdiv"></div>
</template>

<script>
import * as am4core from "@amcharts/amcharts4/core"
import * as am4maps from "@amcharts/amcharts4/maps"
import am4geodata_japanHigh from "@amcharts/amcharts4-geodata/japanHigh"

export default {
  mounted() {
    let chart = am4core.create("chartdiv", am4maps.MapChart)
    chart.geodata = am4geodata_japanHigh
    let polygonSeries = chart.series.push(new am4maps.MapPolygonSeries())
    polygonSeries.mapPolygons.template.fill = am4core.color("#47c78a")
    polygonSeries.useGeodata = true
    polygonSeries.mapPolygons.template.events.on("hit", function(ev) {
      chart.zoomToMapObject(ev.target)
    })

    polygonSeries.exclude = [
      "JP-40",
      "JP-41",
      "JP-42",
      "JP-43",
      "JP-44",
      "JP-45",
      "JP-46",
      "JP-47",
    ]
  },
  beforeDestroy() {
    if (this.chart) {
      this.chart.dispose()
    }
  }
}
</script>
