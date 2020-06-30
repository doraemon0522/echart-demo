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
          trigger: 'axis',
          backgroundColor: 'rgba(255,255,255)', // 默认'rgba(50,50,50,0.7)'
          /** 提示框外框的额外样式，会有意外的惊或喜，可修改看看 */
          extraCssText: 'box-shadow:0px 2px 8px 0px rgba(0,0,0,0.15)',
          /** 内容的文字样式配置 */
          textStyle: {
            color: 'rgba(0,0,0,0.65)', // 默认 '#fff'
            fontSize: 12 // 默认14
          },
          /** 提示框内容展示修改 === 主要想修改marker的大小，不需要时就不用如此麻烦====
           * 模板型(使用模板，marker无法展示，所以既想修改格式又想保留marker，需函数回调方式)
           * formatter: '{b0}: {c0}<br />{b1}: {c1}'
           * 模板变量有 {a}, {b}，{c}，{d}，{e}，数字代表系列series中的索引
           * 折线（区域）图、柱状（条形）图、K线图 : {a}（系列名称），{b}（类目值），{c}（数值）, {d}（无）
           * 散点图（气泡）图 : {a}（系列名称），{b}（数据名称），{c}（数值数组）, {d}（无）
           * 地图 : {a}（系列名称），{b}（区域名称），{c}（合并数值）, {d}（无）
           * 饼图、仪表盘、漏斗图: {a}（系列名称），{b}（数据项名称），{c}（数值）, {d}（百分比）
           * {@xxx}：数据中名为'xxx'的维度的值，如{@product}表示名为'product'` 的维度的值。
           * {@[n]}：数据中维度n的值，如{@[3]}` 表示维度 3 的值，从 0 开始计数。
           * 可参考官网 label.formatter
           */
          formatter: (params) => {
            var result = ''
            params.forEach((item, index) => {
              // console.log(item)
              const cur_marker = '<span style="display:inline-block;margin-right:5px;border-radius:8px;width:8px;height:8px;background-color:' + item.color + '"></span>'
              const title = index === 0 ? item.axisValue + '</br>' : ''
              result += title + cur_marker + item.seriesName + '：' + item.data + '</br>'
            })
            return result
          }
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
