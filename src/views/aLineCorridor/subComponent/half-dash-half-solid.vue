<template>
  <!-- grid中的x轴Y轴标线 axisPointer -->
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
      this.chart = echarts.init(this.$el)
      this.chart.setOption({
        title: {
          text: 'echarts折线图实线加虚线'
        },
        // 用formatter回调函数显示多项数据内容
        tooltip: {
          trigger: 'axis',
          formatter: function(params, ticket, callback) {
            var htmlStr = ''
            var valMap = {}
            for (var i = 0; i < params.length; i++) {
              var param = params[i]
              var xName = param.name // x轴的名称
              var seriesName = param.seriesName // 图例名称
              var value = param.value // y轴值
              var color = param.color // 图例颜色

              // 过滤无效值
              if (value === '-') {
                continue
              }
              // 过滤重叠值
              // eslint-disable-next-line
              if (valMap[seriesName] == value) {
                continue
              }

              if (i === 0) {
                htmlStr += xName + '<br/>' // x轴的名称
              }
              htmlStr += '<div>'
              // 为了保证和原来的效果一样，这里自己实现了一个点的效果
              htmlStr += '<span style="margin-right:5px;display:inline-block;width:10px;height:10px;border-radius:5px;background-color:' + color + ';"></span>'
              // 圆点后面显示的文本
              htmlStr += seriesName + '：' + value
              htmlStr += '</div>'
              valMap[seriesName] = value
            }
            return htmlStr
          }
        },
        legend: {
          data: ['在线数']
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        toolbox: {
          feature: {
            saveAsImage: {}
          }
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
        },
        yAxis: {
          type: 'value'
        },
        series: [
          {
            name: '在线数',
            type: 'line',
            data: [120, 132, 191, '-', '-', '-', '-']
          },
          {
            name: '在线数',
            type: 'line',
            smooth: false, // 关键点，为true是不支持虚线，实线就用true
            itemStyle: {
              normal: {
                lineStyle: {
                  width: 2,
                  type: 'dotted' // 'dotted'虚线 'solid'实线
                }
              }
            },

            data: ['-', '-', 191, 234, 190, '-', '-']
          },
          {
            name: '在线数',
            type: 'line',
            data: ['-', '-', '-', '-', 190, 330, '-']
          },
          {
            name: '在线数',
            type: 'line',
            smooth: false, // 关键点，为true是不支持虚线，实线就用true
            itemStyle: {
              normal: {
                lineStyle: {
                  width: 2,
                  type: 'dotted' // 'dotted'虚线 'solid'实线
                }
              }
            },

            data: ['-', '-', '-', '-', '-', 330, 410]
          }

        ]
      })
    }
  }
}
</script>
