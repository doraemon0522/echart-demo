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
          /** 极坐标  值'item' */
          trigger: 'item'
        },
        color: ['#657796', '#68d9ac', '#6697f6'],
        /** 极坐标字段 */
        angleAxis: {
          type: 'category',
          data: ['2000', '2001', '2002', '2003', '2004', '2005', '2006', '2007', '2008', '2009', '2010', '2011', '2012', '2013', '2014']
        },
        /** 极坐标字段 */
        radiusAxis: {
        },
        /** 极坐标字段 */
        polar: {
          radius: '70%'
        },
        series: [{
          type: 'bar',
          data: [21.0, 25.0, 25.0, 25.0, 25.0, 24.0, 24.0, 26.0, 26.0, 27.1, 27.5, 26.4, 28.8, 33.3, 38.2],
          coordinateSystem: 'polar',
          name: 'A',
          stack: 'a'
        }, {
          type: 'bar',
          data: [16, 16, 15, 14, 14, 13, 14, 16, 15.2, 15.2, 15.4, 15.2, 15.4, 16.7, 19.5],
          /** 极坐标字段 */
          coordinateSystem: 'polar',
          name: 'B',
          stack: 'a'
        }, {
          type: 'bar',
          data: [8, 8, 8, 7, 7, 8, 7, 7, 8, 10, 8, 9, 9, 12, 18],
          coordinateSystem: 'polar',
          name: 'C',
          stack: 'a'
        }],
        legend: {
          show: true,
          data: ['A', 'B', 'C']
        }
      }
      )
    }
  }
}
</script>
