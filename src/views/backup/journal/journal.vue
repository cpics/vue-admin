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
        <el-pagination background layout="sizes, prev, pager, next" :page-sizes="[10,15, 30, 50, 100]" :total="1000" />
      </el-tab-pane>
      <el-tab-pane label="平台操作日志" name="third">
        <el-table :data="optionData" fit highlight-current-row style="width: 100%">
          <el-table-column prop="username" label="用户" min-width="20%" />
          <el-table-column prop="optionDate" label="操作时间" min-width="20%" />
          <el-table-column prop="url" label="操作URL" min-width="30%" />
          <el-table-column prop="content" label="操作描述" min-width="30%" />
        </el-table>
        <el-pagination background layout="sizes, prev, pager, next" :page-sizes="[10,15, 30, 50, 100]" :total="1000" />
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
            data: ['元数据管理', '主数据管理', '代码标准管理', '运行监控管理', '数据共享接口', '质量检测管理', '数据备份处理', '系统管理'],
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
            data: [33, 6, 55, 20, 39, 36, 5, 22]
          }
        ]
      },
      visitData: [{
        username: 'admin',
        visitTime: '2019-07-29 10:43:20',
        url: '/backup/index',
        ip: '192.168.1.36',
        content: '数据备份'
      }, {
        username: 'admin',
        visitTime: '2019-07-29 10:41:34',
        url: '/backup/journal',
        ip: '192.168.1.36',
        content: '系统日志'
      }, {
        username: 'admin',
        visitTime: '2019-07-29 10:40:19',
        url: '/dataShare/index',
        ip: '192.168.1.36',
        content: '数据共享服务'
      }, {
        username: 'admin',
        visitTime: '2019-07-29 10:38:50',
        url: '/mainData/index',
        ip: '192.168.1.36',
        content: ''
      }, {
        username: 'admin',
        visitTime: '2019-07-29 10:36:23',
        url: '/mainData/manage',
        ip: '192.168.1.36',
        content: '主数据管理'
      }, {
        username: 'admin',
        visitTime: '2019-07-29 10:35:26',
        url: '/mData/index',
        ip: '192.168.1.36',
        content: '数据源管理'
      }, {
        username: 'admin',
        visitTime: '2019-07-29 10:34:44',
        url: '/mData/object',
        ip: '192.168.1.36',
        content: '数据对象管理'
      }, {
        username: 'admin',
        visitTime: '2019-07-29 10:34:19',
        url: '/run/index',
        ip: '192.168.1.36',
        content: '数据集成管理'
      }, {
        username: 'admin',
        visitTime: '2019-07-29 10:33:50',
        url: '/run/sql',
        ip: '192.168.1.36',
        content: '数据库监控'
      }, {
        username: 'admin',
        visitTime: '2019-07-29 10:32:23',
        url: '/core/index',
        ip: '192.168.1.36',
        content: ''
      }],
      optionData: [{
        username: 'admin',
        optionDate: '2019-07-29 10:43:20',
        url: '/dataShare/service',
        content: '维护了数据服务：86119c0e4d7c499bbc56e1bc69b2c9df'
      },
      {
        username: 'admin',
        optionDate: '2019-07-29 10:41:18',
        url: '/dataShare/service',
        content: '停用了数据服务：8C4951439A3171CAE05347F413AC2E8F'
      },
      {
        username: 'admin',
        optionDate: '2019-07-29 10:40:08',
        url: '/code/deleteCode',
        content: '删除了代码表标准内容：T_CODE_XB'
      },
      {
        username: 'admin',
        optionDate: '2019-07-29 10:38:50',
        url: '/code/updateObject',
        content: '修改了数据对象TV_MZ'
      },
      {
        username: 'admin',
        optionDate: '2019-07-29 10:36:20',
        url: '/code/updateObject',
        content: '修改了数据对象TV_MZ'
      },
      {
        username: 'admin',
        optionDate: '2019-07-29 10:35:18',
        url: '/code/updateObject',
        content: '修改了数据对象TV_SEX'
      },
      {
        username: 'admin',
        optionDate: '2019-07-29 10:33:48',
        url: '/code/updateObject',
        content: '修改了数据对象TV_SEX'
      },
      {
        username: 'admin',
        optionDate: '2019-07-29 10:32:50',
        url: '/code/deleteObject',
        content: '删除了数据对象T_KY_ZZRY'
      },
      {
        username: 'admin',
        optionDate: '2019-07-29 10:31:18',
        url: '/code/deleteObject',
        content: '删除了数据对象T_YKT_XFJL'
      },
      {
        username: 'admin',
        optionDate: '2019-07-29 10:30:08',
        url: '/code/deleteCode',
        content: '删除了代码表标准内容：T_CODE_MZ'
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
