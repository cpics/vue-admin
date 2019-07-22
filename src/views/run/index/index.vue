<template>
  <div class="g-container">
    <el-tabs v-model="activeName" type="card">
      <el-tab-pane label="集成概况" name="first">
        <div class="statistics-col">
          <div class="statistics-chart">
            <div ref="dmChart" style="height:90%;width:90%;" />
          </div>
        </div>
        <div class="statistics-col">
          <div class="statistics-tit">代码标准表统计</div>
          <el-table ref="table1" :data="tableData1" tooltip-effect="dark" style="width: 100%">
            <el-table-column :key="Math.random()" prop="name" label="接口名称" />
            <el-table-column :key="Math.random()" prop="database" label="目标库" />
            <el-table-column :key="Math.random()" prop="table" label="目标表" />
          </el-table>
        </div>
      </el-tab-pane>
      <el-tab-pane label="接口信息" name="second">
        <div class="double-columns tem-rule-main">
          <div class="column-left">
            <div class="border-box tem-rule-tree">
              <el-input v-model="filterText" placeholder="请输入关键字" />
              <el-tree
                ref="tree"
                class="filter-tree"
                :data="treeData"
                :props="defaultProps"
                default-expand-all
                :filter-node-method="filterNode"
              />
            </div>
          </div>
          <div class="column-right">
            <div class="border-box">
              <div class="m-filter-row">
                <el-form ref="formInline2" v-model="formInline2" :inline="true">
                  <el-form-item label="对象名称:" prop="formInline2.name">
                    <el-input v-model="formInline2.name" placeholder="请输入对象名称" />
                  </el-form-item>
                  <el-form-item label="接口名称:" prop="formInline2.interfaceName">
                    <el-input v-model="formInline2.interfaceName" placeholder="请输入接口名称" />
                  </el-form-item>
                  <el-form-item label="接口流向:" prop="formInline2.flow">
                    <el-select v-model="formInline2.flow" placeholder="请选择" clearable>
                      <el-option label="全部" value="0" />
                      <el-option label="单向" value="1" />
                    </el-select>
                  </el-form-item>
                  <el-form-item>
                    <el-button type="primary" icon="el-icon-search">查询</el-button>
                    <el-button type="success" icon="el-icon-refresh">重置</el-button>
                  </el-form-item>
                </el-form>
              </div>
              <el-table ref="table2" :data="tableData2" tooltip-effect="dark" style="width: 100%">
                <el-table-column :key="Math.random()" prop="name" label="接口名称" />
                <el-table-column :key="Math.random()" prop="headDatabase" label="数据源头库" />
                <el-table-column :key="Math.random()" prop="headTable" label="数据源头表" />
                <el-table-column :key="Math.random()" prop="database" label="目标库" />
                <el-table-column :key="Math.random()" prop="table" label="目标表" />
                <el-table-column :key="Math.random()" prop="flow" label="接口流向" />
                <el-table-column fixed="right" label="操作" width="50">
                  <template>
                    <el-button class="mini-btn" type="success" icon="el-icon-view" circle title="预览" />
                  </template>
                </el-table-column>
              </el-table>
              <el-pagination background layout="prev, pager, next" :total="1000" />
            </div>
          </div>
        </div>
      </el-tab-pane>
      <el-tab-pane label="任务计划" name="third">
        <div class="m-filter-row">
          <el-form ref="formInline3" v-model="formInline3" :inline="true">
            <el-row>
              <el-form-item label="项目名称：" prop="formInline3.name">
                <el-input v-model="formInline3.name" placeholder="" />
              </el-form-item>
              <el-form-item label="相关数据对象名称：" prop="formInline3.objName">
                <el-input v-model="formInline3.objName" placeholder="" />
              </el-form-item>
              <el-form-item label="接口名称：" prop="formInline3.interfaceName">
                <el-input v-model="formInline3.interfaceName" placeholder="" />
              </el-form-item>
            </el-row>
            <el-row>
              <el-form-item>
                <el-button type="primary" icon="el-icon-search">查询</el-button>
                <el-button type="success" icon="el-icon-refresh">重置</el-button>
              </el-form-item>
            </el-row>
          </el-form>
        </div>
        <el-table :data="tableData3" fit highlight-current-row style="width: 100%">
          <el-table-column prop="projectName" label="项目名称" />
          <el-table-column prop="taskName" label="任务名称" />
          <el-table-column prop="version" label="任务版本" />
          <el-table-column prop="proxyName" label="代理名称" />
          <el-table-column prop="proxyUrl" label="代理地址" />
          <el-table-column prop="plan" label="调度计划" />
          <el-table-column prop="status" label="代理状态" />
        </el-table>
        <el-pagination background layout="prev, pager, next" :total="1000" />
      </el-tab-pane>
      <el-tab-pane label="接口运行日志" name="four">
        <div class="m-filter-row">
          <el-form ref="formInline4" v-model="formInline4" :inline="true">
            <el-row>
              <el-form-item label="日期区间:" prop="formInline4.date">
                <el-date-picker
                  v-model="formInline4.date"
                  type="daterange"
                  range-separator="至"
                  start-placeholder="开始日期"
                  end-placeholder="结束日期"
                />
              </el-form-item>
              <el-form-item label="状态:" prop="formInline4.status">
                <el-select v-model="formInline4.status" clearable placeholder="请选择" style="width:160px;">
                  <el-option label="暂停" value="0" />
                  <el-option label="开始" value="1" />
                </el-select>
              </el-form-item>
              <el-form-item label="接口名称：" prop="formInline4.interfaceName">
                <el-input v-model="formInline4.interfaceName" placeholder="" />
              </el-form-item>
            </el-row>
            <el-row>
              <el-form-item>
                <el-button type="primary" icon="el-icon-search">查询</el-button>
                <el-button type="success" icon="el-icon-refresh">重置</el-button>
              </el-form-item>
            </el-row>
          </el-form>
        </div>
        <el-table :data="tableData4" fit highlight-current-row style="width: 100%">
          <el-table-column prop="name" label="接口名称" />
          <el-table-column prop="location" label="接口位置" />
          <el-table-column prop="startTime" label="开始时间" />
          <el-table-column prop="totalTime" label="持续时间" />
          <el-table-column prop="status" label="状态" />
          <el-table-column prop="detail" label="详细(总操作记录/新增数/更新数/删除数)" />
          <el-table-column prop="errorDetail" label="查看错误详细" />
        </el-table>
        <el-pagination background layout="prev, pager, next" :total="1000" />
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
export default {
  data() {
    return {
      filterText: '',
      activeName: 'first',
      defaultProps: {
        children: 'children',
        label: 'label'
      },
      formInline2: {
        name: '',
        interfaceName: '',
        flow: ''
      },
      formInline3: {
        name: '',
        objName: '',
        interfaceName: ''
      },
      formInline4: {
        date: '',
        status: '',
        interfaceName: ''
      },
      dmChart: null,
      dmOptions: {
        title: {
          text: '执行时间最长的前10的接口'
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
          }
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: {
          type: 'value',
          boundaryGap: [0, 0.01]
        },
        yAxis: {
          type: 'category',
          data: ['FACE_1', 'FACE_2', 'FACE_3', 'FACE_4', 'FACE_5', 'FACE_6', 'FACE_7', 'FACE_8', 'FACE_9', 'FACE_10']
        },
        series: [
          {
            name: '执行时间最长的前10的接口',
            type: 'bar',
            data: ['50', '150', '250', '350', '450', '550', '650', '750', '850', '950']
          }
        ]
      },
      treeData: [{
        id: 1,
        label: '所有服务',
        children: [{
          id: 4,
          label: '人事',
          children: [{
            id: 9,
            label: '教职工信息'
          }, {
            id: 10,
            label: '职称信息'
          }]
        }, {
          id: 4,
          label: '学工',
          children: [{
            id: 9,
            label: '学生信息'
          }, {
            id: 10,
            label: '贫困生信息'
          }]
        }, {
          id: 4,
          label: '教务',
          children: [{
            id: 9,
            label: '调课信息'
          }, {
            id: 10,
            label: '排课信息'
          }]
        },
        {
          id: 4,
          label: '财务',
          children: [{
            id: 9,
            label: '项目经费信息'
          }, {
            id: 10,
            label: '部门报销信息'
          }]
        }, {
          id: 4,
          label: '科研',
          children: [{
            id: 9,
            label: '项目信息'
          }]
        }, {
          id: 4,
          label: '资产',
          children: [{
            id: 9,
            label: '教师公寓信息'
          }]
        }, {
          id: 4,
          label: '其他',
          children: [{
            id: 9,
            label: '图书借阅信息'
          }]
        }
        ]
      }],
      tableData1: [
        {
          name: 'INTERFACE_1',
          database: '主数据(zsj)',
          table: '图书借阅信息'
        },
        {
          name: 'INTERFACE_1',
          database: '主数据(zsj)',
          table: '图书借阅信息'
        },
        {
          name: 'INTERFACE_1',
          database: '主数据(zsj)',
          table: '图书借阅信息'
        },
        {
          name: 'INTERFACE_1',
          database: '主数据(zsj)',
          table: '图书借阅信息'
        },
        {
          name: 'INTERFACE_1',
          database: '主数据(zsj)',
          table: '图书借阅信息'
        }
      ],
      tableData2: [{
        name: 'INT_HRTOZSJ',
        headDatabase: '人事系统(ORACLE_HR)',
        headTable: '考核信息',
        database: '主数据(ORACLE_HR)',
        table: '教职工考核信息',
        flow: '上行'
      },
      {
        name: 'INT_HRTOZSJ',
        headDatabase: '人事系统(ORACLE_HR)',
        headTable: '考核信息',
        database: '主数据(ORACLE_HR)',
        table: '教职工考核信息',
        flow: '上行'
      },
      {
        name: 'INT_HRTOZSJ',
        headDatabase: '人事系统(ORACLE_HR)',
        headTable: '考核信息',
        database: '主数据(ORACLE_HR)',
        table: '教职工考核信息',
        flow: '上行'
      },
      {
        name: 'INT_HRTOZSJ',
        headDatabase: '人事系统(ORACLE_HR)',
        headTable: '考核信息',
        database: '主数据(ORACLE_HR)',
        table: '教职工考核信息',
        flow: '上行'
      }],
      tableData3: [{
        projectName: '教务系统',
        taskName: 'PAK_HR',
        version: '1.0.0',
        proxyName: '202.195.244.216',
        proxyUrl: '202.195.244.216:81',
        plan: '当前任务每天10：00执行',
        status: '成功'
      }, {
        projectName: '教务系统',
        taskName: 'PAK_HR',
        version: '1.0.0',
        proxyName: '202.195.244.216',
        proxyUrl: '202.195.244.216:81',
        plan: '当前任务每天10：00执行',
        status: '成功'
      }, {
        projectName: '教务系统',
        taskName: 'PAK_HR',
        version: '1.0.0',
        proxyName: '202.195.244.216',
        proxyUrl: '202.195.244.216:81',
        plan: '当前任务每天10：00执行',
        status: '成功'
      }, {
        projectName: '教务系统',
        taskName: 'PAK_HR',
        version: '1.0.0',
        proxyName: '202.195.244.216',
        proxyUrl: '202.195.244.216:81',
        plan: '当前任务每天10：00执行',
        status: '成功'
      }],
      tableData4: [{
        name: 'INT_ZHGL',
        location: '综合管理>第一个文件夹',
        startTime: '2018-10-30 14:15:10',
        totalTime: '10秒',
        status: '完成',
        detail: '6477 / 0 / 0 / 0',
        errorDetail: '成功'
      },
      {
        name: 'INT_ZHGL',
        location: '综合管理>第一个文件夹',
        startTime: '2018-10-30 14:15:10',
        totalTime: '10秒',
        status: '完成',
        detail: '6477 / 0 / 0 / 0',
        errorDetail: '成功'
      },
      {
        name: 'INT_ZHGL',
        location: '综合管理>第一个文件夹',
        startTime: '2018-10-30 14:15:10',
        totalTime: '10秒',
        status: '完成',
        detail: '6477 / 0 / 0 / 0',
        errorDetail: '成功'
      }, {
        name: 'INT_ZHGL',
        location: '综合管理>第一个文件夹',
        startTime: '2018-10-30 14:15:10',
        totalTime: '10秒',
        status: '完成',
        detail: '6477 / 0 / 0 / 0',
        errorDetail: '成功'
      }]
    }
  },
  watch: {
    filterText(val) {
      this.$refs.tree.filter(val)
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
    filterNode(value, data) {
      if (!value) return true
      return data.label.indexOf(value) !== -1
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
  .statistics-col {
    width: 46%;
    min-width: 450px;
    color: #333;
    font-size: 16px;
    display: inline-block;
    margin-left: 20px;
    .statistics-tit {
      padding: 0 0 10px;
    }
    .statistics-chart {
      width: 100%;
      height: 280px;
      margin-bottom: 15px;
    }
  }
  /*ttt*/
</style>
