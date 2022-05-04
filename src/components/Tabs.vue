<template>
  <div>
    <div class="tabs-wrap">
      <div class="title">管路資訊頁</div>
      <div class="tabs">
        <div 
          class="subTab" :class="{ active: chosenTab === tab }"
          v-for="(tab, tIdx) in tabsArr" :key="tIdx"
          @click="$emit('update:chosenTab', tab)"
        >
          {{ tabNameObj[tab] }}
        </div>
      </div>
      <div class="space"></div>
    </div>
    <hr />
  </div>
</template>

<script>
export default {
  name: 'Tabs',
  props: ['chosenTab'],
  data() {
    return {
      tabsArr: ['Timeline', 'Table'],
      tabNameObj: {
        'Timeline': 'TimeLine',
        'Table': '管路歷程'
      }
    }
  },
}
</script>

<style scoped>
.tabs-wrap {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.tabs {
  display: flex;
  justify-content: center;
}

.space {
  width: 90px;
}

.title {
  font: normal normal bold 18px/21px Arial;
  color: #1E5670;
}

.subTab {
  font: normal normal normal 16px/18px Arial;
  color: #444444;
  background-color: #FFFFFF;
  border-radius: 10px 10px 0px 0px;
  width: 150px;
  height: 46px;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  position: relative;
}

.subTab:hover, .subTab.active{
  font: normal normal bold 16px/18px Arial;
  color: #FFFFFF;
  background-color: #4198B9;
}

.subTab:first-child {
  margin-right: 3px;
}

.subTab:first-child:after {
  content: "";
  display: block;
  width: 1px;
  height: 20px;
  background-color: #e6e7f0;
  right: -2px;
  top: 15px;
  position: absolute;
}

hr {
  margin: 0;
  border: 1px solid #4198B9;
}
</style>