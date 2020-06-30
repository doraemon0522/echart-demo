<template>
  <div :class="className" :style="{height:height,width:width}" />
</template>
<script>
import echarts from 'echarts'
export default {
  props: {
    className: {
      type: String,
      default: 'chart'
    },
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '300px'
    }
  },
  data() {
    return {
      chart: null
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.initChart()
    })
  },
  beforeDestroy() {
    if (!this.chart) {
      return
    }
    this.chart.dispose()
    this.chart = null
  },
  methods: {
    initChart() {
      // typeName 'right' | 'left'
      // const labelConfig = (typeName) => {
      //   return {
      //     normal: {
      //       position: typeName
      //     }
      //   }
      // }
      // 只有一个元素时，可this.$el，组件里多个标签时，用ref去定位找dom
      this.chart = echarts.init(this.$el)

      this.chart.setOption({
        // title: {
        //   text: '交错正负轴标签',
        //   subtext: 'From ExcelHome',
        //   sublink: 'http://e.weibo.com/1341556070/AjwF2AgQm'
        // },
        tooltip: {
          trigger: 'axis',
          axisPointer: { // 坐标轴指示器，坐标轴触发有效
            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
          },
          formatter: (params) => { // 改鼠标悬浮提示值格式
            var relVal = params[0].name + '<br/>'
            params.forEach(item => {
              relVal += item.seriesName + ' : ' + Math.abs(item.value) + '<br/>'
            })
            return relVal
          }
        },
        grid: {
          top: 80,
          bottom: 30
        },
        xAxis: {
          type: 'value',
          position: 'bottom',
          splitLine: {
            lineStyle: {
              type: 'dashed'
            }
          },
          axisLabel: {
            formatter: (value) => {
              return Math.abs(value)
            }
          }
        },
        yAxis: {
          type: 'category',
          axisLine: {
            show: false
          },
          axisLabel: {
            show: false
          },
          axisTick: {
            show: false
          },
          splitLine: {
            show: false
          },
          data: ['ten', 'nine', 'eight', 'seven', 'six', 'five', 'four', 'three', 'two', 'one']
        },
        series: [{
          name: '收入',
          type: 'bar',
          stack: '总量',
          label: {
            normal: {
              show: false,
              formatter: '{b}'
            }
          },
          data: [320, 302, 341, 374, 390, 450, 420, 290, 300, 310]
        }, {
          name: '支出',
          type: 'bar',
          stack: '总量',
          label: {
            normal: {
              show: true,
              formatter: '{b}',
              // formatter: (value) => {
              //   return Math.abs(value.data)
              // },
              position: 'right'
            }
          },
          data: [-120, -132, -101, -134, -190, -230, -210, -230, -290, -218]
        }]
      })
    }
  }
}
</script>
