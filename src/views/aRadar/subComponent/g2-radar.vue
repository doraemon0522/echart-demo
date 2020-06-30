<template>
  <div :id="id" />
</template>
<script>
import DataSet from '@antv/data-set'
import { Chart } from '@antv/g2'

export default {
  props: {
    id: {
      type: String,
      required: true
    }
  },
  data() {
    return {}
  },
  mounted() {
    this.$nextTick(() => {
      this.initChart()
    })
  },
  methods: {
    initChart() {
      const data = [
        { item: '销售', a: 70, b: 30 },
        { item: '市场', a: 60, b: 70 },
        { item: '研发', a: 50, b: 60 },
        { item: '客服', a: 40, b: 50 },
        { item: '信息技术', a: 60, b: 70 },
        { item: '管理', a: 70, b: 50 }
      ]
      const { DataView } = DataSet
      const dv = new DataView().source(data)
      dv.transform({
        type: 'fold',
        fields: ['a', 'b'], // 展开字段集
        key: 'user', // key字段
        value: 'score' // value字段
      })

      const chart = new Chart({
        container: this.id,
        autoFit: true,
        height: 300
      })
      chart.data(dv.rows)
      chart.scale('score', {
        min: 0,
        max: 80
      })
      chart.coordinate('polar', {
        /** 雷达半径 */
        radius: 0.7
      })
      chart.tooltip({
        shared: true,
        showCrosshairs: true,
        crosshairs: {
          line: {
            style: {
              lineDash: [4, 4],
              stroke: '#333'
            }
          }
        }
      })
      /** data中对应item字段 */
      chart.axis('item', {
        line: null,
        tickLine: null,
        grid: {
          line: {
            style: {
              lineDash: null
            }
          }
        },
        // 文本向外偏移
        label: {
          offset: 18 // 向外偏移18
        }
      })
      chart.axis('score', {
        line: null,
        tickLine: null,
        grid: {
          line: {
            type: 'line',
            style: {
              lineDash: null
            }
          }
        }
      })

      chart
        .line()
        .position('item*score')
        .color('user')
        .size(2)
      chart
        .point()
        .position('item*score')
        .color('user')
        .shape('circle')
        .size(4)
        .style({
          stroke: '#fff',
          lineWidth: 1,
          fillOpacity: 1
        })
      chart
        .area()
        .position('item*score')
        .color('user')
      chart.render()
    }
  }
}
</script>
