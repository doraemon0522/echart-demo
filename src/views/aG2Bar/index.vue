<template>
  <div class="app-container">
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">一、正负极柱状图</div>
        <g2-bar id="g2BarDemo1" />
      </el-col>
      <el-col :span="12">
        <div class="title pt-20 mb-20">二、极坐标堆叠柱图</div>
        <g2-polar-bar id="g2PolarBar" />
      </el-col>
    </el-row>
  </div>
</template>
<script>
import g2Bar from './subComponent/g2-bar'
import g2PolarBar from './subComponent/g2-polar-bar'

export default {
  components: {
    g2Bar,
    g2PolarBar
  },
  data() {
    return {}
  }
}
</script>
