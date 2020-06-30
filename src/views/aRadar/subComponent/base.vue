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
        // title: {
        //   text: '基础雷达图'
        // },
        tooltip: {},
        legend: {
          data: ['预算分配', '实际开销']
        },
        radar: {
          /** ====(与布局相关)外半径 默认'75%'==== */
          radius: '50%',
          /** =====(与布局相关)，中心（圆心）坐标；第一个参数横向，第二个纵向；=====
           * 百分比比较有用 自适应；[300,400]就是绝对像素。
           * ['50%', '50%']是默认
           *  */
          center: ['50%', '50%'],
          /** 绘制类型 'polygon'-多边形(默认) 'circle'-圆形 */
          // shape: 'circle',
          name: {
            textStyle: {
              color: '#fff',
              backgroundColor: '#999',
              borderRadius: 3,
              padding: [3, 5]
            }
          },
          indicator: [
            { name: '销售', max: 6500 },
            { name: '管理', max: 16000 },
            { name: '信息技术', max: 30000 },
            { name: '客服', max: 38000 },
            { name: '研发', max: 52000 },
            { name: '市场', max: 25000 }
          ]
        },
        series: [{
          name: '预算 vs 开销',
          type: 'radar',
          // areaStyle: {normal: {}},
          data: [
            {
              value: [4300, 10000, 28000, 35000, 50000, 19000],
              name: '预算分配'
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
