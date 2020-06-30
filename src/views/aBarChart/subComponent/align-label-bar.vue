<template>
  <!-- 刻度与标签保持一致 柱状图 -->
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
        legend: {
          data: ['邮件营销', '联盟广告', '视频广告']
        },
        xAxis: {
          type: 'category',
          /** 刻度和标签对齐
           * searies奇数个的时候会比较好看
           * 标签始终都在柱图（一堆或一个）的中央
           * */
          axisTick: {
            /** type == 'category'时有效 */
            alignWithLabel: true
          },
          /** 刻度线样式 */
          lineStyle: {
            type: 'solid' // 'solid'实线；'dashed'虚线；'dotted'点
          },
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
        },
        {
          name: '视频广告',
          type: 'bar',
          data: [150, 232, 201, 154, 190, 330, 410]
        }
        ]
      })
    }
  }
}
</script>
