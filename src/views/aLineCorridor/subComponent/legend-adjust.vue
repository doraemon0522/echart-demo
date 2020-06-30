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
        /** 改变示例在页面的展示位置 */
        legend: {
          orient: 'horizontal', // 默认'horizontal'-水平, 'vertical'垂直(竖直)
          right: 'center', // 支持像素(px)，百分比(%)，或者'left', 'center', 'right'
          bottom: 0,
          width: '100%',
          itemGap: 15, // 每项之间的间隔
          data: ['邮件营销', '联盟广告', '视频广告']
        },
        /** 坐标网格 */
        grid: {
          left: '3%', // 默认 '10%'
          right: '4%', // 默认 '10%'
          top: '3%', // 默认 60px
          bottom: '10%', // 坐标离容器下侧的距离，支持像素(px)，百分比(%),默认 60px
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
            data: [120, 132, 101, 134, 90, 230, 210]
          },
          {
            name: '联盟广告',
            type: 'line',
            stack: '总量',
            data: [220, 182, 191, 234, 290, 330, 310]
          },
          {
            name: '视频广告',
            type: 'line',
            stack: '总量',
            data: [150, 232, 201, 154, 190, 330, 410]
          }
        ]
      })
    }
  }
}
</script>
