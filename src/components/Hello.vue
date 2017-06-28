<template>
  <div class="hello">
    <div id="main" class="china-map"></div>
  </div>
</template>

<script>
var echarts = require('echarts')
import { options } from '../lib/map.js'
import { chinaJson } from '../lib/china.js'

export default {
  name: 'hello',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  mounted () {
    echarts.registerMap('china', chinaJson)
    var myChart = echarts.init(document.getElementById('main'))
    // 绘制图表
    myChart.setOption(options)

    let currentIndex = -1
    setInterval(function () {
      var dataLen = options.series[0].data.length
      // 取消之前高亮的图形
      myChart.dispatchAction({
        type: 'downplay',
        seriesIndex: 0,
        dataIndex: currentIndex
      })
      currentIndex = (currentIndex + 1) % dataLen
      // 高亮当前图形
      myChart.dispatchAction({
        type: 'highlight',
        seriesIndex: 0,
        dataIndex: currentIndex
      })
      // 显示 tooltip
      myChart.dispatchAction({
        type: 'showTip',
        seriesIndex: 0,
        dataIndex: currentIndex
      })
    }, 1000)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
.hello{
  width: 100%;
  height: 100%; 
}
.china-map{
  width: 100%;
  height: 100%;
}
</style>
