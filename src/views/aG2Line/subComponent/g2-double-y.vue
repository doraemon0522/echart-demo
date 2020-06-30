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
        { date: '05-01', '邮件营销': 120, '联盟广告': 220, '视频广告': 150, count: 15000 },
        { date: '05-02', '邮件营销': 290, '联盟广告': 200, '视频广告': 190, count: 290 },
        { date: '05-03', '邮件营销': 890, '联盟广告': 193, '视频广告': 873, count: 238 },
        { date: '05-04', '邮件营销': 100, '联盟广告': 289, '视频广告': 180, count: 210 },
        { date: '05-05', '邮件营销': 250, '联盟广告': 188, '视频广告': 539, count: 872 },
        { date: '05-06', '邮件营销': 390, '联盟广告': 182, '视频广告': 189, count: 910 },
        { date: '05-07', '邮件营销': 100, '联盟广告': 380, '视频广告': 580, count: 1900 }
      ]
      const { DataView } = DataSet
      const dv = new DataView().source(data)
      /** 3个字段用转换，展开到同一个字段上 即同一个number */
      dv.transform({
        type: 'fold',
        fields: ['邮件营销', '联盟广告', '视频广告'], // 展开字段集
        key: 'name', // key字段
        value: 'number' // value字段
      })

      const chart = new Chart({
        container: this.id,
        autoFit: true,
        height: 300
      })

      chart.data(dv.rows)
      chart.scale({
        date: {
          range: [0, 1]
        },
        /** 左Y */
        number: {
          tickCount: 6,
          nice: true,
          sync: true,
          min: 0
        },
        /** 右Y */
        count: {
          alias: '次数',
          tickCount: 6,
          nice: true,
          sync: true,
          min: 0
        }
      })

      chart.tooltip({
        showCrosshairs: true,
        shared: true
      })

      chart.axis('number', {
        label: {
          formatter: (val) => {
            return val
          }
        }
      })
      // chart.axis('count', {
      //   title: {}
      // })

      /** position的X一样Y不一样，就能映射到不同Y了 */
      chart
        .line()
        .position('date*number')
        .adjust('stack')
        .color('name')
      chart
        .line()
        .position('date*count')
        .color('red')
      chart
        .point()
        .position('date*number')
        .adjust('stack')
        .color('name')
        .shape('circle')

      chart
        .point()
        .position('date*count')
        .color('red')
        .shape('circle')

      chart.render()
    }
  }
}
</script>
