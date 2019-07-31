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
      <el-row class="m-filter-row">
        <el-col class="filter-label" :span="2">默认排序：</el-col>
        <el-col class="mr-20" :span="6">
          <el-select
            v-model="value"
            placeholder=""
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
        </el-col>
        <el-col class="filter-label w-140" :span="4">人员基本信息：</el-col>
        <el-col class="mr-20" :span="6" align justify>
          <el-input v-model="input2" placeholder="请输入内容" />
        </el-col>
        <el-col :span="4">
          <el-button icon="el-icon-search" type="primary">查询</el-button>
        </el-col>
      </el-row>
      <div class="call-columns">
        <ul>
          <li>
            <div class="call-tit">人员基本信息</div>
            <div class="call-row">
              <div class="call-label">申请次数：</div>
              <div class="call-num">30</div>
            </div>
            <div class="call-row">
              <div class="call-label">最近调用：</div>
              <div class="call-num">2019/07/01 09:06:3</div>
            </div>
            <div class="call-count">21/3/6</div>
          </li>
          <li>
            <div class="call-tit">人员基本信息</div>
            <div class="call-row">
              <div class="call-label">申请次数：</div>
              <div class="call-num">30</div>
            </div>
            <div class="call-row">
              <div class="call-label">最近调用：</div>
              <div class="call-num">2019/07/01 09:06:3</div>
            </div>
            <div class="call-count">21/3/6</div>
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
          dimensions: ['product', '非法', '失败', '成功'],
          source: [
            { product: '人员基本信息', '非法': 43.3, '失败': 85.8, '成功': 93.7 },
            { product: '学生基本信息', '非法': 83.1, '失败': 73.4, '成功': 55.1 },
            { product: '教职工缴费查询', '非法': 86.4, '失败': 65.2, '成功': 82.5 },
            { product: '叫时刻表查询', '非法': 72.4, '失败': 53.9, '成功': 39.1 }
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
  .call-columns{
    ul{
      font-size: 0;
      margin-left: -20px;
    }
    li{
      width: 30%;
      min-width: 260px;
      min-height: 124px;
      font-size: 14px;
      padding: 10px;
      box-sizing: border-box;
      display: inline-block;
      margin-left: 20px;
      margin-bottom: 20px;
      border:1px solid #e4e4e4;
      border-radius: 5px;
      div{
        padding: 3px 0;
      }
      .call-row{
        &:after{
          content: "";
          font-size: 0;
          display: block;
          height: 0;
          clear: both;
          visibility: hidden;
        }
      }
      .call-label{
        min-width: 80px;
        float: left;
        text-align: right;
      }
      .call-tit{
        font-weight: bold;
        padding-bottom: 5px;
      }
      .call-num{
        margin-left: 80px;
      }
      .call-count{
        padding-left: 80px;
      }
    }
  }
</style>
