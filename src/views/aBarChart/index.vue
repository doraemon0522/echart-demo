<template>
  <div class="app-container">
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">一、官方demo</div>
        <base-bar />
      </el-col>
      <el-col :span="12">
        <div class="title pt-20 mb-20">一(1)、刻度和标签对齐</div>
        <align-label-bar />
      </el-col>
    </el-row>
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">二、正负极柱状图</div>
        <positive-negative />
      </el-col>
      <el-col :span="12">
        <div class="title pt-20 mb-20">一(2)、圆角柱状图</div>
        <radius-bar />
      </el-col>
    </el-row>
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">三、大数据柱状图（可缩放）</div>
        <data-zoom-bar />
      </el-col>
      <el-col :span="12">
        <div class="title pt-20 mb-20">三、极坐标柱状</div>
        <polar-stack-bar />
      </el-col>
    </el-row>
  </div>
</template>
<script>
import baseBar from './subComponent/base-bar'
import positiveNegative from './subComponent/positive-negative'
import dataZoomBar from './subComponent/data-zoom-bar'
import alignLabelBar from './subComponent/align-label-bar'
import radiusBar from './subComponent/radius-bar'
import polarStackBar from './subComponent/polar-stack-bar'

export default {
  components: {
    baseBar,
    positiveNegative,
    dataZoomBar,
    alignLabelBar,
    radiusBar,
    polarStackBar
  },
  data() {
    return {}
  }
}
</script>
<style lang="scss" scoped>
.title {
  font-size: 20px;
  font-weight: 500;
}
</style>
