<template>
  <div class="home">
    <Tabs :chosenTab.sync="chosenTab"/>
    <component :is="chosenTab" />
    <AddTube />
  </div>
</template>

<script>
// @ is an alias to /src
import Tabs from '@/components/Tabs.vue'
import Table from '@/components/Table.vue'
import Timeline from '@/components/Timeline.vue'
import AddTube from '@/components/AddTube.vue'

export default {
  name: 'Home',
  data() {
    return {
      chosenTab: 'Table'
    }
  },
  components: {
    Tabs, Table, AddTube, Timeline
  }
}
</script>

<style scoped>
  .home {
    padding: 9px 20px;
  }
</style>
