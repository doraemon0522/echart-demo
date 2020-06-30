<template>
  <div :id="id" />
</template>
<script>
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
        { date: '05-01', name: '邮件营销', number: 120 },
        { date: '05-02', name: '邮件营销', number: 132 },
        { date: '05-03', name: '邮件营销', number: 101 },
        { date: '05-04', name: '邮件营销', number: 134 },
        { date: '05-05', name: '邮件营销', number: 90 },
        { date: '05-06', name: '邮件营销', number: 230 },
        { date: '05-07', name: '邮件营销', number: 210 },
        { date: '05-01', name: '联盟广告', number: 220 },
        { date: '05-02', name: '联盟广告', number: 182 },
        { date: '05-03', name: '联盟广告', number: 191 },
        { date: '05-04', name: '联盟广告', number: 234 },
        { date: '05-05', name: '联盟广告', number: 290 },
        { date: '05-06', name: '联盟广告', number: 330 },
        { date: '05-07', name: '联盟广告', number: 310 },
        { date: '05-01', name: '视频广告', number: 150 },
        { date: '05-02', name: '视频广告', number: 232 },
        { date: '05-03', name: '视频广告', number: 201 },
        { date: '05-04', name: '视频广告', number: 154 },
        { date: '05-05', name: '视频广告', number: 190 },
        { date: '05-06', name: '视频广告', number: 330 },
        { date: '05-07', name: '视频广告', number: 410 }
      ]

      const chart = new Chart({
        container: this.id,
        autoFit: true,
        height: 300
      })

      chart.data(data)
      chart.scale({
        date: {
          range: [0, 1]
        },
        number: {
          nice: true,
          /** number轴(y轴)刻度从0开始，默认会从data的最小值开始 */
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

      chart
        .line()
        .position('date*number')
        /** 堆叠数据 */
        .adjust('stack')
        .color('name')
        /** 线平滑 */
        // .shape('smooth')

      chart
        .point()
        .position('date*number')
        .adjust('stack')
        .color('name')
        .shape('circle')

      chart.render()
    }
  }
}
</script>
