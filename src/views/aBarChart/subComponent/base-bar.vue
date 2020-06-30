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
      // 只有一个元素时，可this.$el，组件里多个标签时，用ref去定位找dom
      this.chart = echarts.init(this.$el)

      this.chart.setOption({
        tooltip: {
          trigger: 'axis'
        },
        legend: {
          data: ['邮件营销', '联盟广告', '视频广告']
        },
        xAxis: {
          type: 'category',
          data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
        },
        yAxis: {
          type: 'value'
        },
        series: [{
          name: '邮件营销',
          type: 'bar',
          data: [120, 132, 101, 134, 90, 230, 210]
        }, {
          name: '联盟广告',
          type: 'bar',
          data: [220, 182, 191, 234, 290, 330, 310]
        // eslint-disable-next-line comma-dangle
        },
        // {
        //   name: '视频广告',
        //   type: 'bar',
        //   data: [150, 232, 201, 154, 190, 330, 410]
        // }
        ]
      })
    }
  }
}
</script>
