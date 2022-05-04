<template>
  <div>
    <Axis :xScale="xScale" :svgWidth="svgWidth" />
    <Form :xScale="xScale" :svgWidth="svgWidth" />
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
    }
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
}
</script>

<style scoped>

</style>