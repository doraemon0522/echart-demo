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
      // const data = [
      //   { date: '05-01', name: '邮件营销', number: 120, count: 15000 },
      //   { date: '05-02', name: '邮件营销', number: 132, count: 2320 },
      //   { date: '05-03', name: '邮件营销', number: 101, count: 2001 },
      //   { date: '05-04', name: '邮件营销', number: 134, count: 1504 },
      //   { date: '05-05', name: '邮件营销', number: 90, count: 1900 },
      //   { date: '05-06', name: '邮件营销', number: 230, count: 3030 },
      //   { date: '05-07', name: '邮件营销', number: 210, count: 4010 }
      // ]
      const data = [
        { date: '05-01', '邮件营销': 120, '联盟广告': 220, '视频广告': 150, count: 15000, count1: 1928 },
        { date: '05-02', '邮件营销': 290, '联盟广告': 200, '视频广告': 190, count: 290, count1: 358 },
        { date: '05-03', '邮件营销': 890, '联盟广告': 193, '视频广告': 873, count: 238, count1: 390 },
        { date: '05-04', '邮件营销': 100, '联盟广告': 289, '视频广告': 180, count: 210, count1: 385 },
        { date: '05-05', '邮件营销': 250, '联盟广告': 188, '视频广告': 539, count: 872, count1: 239 },
        { date: '05-06', '邮件营销': 390, '联盟广告': 182, '视频广告': 189, count: 910, count1: 234 },
        { date: '05-07', '邮件营销': 100, '联盟广告': 380, '视频广告': 580, count: 1900, count1: 9394 }
      ]
      // const { DataView } = DataSet
      // const dv = new DataView().source(data)
      // dv.transform({
      //   type: 'fold',
      //   fields: ['邮件营销', '联盟广告', '视频广告'], // 展开字段集
      //   key: 'name', // key字段
      //   value: 'number' // value字段
      // })
      // const dv2 = new DataView().source(data)
      // dv2.transform({
      //   type: 'fold',
      //   fields: ['count2', 'count1'], // 展开字段集
      //   key: 'y2', // key字段
      //   value: 'count' // value字段
      // })

      const chart = new Chart({
        container: this.id,
        autoFit: true,
        height: 300
      })
      const view1 = chart.createView()
      view1.data(data)
      view1.line().position('date*("邮件营销"+"联盟广告"+"视频广告")')
      view1
        .point()
        .position('date*("邮件营销"+"联盟广告"+"视频广告")')
        .shape('circle')

      const view2 = chart.createView()
      view2.data(data)
      view2.line().position('date*count')
      view2
        .point()
        .position('date*count')
        .shape('circle')
        .style({
          stroke: '#fff',
          lineWidth: 1,
          fillOpacity: 1
        })

      // chart.data(dv.rows)
      chart.scale({
        date: {
          type: 'time',
          mask: 'MM-DD',
          range: [0, 1]
        },
        number: {
          tickCount: 6,
          nice: true,
          sync: true,
          min: 0
        },
        count: {
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

      // chart.axis('number', {
      //   label: {
      //     formatter: (val) => {
      //       return val
      //     }
      //   }
      // })

      // chart
      //   .line()
      //   .position('date*number')
      //   .adjust('stack')
      //   .color('name')
      // chart
      //   .line()
      //   .position('date*count')
      //   .color('red')
      // chart
      //   .point()
      //   .position('date*number')
      //   .adjust('stack')
      //   .color('name')
      //   .shape('circle')

      // chart
      //   .point()
      //   .position('date*count')
      //   .color('red')
      //   .shape('circle')

      chart.render()
    }
  }
}
</script>
