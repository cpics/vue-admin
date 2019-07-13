<template>
  <div class="g-container">
    <el-collapse v-model="activeNames" @change="handleChange">
      <el-collapse-item title="按规则统计检测项" name="1">
        <div class="rule-chart">
          <div ref="barChart" style="height:90%;width:90%" />
        </div>
      </el-collapse-item>
      <el-collapse-item title="按规则统计违规率" name="2">
        <div class="violation-chart">
          <div class="violation-col">
            <div class="violation-tit">空值</div>
            <div class="viol-chart">
              <div ref="guChart" style="width:90%;height:90%" />
            </div>
          </div>
          <div class="violation-col">
            <div class="violation-tit">编号不是纯数字</div>
            <div class="viol-chart">
              <div ref="guChart2" style="width:90%;height:90%" />
            </div>
          </div>
          <div class="violation-col">
            <div class="violation-tit">数字超出正常范围</div>
            <div class="viol-chart">
              <div ref="guChart3" style="width:90%;height:90%" />
            </div>
          </div>
          <div class="violation-col">
            <div class="violation-tit">不唯一</div>
            <div class="viol-chart">
              <div ref="guChart4" style="width:90%;height:90%" />
            </div>
          </div>
        </div>
      </el-collapse-item>
      <el-collapse-item title="数TOP10表" name="3">
        <el-table
          :data="tableTop"
          border
          style="width: 100%"
        >
          <el-table-column
            prop="name"
            label="表名"
          />
          <el-table-column
            prop="number"
            label="违规数"
          />
        </el-table>
      </el-collapse-item>
    </el-collapse>

  </div>
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme

export default {
  data() {
    return {
      tableTop: [{
        name: '表名表名表名表名表名表名表名表名表名表名表名',
        number: '88885511'
      }, {
        name: '表名表名表名表名表名表名表名表名表名表名表名',
        number: '88885511'
      }, {
        name: '表名表名表名表名表名表名表名表名表名表名表名',
        number: '88885511'
      }, {
        name: '表名表名表名表名表名表名表名表名表名表名表名',
        number: '88885511'
      }],
      activeNames: ['1', '2', '3'],
      barChart: null,
      guChart: null,
      guChart2: null,
      guChart3: null,
      guChart4: null,
      guOptions: {
        tooltip: {
          formatter: '{a} <br/>{b} : {c}%'
        },
        toolbox: {
          feature: {
            restore: {},
            saveAsImage: {}
          }
        },
        series: [
          {
            name: '业务指标',
            type: 'gauge',
            detail: { formatter: '{value}%' },
            data: [{ value: 50, name: '完成率' }]
          }
        ]
      },
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
      }
    }
  },
  mounted() {
    this.initDmChart()
    this.initguChart()
  },
  methods: {
    handleChange(val) {
      console.log(val)
    },
    initDmChart() {
      this.barChart = echarts.init(this.$refs.barChart)
      this.barChart.setOption(this.dmOptions)
    },
    initguChart() {
      this.guChart = echarts.init(this.$refs.guChart)
      this.guChart.setOption(this.guOptions)

      this.guChart2 = echarts.init(this.$refs.guChart2)
      this.guChart2.setOption(this.guOptions)

      this.guChart3 = echarts.init(this.$refs.guChart3)
      this.guChart3.setOption(this.guOptions)

      this.guChart4 = echarts.init(this.$refs.guChart4)
      this.guChart4.setOption(this.guOptions)
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
.rule-chart{
  width: 1200px;
  height: 350px;
}
.violation-chart{
  font-size: 0;
  padding: 20px 0;
  margin-left: -20px;
  .violation-col{
    width: 260px;
    color: #333;
    font-size: 16px;
    text-align: center;
    display: inline-block;
    margin-left: 20px;
  }
  .viol-chart{
    width: 240px;
    height: 240px;
    margin: 0 auto;
  }
}
</style>
