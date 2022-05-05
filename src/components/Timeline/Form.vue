<template>
  <div class="wrap" ref="wrap">
    <div class="form-title" ref="formTitle">
      <div class="title" v-for="(item, index) in titleArr" :key="index">{{ item }}</div>
    </div>
    <svg class="form-svg" width="760" height="100%">
      <g class="form-grid" />
      <g class="form-data">
        <line class="now-time" />
      </g>
    </svg>
  </div>
</template>

<script>
import * as d3 from 'd3'
import data from './data'

export default {
  name: 'Form',
  props: ['svgWidth', 'xScale', 'titleArr', 'zoomX'],
  data() {
    return {
      zoom: null,
      tubeTypeColor: {
        '一般': '#1E5670',
        '矽質': '#00A1DD',
        '金屬製': '#F89B05',
      },
    }
  },
  mounted() {
    this.drawForm()

    let svg = d3.select('.form-svg')
    this.zoom = d3.zoom().on("zoom", this.panX)
    svg.call(this.zoom).on("dblclick.zoom", null)
    
    this.drawData()

  },
  watch: {
    zoomX() {
      this.drawForm()
    },
  },
  methods: {
    drawForm() {
      this.$nextTick(() => {
        this.setFormHeight()
        this.drawGrid()
      })
    },
    setFormHeight() {
      this.$refs.wrap.style.height = this.titleArr.length * 30 + 'px'
    },
    drawGrid() {
      d3.select(".form-grid")
        .attr("stroke", "#B4B9D8")
        .attr("stroke-opacity", 1.0)
        .call(
          g =>
            g.selectAll(".grid-x")
              .data(this.zoomX.ticks(d3.timeDay.every(1)))
              .join(
                enter =>
                  enter
                    .append("line")
                    .attr("class", "grid-x")
                    .attr("stroke", "#737895")
                    .attr("stroke-width", "1")
                    .attr("y1", 0)
                    .attr("y2", '100%'),
                update => update,
                exit => exit.remove()
              )
              .attr("x1", d => this.zoomX(d) - 1)
              .attr("x2", d => this.zoomX(d) - 1)
        )
        .call(g => 
            g.selectAll('.grid-y')
              .data(this.titleArr.map((item, index) => index * 30))
              .join(
                enter => enter.append('line')
                              .attr('class', 'grid-y')
                              .attr('stroke', '#737895')
                              .attr('stroke-width', '1')
                              .attr('x1', 0)
                              .attr('x2', this.svgWidth - 240)
                              .attr('y1', d => d - 0.5)
                              .attr('y2', d => d - 0.5),
                update => update,
                exit => exit.remove()
              )
        )
    },
    panX(e) {
      let t = d3.zoomIdentity.translate(e.transform.x, 0).scale(1)
      let newScale = t.rescaleX(this.xScale)
      this.$emit('update:zoomX', newScale)
      d3.select('.form-data').attr("transform", t);
    },
    drawData() {
      d3.select(".form-data").call( g => 
        g.selectAll('.data-wrap').data(data).join(
          enter =>
            enter
              .append("g")
              .attr("class", "data-wrap")
              .call(g => g.append("line")
                    .attr("class", "tube-line")
                    .attr("stroke", d => this.tubeTypeColor[d.type])
                    .attr("stroke-width", "3")
                    .attr("x1", d => this.zoomX(d.stim) + 5)
                    .attr("x2", this.zoomX(new Date(2022, 5, 1)))
                    .attr("y1", d => d.id * 30 - 10)
                    .attr("y2", d => d.id * 30 - 10)
              )
              .call(g => g.append("circle")
                    .attr("class", "tube-circle")
                    .attr('fill', '#EA0327')
                    .attr("cx", d => this.zoomX(d.stim))
                    .attr("cy", d => d.id * 30 - 10)
                    .attr("r", 3)
              ),
          update => update,
          exit => exit.remove()
        )  
      )

      d3.select('.now-time')
        .attr('x1', this.zoomX(new Date(2022, 5, 1)))
        .attr('x2', this.zoomX(new Date(2022, 5, 1)))
        .attr('y1', 0)
        .attr('y2', "100%")
        .attr('stroke', '#6EC856')
        .attr('stroke-width', "6")

    },
  },
}
</script>

<style scoped>
.wrap {
  display: flex;
  height: 60px;
}

.form-title {
  width: 240px;
  height: 100%;
  box-sizing: border-box;
  border: 2px solid #737895;
  border-right: none;
}

svg {
  box-sizing: border-box;
  border: 2px solid #737895;
}

.title {
  display: flex;
  align-items: center;
  justify-content: flex-start;
  box-sizing: border-box;
  line-height: 1.8;
  padding-left: 10px;
  height: 30px;
}

.title:not(:last-child) {
  border-bottom: 1px solid #737895;
}
</style>