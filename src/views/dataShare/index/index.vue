<template>
  <div class="g-container">
    <el-col>
      <el-col :span="12">
        <div class="grid-content bg-purple">
          <div class="sjfu-tj">
            <div class="common-title">数据服务统计</div>
            <div class="sjfu-chart e-e-chart">
              <div ref="fwChart" style="height:90%;width:90%;" />
            </div>
          </div>
          <div class="sjdy-tj">
            <div class="common-title">数据调用统计</div>
            <div class="sjdy-chart e-e-chart">
              <div ref="dyChart" style="height:90%;width:90%;" />
            </div>
          </div>
        </div>
      </el-col>
      <el-col :span="12">
        <div class="grid-content bg-purple-light">
          <div class="fw-list">
            <div class="common-title">服务使用提醒</div>
            <div class="table-list">
              <el-table
                border
                :data="tableData"
                style="width: 100%"
              >
                <el-table-column
                  prop="date"
                  label="服务名"
                />
                <el-table-column
                  prop="name"
                  label="说明"
                />
              </el-table>
            </div>
          </div>
          <div class="aq-list">
            <div class="common-title">服务安全提醒</div>
            <div class="aq-table">
              <el-table
                border
                :data="tableData2"
                style="width: 100%"
              >
                <el-table-column
                  prop="name"
                  label="服务名"
                />
                <el-table-column
                  prop="dept"
                  label="调用部门"
                />
                <el-table-column
                  prop="num"
                  label="调用次数"
                />
                <el-table-column
                  prop="date"
                  label="调用时间"
                />
              </el-table>
            </div>
          </div>
        </div>

      </el-col>
    </el-col>
  </div>
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme

export default {
  data() {
    return {
      fwChart: null,
      dyChart: null,
      tableData: [
        {
          date: '教职工基本信息',
          name: '启用未授权'
        }, {
          date: '研究生信息',
          name: '启用未授权'
        }, {
          date: '导师信息',
          name: '启用未授权'
        }
      ],
      tableData2: [
        {
          name: '教职工基本信息',
          dept: '其他',
          num: 26,
          date: '2019-07-02'

        }, {
          name: '教职工基本信息',
          dept: '其他',
          num: 25,
          date: '2019-07-02'

        }
      ],
      dyOptions: {
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
            data: ['图书借阅信息', '教师基本信息', '学生基本信息', '贫困生数据', '研究生信息'],
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
            data: [23, 52, 35, 15, 28]
          }
        ]
      },
      fwOptions: {
        title: {
          text: '数据服务统计',
          x: 'center'
        },
        series: [
          {
            name: '访问来源',
            type: 'pie',
            radius: '80%',
            center: ['50%', '60%'],
            data: [
              { value: 335, name: '启用' },
              { value: 310, name: '未启用' }
            ],
            itemStyle: {
              emphasis: {
                shadowBlur: 10,
                shadowOffsetX: 0,
                shadowColor: 'rgba(0, 0, 0, 0.5)'
              }
            }
          }
        ]
      }
    }
  },
  mounted() {
    this.initChart()
  },
  methods: {
    initChart() {
      this.fwChart = echarts.init(this.$refs.fwChart)
      this.fwChart.setOption(this.fwOptions)

      this.dyChart = echarts.init(this.$refs.dyChart)
      this.dyChart.setOption(this.dyOptions)
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
.e-e-chart {
    height: 300px;
}
  .common-h1-tit{
    padding-bottom: 25px;
  }
  .table-list{
    margin-bottom: 35px;
  }
</style>
