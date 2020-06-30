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
        tooltip: {
          trigger: 'axis'
        },
        /** 调色盘颜色列表 */
        color: ['#fb474b', '#fbca47', '#ca47fb'],
        legend: {
          orient: 'horizontal',
          right: 'center',
          bottom: 0,
          width: '100%',
          itemGap: 15,
          data: ['邮件营销', '联盟广告', '视频广告']
        },
        grid: {
          left: '3%',
          right: '4%',
          top: '3%',
          bottom: '10%',
          containLabel: true
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
            name: '邮件营销',
            type: 'line',
            stack: '总量',
            data: [120, 132, 101, 134, 90, 230, 210],
            lineStyle: {
              width: 1.5
            }
          },
          {
            name: '联盟广告',
            type: 'line',
            stack: '总量',
            data: [220, 182, 191, 234, 290, 330, 310],
            lineStyle: {
              width: 1.5
            }
          },
          {
            name: '视频广告',
            type: 'line',
            stack: '总量',
            data: [150, 232, 201, 154, 190, 330, 410],
            lineStyle: {
              width: 1.5
            }
          }
        ]
      })
    }
  }
}
</script>
