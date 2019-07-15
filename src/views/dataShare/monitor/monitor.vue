<template>
  <div class="g-container">
    <div class="double-columns tem-rule-main">
      <div class="column-left">
        <div class="border-box tem-rule-tree">
          <el-input
            v-model="filterText"
            placeholder="数据目录"
          />
          <el-tree
            ref="tree"
            class="filter-tree"
            :data="data"
            :props="defaultProps"
            default-expand-all
            :filter-node-method="filterNode"
          />
        </div>
      </div>
      <div class="column-right">
        <div class="border-box">
          <el-row class="m-filter-row">
            <el-col class="filter-label w-60" :span="2">状态：</el-col>
            <el-col class="mr-20" :span="6">
              <el-select
                v-model="form.template"
                placeholder="请选择"
              >
                <el-option
                  label="成功"
                  value="1"
                />
                <el-option
                  label="失败"
                  value="2"
                />
                <el-option
                  label="违法"
                  value="3"
                />
              </el-select>
            </el-col>
            <el-col class="filter-label w-60" :span="4">日期：</el-col>
            <el-col :span="12">
              <el-date-picker
                v-model="form.date"
                type="daterange"
                range-separator="至"
                start-placeholder="开始日期"
                end-placeholder="结束日期"
              />
            </el-col>
          </el-row>
          <div class="m-buttons-row">
            <el-button type="primary" icon="el-icon-search">查询</el-button>
            <el-button type="success" icon="el-icon-eye" @click="showDia">监控</el-button>
          </div>
          <el-table
            ref="multipleTable"
            :data="tableData"
            tooltip-effect="dark"
            style="width: 100%"
            @selection-change="wFilterTableData"
          >
            <el-table-column
              type="selection"
              width="55"
            />
            <el-table-column
              prop="id"
              label="ID"
            />
            <el-table-column
              prop="fwName"
              label="服务名"
            />
            <el-table-column
              prop="ywy"
              label="业务域"
            />
            <el-table-column
              prop="sqID"
              label="申请ID"
            />
            <el-table-column
              prop="state"
              label="调用状态"
            />
            <el-table-column
              prop="rzxx"
              label="日志信息"
            />
            <el-table-column
              prop="date"
              label="调用日期"
            />
          </el-table>
          <el-pagination background layout="prev, pager, next" :total="1000" />
        </div>
      </div>
    </div>
    <el-dialog
      title="监控"
      :visible.sync="dialogFormVisible"
    >
      <div class="jk-pop">
        <div ref="jkPopChart" style="width:90%;height:90%" />
      </div>
    </el-dialog>
  </div>
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
export default {

  data() {
    return {
      jkPopChart: null,
      jkOptions: {
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
            data: ['成功', '失败', '非法'],
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
            data: [10, 52, 200]
          }
        ]
      },
      type: 1, // 1代表添加，2代表修改
      multipleSelection: [],
      popSelection: [],
      filterText: '',
      form: {
        template: '',
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        content: '',
        desc: ''
      },
      formLabelWidth: '120px',
      tableData: [
        {
          id: 0,
          fwName: '人员基本信息',
          ywy: '人事',
          sqID: '001',
          state: '200',
          rzxx: 'successful',
          date: '2019-06-20 17:28:37.0'
        },
        {
          id: 2,
          fwName: '人员基本信息',
          ywy: '人事',
          sqID: '001',
          state: '200',
          rzxx: 'successful',
          date: '2019-06-20 17:28:37.0'
        }
      ],
      dialogFormVisible: false,
      data: [{
        id: 1,
        label: '一级 1',
        children: [{
          id: 4,
          label: '二级 1-1',
          children: [{
            id: 9,
            label: '三级 1-1-1'
          }, {
            id: 10,
            label: '三级 1-1-2'
          }]
        }]
      }, {
        id: 2,
        label: '一级 2',
        children: [{
          id: 5,
          label: '二级 2-1'
        }, {
          id: 6,
          label: '二级 2-2'
        }]
      }, {
        id: 3,
        label: '一级 3',
        children: [{
          id: 7,
          label: '二级 3-1'
        }, {
          id: 8,
          label: '二级 3-2'
        }]
      }],
      defaultProps: {
        children: 'children',
        label: 'label'
      }
    }
  },
  watch: {
    filterText(val) {
      this.$refs.tree.filter(val)
    }
  },
  mounted() {
    // this.initJkChart()
  },
  methods: {
    initJkChart() {
      console.log(this.$refs.jkPopChart)
      this.jkPopChart = echarts.init(this.$refs.jkPopChart)
      this.jkPopChart.setOption(this.jkOptions)
    },
    showDia() {
      this.dialogFormVisible = !this.dialogFormVisible
      if (this.dialogFormVisible) {
        this.$nextTick(() => {
          this.initJkChart()
        })
      }
    },
    filterNode(value, data) {
      if (!value) return true
      return data.label.indexOf(value) !== -1
    },

    wFilterTableData(val) {
      this.multipleSelection = val
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
.tem-rule-main {
    .tem-rule-tree {
        .el-input {
            margin-bottom: 10px;
        }
    }
}
.jk-pop{
  width:600px;
  height:400px;
}
</style>
