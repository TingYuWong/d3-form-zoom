<template>
  <div class="axis-wrap">
    <svg class="axisSvg" height="45" :width="svgWidth">
      <rect class="axisRect" width="100%" height="100%"/>
      <text x="10" y="30">Tube</text>
      <text x="150" y="30">Date</text>
      <g class="month-axis"/>
      <g class="day-axis"/>
      <line class="axisLine" x1="0" y1="44" x2="100%" y2="44"/>
    </svg>
  </div>
</template>

<script>
import * as d3 from "d3"

export default {
  name: 'Axis',
  props: ['xScale', 'svgWidth', 'zoomX'],
  data() {
    return {
      axisHeight: 45,
      setMonthObj: {
        '01': '1月',
        '02': '2月',
        '03': '3月',
        '04': '4月',
        '05': '5月',
        '06': '6月',
        '07': '7月',
        '08': '8月',
        '09': '9月',
        '10': '10月',
        '11': '11月',
        '12': '12月'
      }
    }
  },
  mounted() {
    this.drawMonthAxis()
    this.drawDayAxis()
  },
  watch: {
    zoomX() {
      this.drawMonthAxis()
      this.drawDayAxis()
    },
  },
  methods: {
    drawDayAxis() {
      d3.selectAll(".day-axis")
        .attr("transform", `translate(240,${this.axisHeight - 1})`)
        .style("font", "12px Arial")
        .call(
          d3
            .axisTop(this.zoomX)
            .tickSize(3)
            .tickPadding(8)
            .tickFormat(d3.timeFormat("%d"))
            .ticks(d3.timeDay.every(1))
        )
        .selectAll("text")
        .attr("color", (d) => {
          return new Date(d).getDate() % 5 == 0 ? "#737895" : "#B4B9D8";
        })
        .select("path")
        .attr("stroke", "none");
    },
    drawMonthAxis() {
      d3.selectAll(".month-axis")
        .attr("transform", `translate(240,${this.axisHeight - 20})`)
        .style("font", "12px Arial")
        .call(
          d3
            .axisTop(this.zoomX)
            .tickSize(0)
            .tickPadding(8)
            .tickFormat((tim, index) => {
              if (index === 0 || tim.getDate() === 1) {
                return this.setMonthObj[d3.timeFormat("%m")(tim)]
              }
              return ''
            })
            .ticks(d3.timeDay.every(1))
        )
        .select("path")
        .attr("stroke", "none");
    }
  }
}
</script>

<style scoped>
.axis-wrap {
  margin-top: 35px;
  margin-bottom: 20px;
}

text {
  font: normal normal normal 14px/16px Arial;
  fill: #444444;
}

.axisRect {
  fill: #EDF5F9;
}

.axisLine {
  stroke: #737895;
  stroke-width: 2;
}
</style>