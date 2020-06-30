<template>
  <div class="app-container">
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">一、官方demo</div>
        <g2-line id="lineDemo1" />
      </el-col>
      <el-col :span="12">
        <div class="title pt-20 mb-20">二、双Y轴</div>
        <g2-double-y id="g2DoubleY" />
      </el-col>
    </el-row>
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <!-- <div class="title pt-20 mb-20">三、复杂双Y</div> -->
        <!-- <g2-double-y-multi id="g2DoubleYMuti" /> -->
      </el-col>
      <el-col :span="12">
        <span />
      </el-col>
    </el-row>
  </div>
</template>
<script>
import g2Line from './subComponent/g2-line'
import g2DoubleY from './subComponent/g2-double-y'
// import g2DoubleYMulti from './subComponent/g2-double-y-multi'

export default {
  components: {
    g2Line,
    g2DoubleY,
    // g2DoubleYMulti
  },
  data() {
    return {}
  }
}
</script>
