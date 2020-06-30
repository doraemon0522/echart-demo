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
        /**  方法一 */
        color: ['blue'],
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
          /** 图例悬浮 柱图高亮（如果有颜色替换，这个效果好像就没了） */
          legendHoverLink: true,
          itemStyle: { // ---图形形状
            /**  方法二 */
            // color: 'blue',
            // 圆角半径 只支持px
            barBorderRadius: [49, 49, 0, 0],
            /** 描边 宽度，默认不描边，所以borderType borderColor要在设置了borderWidth之后才会生效 */
            borderWidth: 2,
            /** 柱条的描边 'solid', 'dashed', 'dotted'*/
            borderType: 'solid',
            borderColor: '#477efb'

          },
          /** 柱宽 50(绝对像素px) '50%'(自适应宽度) */
          barWidth: '50%',
          data: [120, 132, 101, 134, 90, 230, 210]
        }
        // , {
        //   name: '联盟广告',
        //   type: 'bar',
        //   data: [220, 182, 191, 234, 290, 330, 310]
        // },
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
