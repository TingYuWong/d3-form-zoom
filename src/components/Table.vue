<template>
  <div class="table-wrapper">
    <div class="tableHeader">
      <div v-for="(headerValue, headerKey, headerIdx) in headerNameObj"
        :key="headerIdx" 
        :class="headerValue">{{ headerKey }}
      </div>
    </div>
    <div class="hr"></div>
    <div class="tableContent" v-for="(fakeObj, fakeIdx) in fakeData" :key="fakeIdx">
      <div v-for="(fakeValue, fakeKey, idx) in fakeObj" :key="idx" :class="fakeKey">
        {{ fakeValue }}
      </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'Table',
  data() {
    return {
      headerNameObj: {
        '管路名稱': 'tubeName',
        '材料名稱': 'materialName',
        '材質': 'tubeType',
        '部位': 'tubePart',
        '尺寸': 'tubeSize',
        '編號': 'tubeNumb',
        '置入日期': 'inDate',
        '拔管日期': 'outDate',
        '天數': 'tubeDays',
        '備註': 'tubeMemo',
      },
      fakeData: [
        {
          tubeName: 'Foley catheter  2way',
          materialName: '367341#25G *0.7主動回縮式翼型薄壁安全針',
          tubeType: '一般材質',
          tubePart: '泌尿道',
          tubeSize: '14',
          tubeNumb: '1號',
          inDate: '2022-04-01 8:00',
          outDate: '2022-04-30 8:00',
          tubeDays: '30天',
          tubeMemo: 'Hi My name is Abaracab',
        },
        {
          tubeName: 'Foley catheter  2way',
          materialName: '367341#25G *0.7主動回縮式翼型薄壁安全針',
          tubeType: '一般材質',
          tubePart: '泌尿道',
          tubeSize: '14',
          tubeNumb: '1號',
          inDate: '2022-04-01 8:00',
          outDate: '2022-04-30 8:00',
          tubeDays: '30天',
          tubeMemo: '',
        }
      ],
    }
  }
}
</script>

<style scoped>
.table-wrapper {
  margin-top: 10px;
}

.tableHeader {
  display: flex;
  text-align: left;
  font: normal normal normal 14px/16px Arial;
  color: #444444;
  height: 40px;
  line-height: 1.5;
  background-color: #EDF5F9;
  align-items: center;
  padding-left: 10px;
}

.tubeName, .materialName {
  width: calc((100% / 20) * 4);
  padding-right: 10px;
}

.tubeType, .tubePart {
  width: calc((100% / 20)* 1.5);
  padding-right: 10px;
}

.tubeSize, .tubeNumb, .tubeDays {
  width: calc((100% / 20) * 1);
  padding-right: 10px;
}

.inDate, .outDate, .tubeMemo {
  width: calc((100% / 20) * 2);
  padding-right: 10px;
}

.tubeMemo {
  /* 會斷掉英文單字 但可以不讓備註跑版 */
  word-break: break-all;
}

.tableContent {
  display: flex;
  text-align: left;
  align-items: center;
  line-height: 1.5;
  min-height: 50px;
  border-bottom: 1px solid #EAECFA;
  font: normal normal normal 16px/20px Arial;
  color: #222222;
  padding: 5px 0px 5px 10px;
}

.hr {
  width: 100%;
  margin-top: 10px;
  border-top: 1px solid #EAECFA;
}
</style>