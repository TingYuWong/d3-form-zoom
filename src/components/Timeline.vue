<template>
  <div class="timeline-wrap">
    <button @click="changeTitleArr(3)">3</button>
    <button @click="changeTitleArr(6)">6</button>
    <Axis :xScale="xScale" :svgWidth="svgWidth" :zoomX="zoomX" />
    <Form :xScale="xScale" :svgWidth="svgWidth" :titleArr="titleArr" :zoomX.sync="zoomX" ref="Form" />
  </div>
</template>

<script>
import * as d3 from 'd3'
import Axis from '@/components/Timeline/Axis.vue'
import Form from '@/components/Timeline/Form.vue'

export default {
  name: 'Timeline',
  data() {
    return {
      svgWidth: 1000,
      defaultDays: 40,
      titleArr: ['Foley Catheter 2Way', 'Foley Catheter 2Way', 'Foley Catheter 2Way'],
      zoomX: null,
    }
  },
  beforeMount() {
    this.zoomX = this.xScale
  },
  components: {
    Axis,
    Form,
  },
  computed: {
    xScale() {
      let dt = new Date()
      let yyyy = dt.getFullYear()
      let month = dt.getMonth()
      let dd = dt.getDate()
      let st = new Date(yyyy, month, dd, 0, 0, 0).getTime()
      return d3.scaleTime()
               .domain([st, st + (30 * 24 * 60 * 60 * 1000)])
               .range([0, this.svgWidth - 240])
    },
  },
  methods: {
    changeTitleArr(num) {
      if(num == 3) {
        this.titleArr = ['', '', '']
      } else {
        this.titleArr = ['Foley Catheter 2Way', 'Foley Catheter 2Way', 'Foley Catheter 2Way',
         'Foley Catheter 2Way', 'Foley Catheter 2Way', 'Foley Catheter 2Way']
      }

      this.$refs.Form.drawForm()
    }
  },
}
</script>

<style scoped>
.timeline-wrap {
  display: flex;
  flex-direction: column;
  align-items: center;
}
</style>