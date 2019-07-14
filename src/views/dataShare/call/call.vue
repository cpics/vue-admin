<template>
  <div class="g-container">
    <div class="chart-wrapper">
      <div class="common-title">
        数据调用统计
      </div>
      <div class="chart-box">
        <div
          ref="dataChart"
          style="width:90%;height:90%"
        />
      </div>
    </div>
    <div>
      <el-form>
        <el-form-item>
          <el-select
            v-model="value"
            placeholder="默认排序"
          >
            <el-option
              label="时间升序"
              value="0"
            />
            <el-option
              label="时间倒序"
              value="1"
            />
            <el-option
              label="申请降序"
              value="2"
            />
            <el-option
              label="时间升序"
              value="3"
            />
          </el-select>
        </el-form-item>
        <el-form-item>
          <el-input />
        </el-form-item>
        <el-form-item>
          <el-button>查询</el-button>
        </el-form-item>
      </el-form>

      <div>
        <ul>
          <li>
            <div>人员基本信息</div>
            <div>申请次数:30</div>
            <div>最近调用：2019/07/01 09:06:3</div>
            <div class="center">21/3/6</div>
          </li>
          <li>
            <div>人员基本信息</div>
            <div>申请次数:30</div>
            <div>最近调用：2019/07/01 09:06:3</div>
            <div class="center">21/3/6</div>
          </li>
        </ul>
      </div>
    </div>
  </div>

</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
export default {
  data() {
    return {
      dataChart: null,
      dataOptions: {
        legend: {},
        tooltip: {},
        dataset: {
          dimensions: ['product', '违法', '失败', '成功'],
          source: [
            { product: '人员基本信息', '违法': 43.3, '失败': 85.8, '成功': 93.7 },
            { product: '学生基本信息', '违法': 83.1, '失败': 73.4, '成功': 55.1 },
            { product: '教职工缴费查询', '违法': 86.4, '失败': 65.2, '成功': 82.5 },
            { product: '叫时刻表查询', '违法': 72.4, '失败': 53.9, '成功': 39.1 }
          ]
        },
        xAxis: { type: 'category' },
        yAxis: {},
        // Declare several bar series, each will be mapped
        // to a column of dataset.source by default.
        series: [
          { type: 'bar' },
          { type: 'bar' },
          { type: 'bar' }
        ]
      },
      value: ''
    }
  },
  mounted() {
    this.initDmChart()
  },
  methods: {
    initDmChart() {
      this.dataChart = echarts.init(this.$refs.dataChart)
      this.dataChart.setOption(this.dataOptions)
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
.chart-box {
    height: 400px;
    padding-bottom: 30px;
}
</style>
