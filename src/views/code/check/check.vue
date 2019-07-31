<template>
  <div class="app-container">
    <el-tabs v-model="activeName" type="card">
      <el-tab-pane label="概况" name="first">
        <div class="data-statistics">
          <div class="statistics-col">
            <div class="statistics-chart">
              <div ref="dmChart" style="height:90%;width:90%;" />
            </div>
          </div>
          <div class="statistics-col">
            <div class="statistics-chart">
              <div ref="dmChart2" style="height:90%;width:90%;" />
            </div>
          </div>
        </div>
      </el-tab-pane>
      <el-tab-pane label="待处理" name="second">
        <el-row class="m-filter-row">
          <el-col class="filter-label" :span="1" align justify>标准代码：</el-col>
          <el-col class="mr-20" :span="4" align justify>
            <el-input v-model="input1" placeholder="请输入内容" />
          </el-col>
          <el-col class="filter-label" :span="1" align justify>业务代码：</el-col>
          <el-col class="mr-20" :span="4" align justify>
            <el-input v-model="input2" placeholder="请输入内容" />
          </el-col>
          <el-col class="filter-label" :span="1" align justify>数据源：</el-col>
          <el-col class="mr-20" :span="4" align justify>
            <el-select v-model="input3" placeholder="请选择数据源" clearable>
              <el-option label="教育管理基础" value="1" />
              <el-option label="教育行政管理" value="2" />
              <el-option label="高等学校管理" value="3" />
              <el-option label="教育统计" value="4" />
            </el-select>
          </el-col>
        </el-row>
        <el-row>
          <el-col>
            <el-button icon="el-icon-search" type="primary">查询</el-button>
            <el-button icon="el-icon-refresh" type="success">重置</el-button>
            <el-button type="warning">重新检测</el-button>
            <el-button icon="el-icon-download" type="info">导出</el-button>
          </el-col>
        </el-row>
        <el-table ref="table1" :data="tableData1" tooltip-effect="dark" style="width: 100%">
          <el-table-column prop="id" label="ID" />
          <el-table-column prop="code" label="标准代码" />
          <el-table-column prop="source" label="数据源" />
          <el-table-column prop="bussinessCode" label="业务代码" />
          <el-table-column prop="dataFlow" label="数据流向" />
          <el-table-column prop="checkResult" label="检查结果" />
          <el-table-column prop="checkTime" label="检查时间" />
        </el-table>
        <el-pagination background layout="prev, pager, next" :total="1000" />
      </el-tab-pane>
      <el-tab-pane label="已处理" name="third">
        <el-row class="m-filter-row">
          <el-col class="filter-label" :span="1" align justify>标准代码：</el-col>
          <el-col class="mr-20" :span="4" align justify>
            <el-input v-model="input1" placeholder="请输入内容" />
          </el-col>
          <el-col class="filter-label" :span="1" align justify>业务代码：</el-col>
          <el-col class="mr-20" :span="4" align justify>
            <el-input v-model="input2" placeholder="请输入内容" />
          </el-col>
          <el-col class="filter-label" :span="1" align justify>数据源：</el-col>
          <el-col class="mr-20" :span="4" align justify>
            <el-select v-model="input3" placeholder="请选择数据源" clearable>
              <el-option label="教育管理基础" value="1" />
              <el-option label="教育行政管理" value="2" />
              <el-option label="高等学校管理" value="3" />
              <el-option label="教育统计" value="4" />
            </el-select>
          </el-col>
        </el-row>
        <el-row>
          <el-col>
            <el-button icon="el-icon-search" type="primary">查询</el-button>
            <el-button icon="el-icon-refresh" type="success">重置</el-button>
            <el-button icon="el-icon-download" type="info">导出</el-button>
          </el-col>
        </el-row>
        <el-table ref="table1" :data="tableData2" tooltip-effect="dark" style="width: 100%">
          <el-table-column prop="id" label="ID" />
          <el-table-column prop="code" label="标准代码" />
          <el-table-column prop="source" label="数据源" />
          <el-table-column prop="bussinessCode" label="业务代码" />
          <el-table-column prop="dataFlow" label="数据流向" />
          <el-table-column prop="checkResult" label="检查结果" />
          <el-table-column prop="checkTime" label="检查时间" />
          <el-table-column prop="updateTime" label="处理时间" />
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
      dmChart: null,
      activeName: 'first',
      input1: '',
      input2: '',
      input3: '',
      dmOptions1: {
        title: {
          text: '总体情况(记录)'
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
          data: ['教育管理基础1', '教育行政管理', '高等学校管理', '教育统计']
        },
        series: [
          {
            name: '代码标准(表数量)',
            type: 'bar',
            data: [100, 500, 1500, 2200]
          }
        ]
      },
      dmOptions2: {
        title: {
          text: '总体情况(记录)'
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
          data: ['教育管理基础2', '教育行政管理', '高等学校管理', '教育统计']
        },
        series: [
          {
            name: '代码标准(表数量)',
            type: 'bar',
            data: [100, 500, 1500, 2200]
          }
        ]
      },
      tableData1: [
        {
          id: '1',
          code: 'SFBZ(DM)',
          source: '代码标准',
          bussinessCode: 'GXXX0101',
          dataFlow: '下行',
          checkResult: '不一致',
          checkTime: '2019-01-02'
        }, {
          id: '2',
          code: 'SFBZ(DM)',
          source: '代码标准',
          bussinessCode: 'GXXX0101',
          dataFlow: '下行',
          checkResult: '不一致',
          checkTime: '2019-01-02'
        }, {
          id: '3',
          code: 'SFBZ(DM)',
          source: '代码标准',
          bussinessCode: 'GXXX0101',
          dataFlow: '下行',
          checkResult: '不一致',
          checkTime: '2019-01-02'
        }
      ],
      tableData2: [
        {
          id: '1',
          code: 'SFBZ(DM)',
          source: '代码标准',
          bussinessCode: 'GXXX0101',
          dataFlow: '下行',
          checkResult: '不一致',
          checkTime: '2019-01-02',
          updateTime: '2019-01-14'
        }, {
          id: '2',
          code: 'SFBZ(DM)',
          source: '代码标准',
          bussinessCode: 'GXXX0101',
          dataFlow: '下行',
          checkResult: '不一致',
          checkTime: '2019-01-02',
          updateTime: '2019-01-14'
        }, {
          id: '3',
          code: 'SFBZ(DM)',
          source: '代码标准',
          bussinessCode: 'GXXX0101',
          dataFlow: '下行',
          checkResult: '不一致',
          checkTime: '2019-01-02',
          updateTime: '2019-01-14'
        }]
    }
  },
  mounted() {
    this.initDmChart()
  },
  methods: {
    initDmChart() {
      this.dmChart = echarts.init(this.$refs.dmChart)
      this.dmChart.setOption(this.dmOptions1)

      this.dmChart2 = echarts.init(this.$refs.dmChart2)
      this.dmChart2.setOption(this.dmOptions2)
    },
    onSubmit() {
      this.$message({
        message: '保存成功',
        type: 'success'
      })
    },
    manualSubmit() {
      this.$message({
        message: '手动执行成功',
        type: 'success'
      })
    },
    handleSearch() {
      this.$message({
        message: '搜索成功',
        type: 'success'
      })
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
.data-statistics {
  font-size: 0;
  padding: 20px 0;
  margin-left: -20px;
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
}
</style>

