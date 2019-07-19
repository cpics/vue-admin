<template>
  <div class="app-container">
    <el-form ref="formInline" v-model="formInline" :inline="true">
      <el-form-item label="日期:" prop="formInline.date">
        <el-date-picker v-model="formInline.date" type="daterange" range-separator="至" start-placeholder="开始日期" end-placeholder="结束日期" />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" icon="el-icon-search" @click="handleSearch">查询</el-button>
      </el-form-item>
    </el-form>

    <el-tabs v-model="activeName" type="card">
      <el-tab-pane label="模块访问统计" name="first">
        <div class="statistics-chart">
          <div ref="dmChart" style="height:90%;width:90%;" />
        </div>
      </el-tab-pane>
      <el-tab-pane label="平台访问日志" name="second">
        22222223
      </el-tab-pane>
      <el-tab-pane label="平台操作日志" name="third">
        3
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
export default {
  name: 'BackupVisit',
  data() {
    return {
      activeName: 'first',
      formInline: {
        date: ''
      },
      dmChart: null,
      dmOptions: {
        color: ['#3398DB'],
        tooltip: {
          trigger: 'axis',
          axisPointer: { // 坐标轴指示器，坐标轴触发有效
            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
          }
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: [
          {
            type: 'category',
            data: ['教务', '学工', '人事', '财务', '科研', '后勤', '一卡通'],
            axisTick: {
              alignWithLabel: true
            }
          }
        ],
        yAxis: [
          {
            type: 'value'
          }
        ],
        series: [
          {
            name: '直接访问',
            type: 'bar',
            barWidth: '60%',
            data: [10, 52, 200, 334, 390, 330, 220]
          }
        ]
      }
    }
  },
  mounted() {
    this.initDmChart()
  },
  methods: {
    initDmChart() {
      this.dmChart = echarts.init(this.$refs.dmChart)
      this.dmChart.setOption(this.dmOptions)
    },
    handleSearch() {
      this.$message({
        message: '查询成功',
        type: 'success'
      })
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
.statistics-chart {
  width: 100%;
  height: 280px;
  margin-bottom: 15px;
}
</style>
