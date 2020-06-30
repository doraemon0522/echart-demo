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
      const data = [{
        'hour': '0',
        'total_percentage': 500,
        'xalias': '男',
        'date': 1404172800
      }, {
        'hour': '1',
        'total_percentage': 290,
        'xalias': '男',
        'date': 1404172800
      }, {
        'hour': '2',
        'total_percentage': 219,
        'xalias': '男',
        'date': 1404172800
      }, {
        'hour': '3',
        'total_percentage': 203,
        'xalias': '男',
        'date': 1404172800
      }, {
        'hour': '4',
        'total_percentage': 223,
        'xalias': '男',
        'date': 1404172800
      }, {
        'hour': '5',
        'total_percentage': 120,
        'xalias': '男',
        'date': 1404172800
      }, {
        'hour': '6',
        'total_percentage': 193,
        'xalias': '男',
        'date': 1404172800
      }, {
        'hour': '7',
        'total_percentage': 393,
        'xalias': '男',
        'date': 1404172800
      }, {
        'hour': '0',
        'total_percentage': 2309,
        'xalias': '女',
        'date': 1404172800
      }, {
        'hour': '1',
        'gender_percentage': 1.21577982,
        'total_percentage': 2230,
        'xalias': '女',
        'date': 1404172800
      }, {
        'hour': '2',
        'gender_percentage': 1.21577982,
        'total_percentage': 2230,
        'xalias': '女',
        'date': 1404172800
      }, {
        'hour': '3',
        'gender_percentage': 1.21577982,
        'total_percentage': 20,
        'xalias': '女',
        'date': 1404172800
      }, {
        'hour': '4',
        'gender_percentage': 1.21577982,
        'total_percentage': 2283,
        'xalias': '女',
        'date': 1404172800
      }, {
        'hour': '5',
        'gender_percentage': 1.21577982,
        'total_percentage': 1289,
        'xalias': '女',
        'date': 1404172800
      }, {
        'hour': '6',
        'gender_percentage': 1.21577982,
        'total_percentage': 230,
        'xalias': '女',
        'date': 1404172800
      }, {
        'hour': '7',
        'gender_percentage': 1.23577839,
        'total_percentage': 403,
        'xalias': '女',
        'date': 1404172800
      }]

      const chart = new Chart({
        container: this.id,
        autoFit: true,
        height: 350,
        /** grid能展示的区域与边界的留白 */
        padding: [35, 16]
      })

      chart.data(data)
      chart.scale({
        hour: {
          sync: true
          // tickCount: 11
        },
        total_percentage: {
          sync: true
          // formatter(v) {
          //   return v + '%';
          // }
        },
        xalias: {
          sync: true
        }
      })

      chart.facet('mirror', {
        fields: ['xalias'],
        transpose: true,
        padding: [0, 48, 0, 0],
        eachView(view) {
          view.interval()
            .position('hour*total_percentage')
            .color('xalias', ['#1890ff', '#f04864'])
        }
      })
      chart.render()
    }
  }
}
</script>
