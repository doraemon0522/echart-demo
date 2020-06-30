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
        tooltip: {
          trigger: 'axis',
          /** 坐标轴指示器(grid里悬浮后显示的坐标十字架)，柱状图一般为阴影
           *  简单场景此处用，xAxis或yAxis的axisPointer可覆盖此处配置
           */
          axisPointer: {
            /** 'line'-直线;'shadow'-阴影(柱状图用的较多);'none'-无;'cross'-启用指示器(十字)，即x轴y轴都启用*/
            type: 'cross',
            lineStyle: {
              type: 'dashed',
              // 红色
              color: '#ff7200'
            }
          }
        },
        legend: {
          data: ['邮件营销', '联盟广告', '视频广告']
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: {
          type: 'category',
          boundaryGap: false,
          data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日'],
          /** 如果x轴或者y轴某一轴设置了一个字段，另一轴这个字段会填充echart默认值，并且有复杂的各字段权重不一样的情况 */
          axisPointer: {
            /** 可注释掉看效果 */
            label: {
              show: false
            }
          }
        },
        yAxis: {
          type: 'value',
          /** 此处设置后，相同api字段就会覆盖tooltip中的axisPointer */
          axisPointer: {
            /** yAxis或xAxis时，类型比tooltip少，即不存在cross */
            type: 'line',
            // 轴标签
            label: {
              show: true, // 默认false
              precision: 'auto', // 小数点精度，如2
              /** 其他还有很多style属性参看官网 */
              color: '#333', // 默认 #fff
              backgroundColor: 'none' // 默认和lineStyle.color 的设置相同
            },
            lineStyle: {
              type: 'solid',
              // 紫色
              color: '#ca47fb'
            }
          }
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
