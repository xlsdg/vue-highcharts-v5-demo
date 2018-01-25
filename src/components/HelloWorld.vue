<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <div class="charts">
      <div>
        <button @click="onClick">Random</button>
      </div>
      <div class="highcharts" :style="styles">
        <IHighCharts
          :options="options"
          :loading="loading"
          :resizable="true"
          @load="onLoad"
          @resize="onResize"
        />
      </div>
    </div>
  </div>
</template>

<script>
import _ from 'lodash'
import IHighCharts from 'vue-highcharts-v5/src/HighCharts.js'

function getRndNum (len = 8) {
  const data = []
  for (let i = 0, min = 0, max = 99999; i < len; i++) {
    data.push(Math.floor(Math.random() * (max + 1 - min) + min))
  }
  return data
}

export default {
  name: 'HelloWorld',
  components: {
    IHighCharts
  },
  data: () => ({
    msg: 'Welcome to Your Vue.js App',
    styles: {},
    loading: true,
    options: {
      title: {
        text: 'Solar Employment Growth by Sector, 2010-2016'
      },
      subtitle: {
        text: 'Source: thesolarfoundation.com'
      },
      yAxis: {
        title: {
          text: 'Number of Employees'
        }
      },
      series: [{
        name: 'Installation',
        data: [43934, 52503, 57177, 69658, 97031, 119931, 137133, 154175]
      }, {
        name: 'Manufacturing',
        data: [24916, 24064, 29742, 29851, 32490, 30282, 38121, 40434]
      }, {
        name: 'Sales & Distribution',
        data: [11744, 17722, 16005, 19771, 20185, 24377, 32147, 39387]
      }, {
        name: 'Project Development',
        data: [null, null, 7988, 12169, 15112, 22452, 34400, 34227]
      }, {
        name: 'Other',
        data: [12908, 5948, 8105, 11248, 8989, 11816, 18274, 18111]
      }]
    }
  }),
  methods: {
    onLoad (instance, HighCharts) {
      console.log(instance, HighCharts)
    },
    onResize (width, height) {
      console.log(width, height)
    },
    onClick () {
      const that = this

      const opts = _.cloneDeep(that.options)
      opts.series[0].data = getRndNum(8)
      opts.series[1].data = getRndNum(8)
      opts.series[2].data = getRndNum(8)
      opts.series[3].data = getRndNum(8)
      opts.series[4].data = getRndNum(8)
      that.options = opts

      that.styles = {
        width: Math.floor(Math.random() * (1024 + 1 - 400) + 400) + 'px',
        height: Math.floor(Math.random() * (768 + 1 - 200) + 200) + 'px'
      }

      that.loading = !that.loading
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

.charts {
  width: 1024px;
  height: 768px;
  margin: 0 auto;
}

.highcharts {
  width: 600px;
  height: 400px;
  border: 1px solid #000;
}
</style>
