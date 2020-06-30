<template>
  <div class="app-container">
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">一、echarts官方demo</div>
        <Base />
      </el-col>
      <el-col :span="12">
        <div class="title pt-20 mb-20">一（1）、echarts区域型雷达图</div>
        <Area-radar />
      </el-col>
    </el-row>
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">二、antv/g2 雷达图</div>
        <g2-radar id="g2RadarDemo" />
      </el-col>
      <el-col :span="12">
        <span />
      </el-col>
    </el-row>
  </div>
</template>
<script>
import Base from './subComponent/base'
import AreaRadar from './subComponent/area-radar'
import g2Radar from './subComponent/g2-radar'

export default {
  components: {
    Base,
    AreaRadar,
    g2Radar
  },
  data() {
    return {}
  }
}
</script>
