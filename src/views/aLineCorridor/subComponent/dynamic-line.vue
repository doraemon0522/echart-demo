<template>
  <!-- 区域图 -->
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
      chart: null,
      xAxisList: [],
      yAxisMap: {
        email: [],
        union: [],
        video: []
      }
    }
  },
  mounted() {
    this.getData()
  },
  beforeDestroy() {
    if (!this.chart) {
      return
    }
    this.chart.dispose()
    this.chart = null
  },
  methods: {
    // 获取后端数据(**== 数据更新chart需重绘时，不用另处理，直接再来一次getData全流程重复即可 ==**)
    getData() {
      const data = [{
        dateTm: '2020-05-02',
        email: 120,
        union: 220,
        video: 150
      }, {
        dateTm: '2020-05-03',
        email: 132,
        union: 182,
        video: 232
      }, {
        dateTm: '2020-05-04',
        email: 101,
        union: 191,
        video: 201
      }, {
        dateTm: '2020-05-05',
        email: 134,
        union: 234,
        video: 154
      }, {
        dateTm: '2020-05-06',
        email: 90,
        union: 290,
        video: 190
      }, {
        dateTm: '2020-05-07',
        email: 230,
        union: 330,
        video: 330
      }, {
        dateTm: '2020-05-08',
        email: 210,
        union: 310,
        video: 410
      }]
      setTimeout(() => {
        const email = []
        const union = []
        const video = []
        const xAxisList = []
        data.forEach((item) => {
          xAxisList.push(item.dateTm)
          email.push(item.email)
          union.push(item.union)
          video.push(item.video)
        })
        this.xAxisList = xAxisList
        this.yAxisMap = {
          email,
          union,
          video
        }
        // nextTick不可少，画图与数据处理间隔出时间，防止渲染错误
        this.$nextTick(() => {
          this.initChart()
        })
      }, 1000)
    },
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
          /** 横坐标显示不下时一种思路是直接键入换行符 */
          data: this.xAxisList.map((str) => {
            // 键入换行符
            // return str.replace('-','\n')
            return str.substring(5)
          }),
          /** 坐标轴刻度设置（ 与yAxis有很多相同api可结合看double-y.vue） */
          axisLabel: {
            show: true, // 默认true
            interval: 0, // 标签之间的间隔，1-表示『隔一个标签显示一个标签』；2-隔2个；以此类推
            rotate: 45, // 角度-90~90
            padding: 0, // 默认
            // color: '#f63980', // 刻度文字颜色,一般不设置
            height: 'auto' // 一般不配置
          }
        },
        yAxis: {
          type: 'value'
        },
        /** 坑点：当series整个都是动态时（即长度可变），echarts会有缓存，需要强力清缓存 */
        series: [
          {
            name: '邮件营销',
            type: 'line',
            symbol: 'none',
            smooth: true,
            stack: '总量',
            areaStyle: {
              color: '#fb474b',
              opacity: 0.2
            },
            data: this.yAxisMap.email,
            lineStyle: {
              width: 1.5
            }
          },
          {
            name: '联盟广告',
            type: 'line',
            symbol: 'none',
            smooth: true,
            stack: '总量',
            areaStyle: {
              color: '#fbca47',
              opacity: 0.2
            },
            data: this.yAxisMap.union,
            lineStyle: {
              width: 1.5
            }
          },
          {
            name: '视频广告',
            type: 'line',
            symbol: 'none',
            smooth: true,
            stack: '总量',
            areaStyle: {
              color: '#ca47fb',
              opacity: 0.2
            },
            data: this.yAxisMap.video,
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
