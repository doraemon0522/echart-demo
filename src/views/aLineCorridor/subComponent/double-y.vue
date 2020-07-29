<template>
  <div :class="className" :style="{height:height,width:width}" />
</template>
<script>
import echarts from 'echarts'
// Y轴刻度数
const SPLIT_NUMBER = 5

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
      this.handleUpdateOption()
      // 图例点击 更新y轴刻度
      this.chart.on('legendselectchanged', (params) => {
        this.handleUpdateOption(params.selected)
      });
      
    },
    handleUpdateOption(selectedObj) {
      /** data1 有变化 === 为了拉大双Y轴刻度线====*/
      const data1 = [120, 9132, 101, 134, 90, 230, 210]
      const data2 = [220, 182, 191, 234, 290, 330, 310]
      const data3 = [150, 232, 201, 154, 190, 330, 410]

      const legendDataArr = ['邮件营销', '联盟广告', '视频广告']
      let new_stack = {},optionParams;
      let initSelectObj = {};
      legendDataArr.forEach(item => {
        initSelectObj[item] = true
      })
      let savesSelectObj = selectedObj? selectedObj: initSelectObj
      Object.keys(savesSelectObj).forEach(key =>{
        if(savesSelectObj[key]) {
          switch(key) {
            case '联盟广告':
              new_stack['data2'] = data2
              break;
            case '视频广告':
              new_stack['data3'] = data3
              break;
          }
        }
      })
      
      /** 有'stack'时 */
      const multi_data = this.sumMultiArr(new_stack)
      /** series配置无'stack'时，即后一项不累加前一项*/
      // const multi_data = data2.slice().concat(data3)
      const y_max0 = this.calMax(data1)
      const y_max1 = this.calMax(multi_data)
      const intv0 = (y_max0 - 0) / SPLIT_NUMBER
      const intv1 = (y_max1 - 0) / SPLIT_NUMBER

      if(selectedObj) {
        optionParams = {
          yAxis: [{
            name: '邮件营销',
            max: y_max0,
            interval: intv0,
          },{
            name: '广告',
            max: y_max1,
            interval: intv1,
          }]
        }
      }else {
        optionParams = {
          tooltip: {
            /** 'axis'-有类目的图使用(折线图，柱图)，'item'-无类目图（散点图，饼图等）*/
            trigger: 'axis',
            /** 坐标轴指示器(grid里悬浮后显示的坐标十字架)，柱状图一般为阴影
             *  简单场景此处用，xAxis或yAxis的axisPointer可覆盖此处配置
             */
            axisPointer: {
              /** 'line'-直线;'shadow'-阴影(柱状图用的较多);'none'-无;'cross'-启用指示器(十字)，即x轴y轴都启用*/
              type: 'line',
              lineStyle: {
                type: 'dashed',
                color: '#ff7200'
              }
            }
          },
          color: ['#fb474b', '#fbca47', '#ca47fb'],
          legend: {
            orient: 'horizontal',
            right: 'center',
            bottom: 0,
            width: '100%',
            itemGap: 15,
            data: legendDataArr
          },
          grid: {
            left: '3%',
            right: '4%',
            top: '3%',
            bottom: '10%',
            containLabel: true
          },
          /** x轴和y轴好多参数相同，所以X轴简略了好多 */
          xAxis: {
            /** category-类目轴 */
            type: 'category',
            /** 坐标轴两边留白，默认true，此时标签和数据点都会在两个刻度中间,即不对齐。false-标签和数据对齐 */
            boundaryGap: false,
            data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
          },
          /** 双Y轴关键处 ==== yAxis为数组 === */
          yAxis: [{
            /** 'value'-数值轴，'time' 时间轴，'log' 对数轴，统称非类目轴 */
            type: 'value',
            /** 是否显示该轴，默认值true */
            show: true,
            axisTick: {
              show: false
            },
            /** 关键 解决Y轴2边数组差距很大时，刻度自适应导致的2边刻度不一样，各自画刻度，难看
             * 一般时，可不用定义，且不建议设置自定义
             * min: 0
             * max: y_max0
             * interval: intv0
             */
            min: 0,
            max: y_max0,
            interval: intv0,
            // splitNumber: SPLIT_NUMBER, // 当设置interval时，此设置就不生效了
            /** 坐标轴名称 */
            name: '邮件营销',
            /** 坐标轴名称 文字样式设置 */
            nameTextStyle: {
              color: '#000'
            },
            /** 坐标轴轴线 y轴有时需要不显示 */
            axisLine: {
              show: false,
              lineStyle: {
                color: '#88c6ff'
              }
            },
            /** 坐标轴刻度设置 */
            axisLabel: {
              margin: 10,
              /** 相当于没变化，仅作示例告知有此参数与写法 */
              formatter: '{value}',
              textStyle: {
                fontSize: 14,
                color: '#88c6ff'
              }
            },
            /** grid区域的分割线 */
            splitLine: {
              show: true,
              lineStyle: {
                /** 多个时依次循环使用 */
                color: ['#1a4859'],
                /** 'solid','dashed','dotted' */
                type: 'dashed'
              }
            }
          }, {
            type: 'value',
            show: true,
            axisTick: {
              show: false
            },
            min: 0,
            max: y_max1,
            interval: intv1,
            /** 反向坐标轴（与常见的坐标轴反着来展示） */
            // inverse: true,
            // splitNumber: SPLIT_NUMBER,
            name: '广告',
            axisLine: {
              show: false,
              lineStyle: {
                color: '#88c6ff'
              }
            },
            nameTextStyle: {
              padding: 11,
              color: '#c647fb'
            },
            axisLabel: {
              margin: 15,
              formatter: '{value}',
              textStyle: {
                fontSize: 14,
                color: '#000'
              }
            },
            // nameLocation:'middle',
            splitLine: {
              show: true,
              lineStyle: {
                color: ['#1a4859'],
                type: 'dashed'
              }
            }
          }],
          series: [
            {
              name: '邮件营销',
              type: 'line',
              /** 双Y轴关键处 === 指定本数据放在哪个Y轴===*/
              yAxisIndex: 0,
              stack: '其他',
              data: data1,
              lineStyle: {
                width: 1.5
              }
            },
            {
              name: '联盟广告',
              type: 'line',
              yAxisIndex: 1,
              stack: '总量',
              data: data2,
              lineStyle: {
                width: 1.5
              }
            },
            {
              name: '视频广告',
              type: 'line',
              yAxisIndex: 1,
              stack: '总量',
              data: data3,
              lineStyle: {
                width: 1.5
              }
            }
          ]
        }
      }

      this.chart.setOption(optionParams)
    },
    sumMultiArr(json) {
      const result = []
      for (const key in json) {
        // 遍历数组的每一项
        json[key].forEach((value, index) => {
          if (this.isBlank(result[index])) {
            result[index] = 0
          }
          result[index] += value
        })
      }
      return result
    },
    isBlank(val) {
      if (val == null || val === '') {
        return true
      }
    },
    /** 刻度整数显示，然后除的数值取值有技巧
     * 这一步提取能使得2边Y轴不会画出2条紧挨着的线（视觉上看起来很粗，其实是分割的误差导致的）
     *  */
    calMax(arr) {
      let max = 0
      arr.forEach((el1) => {
        if (!(el1 === undefined || el1 === '')) {
          if (max < el1) {
            max = el1
          }
        }
      })
      const two_num = SPLIT_NUMBER * 2
      const tran_num = two_num - 0.5
      const maxint = Math.ceil(max / tran_num) // 不让最高的值超过最上面的刻度
      const maxval = maxint * two_num // 让显示的刻度是整数
      return maxval
    }
  }
}
</script>
