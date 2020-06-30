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
      this.chart = echarts.init(this.$el)
      this.chart.setOption({
        /** 画布背景颜色 */
        // backgroundColor: '#05254D',
        tooltip: {},
        color: ['#fda3e1', '#32CD32'],
        legend: {
          data: ['预算分配', '实际开销']
        },
        radar: {
          radius: '50%',
          /** 每个指示器名称 */
          name: {
            /** 文字样式 */
            textStyle: {
              /** 蓝 */
              color: '#7ecdff',
              // backgroundColor: '#999',
              // borderRadius: 3,
              padding: [3, 5]
            }
          },
          /** 坐标轴线 样式 */
          axisLine: {
            lineStyle: {
              color: '#cccccc'
              // color: '#1C8CB3'
            }
          },
          /** grid区域的分割线 */
          splitLine: {
            lineStyle: {
              color: '#cccccc'
              // color: '#1C8CB3'
            }
          },
          indicator: [
            { name: '销售', max: 6500 },
            { name: '管理', max: 16000 },
            { name: '信息技术', max: 30000 },
            { name: '客服', max: 38000 },
            { name: '研发', max: 52000 },
            { name: '市场', max: 25000 }
          ],
          /** grid区域的分割区域（默认不展示，有字段就会去展示） */
          splitArea: {
            /** 默认true */
            show: true,
            areaStyle: {
              /** 数组,默认['rgba(250,250,250,0.3)','rgba(200,200,200,0.3)']即base当中的样式
               * 按数组中颜色的顺序依次循环设置颜色，一般是深浅间隔着来
               * 不够维度时，就会再循环一遍
               */
              // color: [
              //   'rgba(3,57,104, 0.1)', 'rgba(7,74,127, 0.4)',
              //   'rgba(14,94,149, 0.5)', 'rgba(15,95,165, 0.6)',
              //   'rgba(15,95,165, 0.8)', 'rgba(15,95,165, 1)'
              // ].reverse()
              color: ['rgba(255,255,255)']
            }
          }
        },
        series: [{
          name: '预算 vs 开销',
          type: 'radar',
          // areaStyle: {normal: {}},
          data: [
            {
              value: [4300, 10000, 28000, 35000, 50000, 19000],
              name: '预算分配',
              /** 当前数据维度的线条样式，拐点相连的线条 */
              lineStyle: {
                type: 'solid',
                // color: 'rgba(251, 71, 194, .5)',
                width: 2
              },
              /** 拐点相连的区域内填充色 */
              areaStyle: {
                // color: 'rgba(250, 137, 222, 0.5)'
              }
            },
            {
              value: [5000, 14000, 28000, 31000, 42000, 21000],
              name: '实际开销'
            }
          ]
        }]
      })
    }
  }
}
</script>
