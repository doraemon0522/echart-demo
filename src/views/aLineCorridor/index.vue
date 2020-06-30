<template>
  <div class="app-container">
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">一、官方demo</div>
        <base-line />
      </el-col>
      <el-col :span="12">
        <div class="title pt-20 mb-20">一（1）、基于一不层叠(no-stack)的效果</div>
        <no-stack />
      </el-col>
    </el-row>
    <!-- 调整图例 -->
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">二、基于一调整图例legend</div>
        <legend-adjust />
      </el-col>
      <el-col :span="12">
        <div class="title pt-20 mb-20">一（2）、基于一修改标线(axisPoniter)</div>
        <axis-pointer />
      </el-col>
    </el-row>
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">三、基于二修改“线”颜色</div>
        <change-color />
      </el-col>
      <el-col :span="12">
        <div class="title pt-20 mb-20">三(1)、基于三修改悬浮层tooltip</div>
        <line-tooltip />
      </el-col>
    </el-row>
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">四、基于三修改“点”配置</div>
        <div class="pb-50">（无）</div>
        <point-symbol />
      </el-col>
      <el-col :span="12">
        <div class="title pt-20 mb-20">三(2)、基于三变双Y轴(yAxis)</div>
        <div class="mb-30">如果两个数据的数量级相差很大，会造成数量级低的数据折线图被压缩成一条很直的线，双Y轴来解决</div>
        <!-- 讲解Y轴(yAxis)细节api -->
        <double-y />
      </el-col>
    </el-row>
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">五、基于四且线只取“邮件营销”类型修改为区域图</div>
        <line-area />
      </el-col>
      <el-col :span="12">
        wwwww
      </el-col>
    </el-row>
    <el-row :gutter="20" class="bg-white">
      <el-col :span="12">
        <div class="title pt-20 mb-20">六、基于五动态化数据（后端数据处理+xAxis）</div>
        <!-- 附带xAxis讲解 -->
        <dynamic-line />
      </el-col>
      <el-col :span="12">
        wwwww
      </el-col>
    </el-row>
  </div>
</template>

<script>
import baseLine from './subComponent/base-line'
import legendAdjust from './subComponent/legend-adjust'
import changeColor from './subComponent/change-color'
import pointSymbol from './subComponent/point-symbol'
import doubleY from './subComponent/double-y'
import lineTooltip from './subComponent/line-tooltip'
import noStack from './subComponent/no-stack'
import lineArea from './subComponent/line-area'
import dynamicLine from './subComponent/dynamic-line'
import axisPointer from './subComponent/axis-pointer'

export default {
  name: 'LineCorridor',
  components: {
    baseLine,
    legendAdjust,
    changeColor,
    pointSymbol,
    doubleY,
    lineTooltip,
    noStack,
    lineArea,
    dynamicLine,
    axisPointer
  },
  data() {
    return {
      articleList: []
    }
  }
}
</script>

<style lang="scss" scoped>
.title {
  font-size: 20px;
  font-weight: 500;
}
.documentation-container {
  margin: 50px;
  display: flex;
  flex-wrap: wrap;
  justify-content: space-evenly;

  .document-btn {
    flex-shrink: 0;
    display: block;
    cursor: pointer;
    background: black;
    color: white;
    height: 60px;
    width: 200px;
    margin-bottom: 16px;
    line-height: 60px;
    font-size: 20px;
    text-align: center;
  }
}
</style>
