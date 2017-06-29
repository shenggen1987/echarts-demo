<template>
  <div class="hello">
    <div id="main" class="china-map"></div>
  </div>
</template>

<script>
// var echarts = require('echarts')
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

    // var currentIndex = -1
    // setInterval(function () {
    //   var dataLen = options.series[0].data.length
    //   console.log(currentIndex)
    //   // 取消之前高亮的图形
    //   myChart.dispatchAction({
    //     type: 'downplay',
    //     seriesIndex: 0,
    //     dataIndex: currentIndex
    //   })
    //   currentIndex = (currentIndex + 1) % dataLen
    //   // 高亮当前图形
    //   myChart.dispatchAction({
    //     type: 'highlight',
    //     seriesIndex: 0,
    //     dataIndex: currentIndex
    //   })
    //   // 显示 tooltip
    //   myChart.dispatchAction({
    //     type: 'showTip',
    //     seriesIndex: 0,
    //     dataIndex: currentIndex
    //   })

    //   // myChart.setOption({
    //   //   series: [{
    //   //     center: options.series[0].data[currentIndex].coord,
    //   //     zoom: 4,
    //   //     data: [
    //   //         {name: options.series[0].data[currentIndex].name, selected: true}
    //   //     ],
    //   //     animationDurationUpdate: 1000,
    //   //     animationEasingUpdate: 'cubicInOut'
    //   //   }]
    //   // })
    // }, 1000)

    var bmap = myChart.getModel().getComponent('bmap').getBMap()
    bmap.addControl(new BMap.MapTypeControl())
    var myIcon = new BMap.Icon('http://banana001.w221.mc-test.com/Content/img/marker.png', new BMap.Size(1, 1))
    var arr = [
      {
        title: '美的空调',
        x: 91.1865,
        y: 30.1465
      },
      {
        title: '亚士漆',
        x: 116.0046,
        y: 28.6633
      }
    ]
    var currentIndex = -1
    setInterval(function () {
      var dataLen = arr.length
      currentIndex = (currentIndex + 1) % dataLen
      var dd = arr[currentIndex]
      var marker1 = new BMap.Marker(new BMap.Point(dd.x, dd.y), { icon: myIcon })
      bmap.addOverlay(marker1)
      var infoWindow1 = new BMap.InfoWindow(dd.title + '<br>合同金额: 1210万<br>签约时间: 2017-06-28')
      marker1.openInfoWindow(infoWindow1)
    }, 2000)
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
