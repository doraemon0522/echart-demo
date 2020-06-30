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
            /** 点图案：'emptyCircle'-空心圆(默认)'circle'-实心圆, 'rect'-方块, 'roundRect'-圆角方块,
             * 'triangle'-三角形, 'diamond'-菱形, 'pin'-大头针形(像定位标记图标), 'arrow'-小飞机, 'none' */
            symbol: 'circle',
            /** 是否平滑 */
            smooth: true,
            /** 同个类目,后一个系列的值会在前一个系列的值上相加 */
            stack: '总量',
            data: [120, 132, 101, 134, 90, 230, 210],
            lineStyle: {
              width: 1.5
            }
          },
          {
            name: '联盟广告',
            type: 'line',
            symbol: 'arrow',
            /** 点大小 */
            // symbolSize: 6,
            // symbolSize: [10,6], // 宽10，高6
            symbolSize: (value, params) => { // value-'data'数组的当前值，params-相关数据项参数，打印自行查看哪些有用
              console.log(value)
              const size = params.dataIndex < 3 ? 6 : 9
              return size
            },
            symbolRotate: 90, // 旋转角度,当为'arrow'时是小飞机切线角度的旋转
            connectNulls: false, // 是否连接空数据(null),默认true
            stack: '总量',
            data: [220, 182, null, 234, 290, 330, 310],
            lineStyle: {
              width: 1.5
            }
          },
          {
            name: '视频广告',
            type: 'line',
            symbol: 'triangle', // 三角形
            symbolOffset: [0, '50%'], // 相对原位置的偏移 下移一半
            hoverAnimation: false, // 悬浮 拐点动画 默认true(图标变大，闪一下)
            legendHoverLink: false, // 悬浮图例时，点线变粗变大，false-关闭,true-开启(默认)
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
