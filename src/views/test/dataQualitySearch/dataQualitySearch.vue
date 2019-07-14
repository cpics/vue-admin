<template>
  <div class="g-container">
    <div class="double-columns">
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
          <div class="tem-rule-filter">
            <el-form :model="form">
              <el-form-item label="规则模板" :label-width="formLabelWidth">
                <el-select v-model="form.template" placeholder="请选择">
                  <el-option label="不符合身份证号规则" value="shanghai" />
                  <el-option label="不唯一" value="beijing" />
                </el-select>
              </el-form-item>
            </el-form>
            <div class="tem-button">
              <el-button icon="el-icon-search" type="primary">查询</el-button>
              <el-button icon="el-icon-download" type="info">导出</el-button>
            </div>
          </div>
          <el-table
            :data="tableSearchData"
            style="width: 100%"
          >
            <el-table-column
              prop="obj"
              label="检测对象"
            />
            <el-table-column
              prop="field"
              label="检测字段"
            />
            <el-table-column
              prop="rule"
              label="检测规则"
            />
            <el-table-column
              prop="count"
              label="扫描量"
            />
            <el-table-column
              prop="violation"
              label="违规量"
            />
            <el-table-column
              fixed="right"
              label="操作"
              width="100"
            >
              <template>
                <el-button type="text" size="small" @click="dialogTableVisible = true">违规明细</el-button>
              </template>
            </el-table-column>
          </el-table>
        </div>
        <div class="border-box tem-rule-chart">
          <div class="tem-rule-tit">数据中心整体质量情况</div>
          <div class="tem-chart">
            <div ref="temChart" style="width:90%;height:90%" />
          </div>
        </div>
      </div>
    </div>
    <el-dialog title="明细结果" :visible.sync="dialogTableVisible">
      <el-table
        ref="multipleTable"
        :data="tableData"
        height="400"
        style="width: 100%"
      >
        <el-table-column
          prop="no"
          label="职工号"
        />
        <el-table-column
          prop="name"
          label="姓名"
        />
        <el-table-column
          prop="card"
          label="身份证件号"
        />
      </el-table>
    </el-dialog>
  </div>
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
export default {

  data() {
    return {
      filterText: '',
      form: {
        template: ''
      },
      temChart: null,
      temOptions: {
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
      formLabelWidth: '120px',
      tableSearchData: [{
        id: 0,
        obj: 'T_JZG[教职工基本信息]',
        field: 'ZGH[职工号]',
        rule: '不唯一',
        count: '999',
        violation: '123'
      }, {
        id: 1,
        obj: 'T_JZG[教职工基本信息]',
        field: 'ZGH[职工号]',
        rule: '不唯一',
        count: '999',
        violation: '123'
      }],
      tableData: [{
        id: 0,
        no: '001',
        name: '张三',
        card: '111111111111111111111111111'
      }, {
        id: 0,
        no: '001',
        name: '张三',
        card: '111111111111111111111111111'
      }, {
        id: 0,
        no: '001',
        name: '张三',
        card: '111111111111111111111111111'
      }, {
        id: 0,
        no: '001',
        name: '张三',
        card: '111111111111111111111111111'
      }, {
        id: 0,
        no: '001',
        name: '张三',
        card: '111111111111111111111111111'
      }, {
        id: 0,
        no: '001',
        name: '张三',
        card: '111111111111111111111111111'
      }],
      dialogTableVisible: false,
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
    this.initTemChart()
  },

  methods: {
    filterNode(value, data) {
      if (!value) return true
      return data.label.indexOf(value) !== -1
    },
    initTemChart() {
      this.temChart = echarts.init(this.$refs.temChart)
      this.temChart.setOption(this.temOptions)
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

  .tem-rule-chart {
    padding-top: 20px;
    font-size: 14px;
    text-align: center;
    .tem-rule-tit {
      padding-bottom: 10px;
    }
  }

  .tem-chart {
    width: 80%;
    height: 300px;
    margin: 0 auto;
  }
</style>
