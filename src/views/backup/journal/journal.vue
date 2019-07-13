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
        <el-table :data="visitData" fit highlight-current-row style="width: 100%">
          <el-table-column prop="username" label="用户" />
          <el-table-column prop="visitTime" label="访问时间" />
          <el-table-column prop="url" label="请求URL" />
          <el-table-column prop="ip" label="访问IP" />
          <el-table-column prop="content" label="访问说明" />
        </el-table>
      </el-tab-pane>
      <el-tab-pane label="平台操作日志" name="third">
        <el-table :data="optionData" fit highlight-current-row style="width: 100%">
          <el-table-column prop="username" label="用户" />
          <el-table-column prop="optionDate" label="操作时间" />
          <el-table-column prop="url" label="操作URL" />
          <el-table-column prop="content" label="操作描述" />
        </el-table>
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
            data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun'],
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
      },
      visitData: [{
        username: 'demo_mdc',
        visitTime: '2019-07-09 10:43:20',
        url: '/mdc/history/tableData',
        ip: '192.168.1.1',
        content: '历史调度任务日志'
      }, {
        username: 'demo_mdc',
        visitTime: '2019-07-09 10:43:20',
        url: '/mdc/history/tableData',
        ip: '192.168.1.1',
        content: '历史调度任务日志'
      }, {
        username: 'demo_mdc',
        visitTime: '2019-07-09 10:43:20',
        url: '/mdc/history/tableData',
        ip: '192.168.1.1',
        content: '历史调度任务日志'
      }, {
        username: 'demo_mdc',
        visitTime: '2019-07-09 10:43:20',
        url: '/mdc/history/tableData',
        ip: '192.168.1.1',
        content: '历史调度任务日志'
      }, {
        username: 'demo_mdc',
        visitTime: '2019-07-09 10:43:20',
        url: '/mdc/history/tableData',
        ip: '192.168.1.1',
        content: '历史调度任务日志'
      }, {
        username: 'demo_mdc',
        visitTime: '2019-07-09 10:43:20',
        url: '/mdc/history/tableData',
        ip: '192.168.1.1',
        content: '历史调度任务日志'
      }],
      optionData: [{
        username: '小王',
        optionDate: '2019-07-09 10:43:20',
        url: '/mdc/history/tableData',
        content: '删除了数据服务：123213'
      },
      {
        username: '小王',
        optionDate: '2019-07-09 10:43:20',
        url: '/mdc/history/tableData',
        content: '删除了数据服务：123213'
      },
      {
        username: '小王',
        optionDate: '2019-07-09 10:43:20',
        url: '/mdc/history/tableData',
        content: '删除了数据服务：123213'
      },
      {
        username: '小王',
        optionDate: '2019-07-09 10:43:20',
        url: '/mdc/history/tableData',
        content: '删除了数据服务：123213'
      },
      {
        username: '小王',
        optionDate: '2019-07-09 10:43:20',
        url: '/mdc/history/tableData',
        content: '删除了数据服务：123213'
      }]
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
