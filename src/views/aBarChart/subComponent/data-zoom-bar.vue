<template>
  <div :class="className" :style="{height:height,width:width}" />
</template>
<script>
import echarts from 'echarts'
import { timeFormatter } from '@/utils/index'
const MAX_DAY = 100
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
      chart: null,
      xAxisArr: [],
      yAxisData: []
    }
  },
  mounted() {
    this.prepareYData()
    this.prepareDate()
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
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data: ['邮件营销']
        },
        /** 区域缩放echart按需引入时，用到datazoom需先将其引入
         * 此功能只相当于缩放功能，如多维度比较时，要查看单独维度的数据，可用图例滚动grid单条来达到效果。
         * 缩放组件
         */
        dataZoom: [{
          // 鼠标在grid中，滚轮或手势缩放
          type: 'inside',
          // 组件离容器下侧距离 '20%',另有上、左、右
          bottom: 'auto',
          // 在type：'inside'下未研究出效果，slider时很直观，就是横竖的摆放
          orient: 'vertical',
          // 官方建议显式指定，默认0，数组如[0,3]多个x轴的索引值 第一个 和 第四个 xAxis
          // 带Axis的是设置直角轴，其他轴，此关键词会换，参考官网
          xAxisIndex: 0,
          // 数据窗口范围：0 ~ 100。表示 0% ~ 100%。
          start: 50,
          end: 100
          // 缩放轴data数组中的某个值，或data数组的index,感觉这个好鸡肋
          // startValue: 10
        }, {
          // 设置滑动条，拖动滑动条实现数据缩放
          type: 'slider'

        }],
        grid: {
          // 给dataZoom预留空间，90px
          bottom: 90
        },
        xAxis: {
          type: 'category',
          data: this.xAxisArr
        },
        yAxis: {
          type: 'value'
        },
        series: [{
          name: '邮件营销',
          type: 'bar',
          data: this.yAxisData
        }
        ]
      })
    },
    prepareYData() {
      const max = 500
      const min = 100
      const yArr = []
      for (let i = 1; i <= MAX_DAY; i++) {
        const randomD = Math.floor(Math.random() * (max - min)) + min
        yArr.push(randomD)
      }
      this.yAxisData = yArr
    },
    prepareDate() {
      const xDataArr = []
      const endDay = new Date()
      const endDayTm = endDay.getTime()
      for (let i = 1; i <= MAX_DAY; i++) {
        const oneDay = endDayTm - 24 * 60 * 60 * 1000 * i
        const formatDay = timeFormatter(oneDay, 0)
        xDataArr.push(formatDay)
      }
      this.xAxisArr = xDataArr
    }
  }
}
</script>
