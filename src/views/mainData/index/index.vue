<template>
  <div class="g-container">
    <div class="dashboard-box">
      <h2 class="dashboard-tit c-overview">概况</h2>
      <div class="dashboard-data">
        <div class="dashboard-col">
          <section>
            <h1>489</h1>
            <p>总数据数</p>
          </section>
        </div>
        <div class="dashboard-col">
          <section>
            <h1>300</h1>
            <p>集成数据</p>
          </section>
        </div>
        <div class="dashboard-col">
          <section>
            <h1>600w+</h1>
            <p>数据资产</p>
          </section>
        </div>
      </div>
    </div>
    <div class="dashboard-box">
      <h2 class="dashboard-tit c-counter">数据量TOP10</h2>
      <div class="data-statistics">
        <div class="statistics-col">
          <div class="statistics-chart">
            <div ref="dmChart" style="height:90%;width:90%;" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
export default {
  name: 'MainData',
  data() {
    return {
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
      }
    }
  },
  mounted() {
    this.initDmChart()
  },
  methods: {
    initDmChart() {
      this.dmChart = echarts.init(this.$refs.dmChart)
      this.dmChart.setOption(this.dmOptions)
    }
  }
}
</script>
<style scoped="scoped" lang="scss">
  .dashboard-tit {
    position: relative;
    color: #333;
    font-size: 24px;
    font-weight: normal;
    margin: 0;
    padding: 10px 0 10px 15px;
    &:before{
      position: absolute;
      left: 0;
      top:50%;
      width: 4px;
      height: 20px;
      content: "";
      margin-top: -10px;
    }
    &.c-counter{
      color: #3775ff;
      &:before{
        background: #3775ff;
      }
    }
    &.c-overview{
      color:#F56C6C;
      &:before{
        background: #F56C6C;
      }
    }
  }
.dashboard-data {
  padding: 20px 0;
  margin-left: -20px;
  &:after {
    content: '';
    font-size: 0;
    display: block;
    height: 0;
    clear: both;
    visibility: hidden;
  }
  .dashboard-col {
    position: relative;
    width: 30%;
    min-width: 280px;
    height: 160px;
    color: #fff;
    font-size: 18px;
    text-align: center;
    float: left;
    margin: 0 0 20px 20px;
    display: table;
    word-break: keep-all;
    white-space: nowrap;
    overflow: hidden;
    border-radius: 5px;
    background-color: #5d95ff;
    background: linear-gradient(to right, #6bb5ff, #5d95ff);
    section{
      display: table-cell;
      vertical-align: middle;
    }
    &:nth-child(2) {
      background-color: #f08d36;
      background: linear-gradient(to right, #fab83b, #f08d36);
    }
    &:nth-child(3) {
      background-color: #2f9fc9;
      background: linear-gradient(to right, #48c5bf, #2f9fc9);
    }
    &:nth-child(4) {
      background-color: #8f60f2;
      background: linear-gradient(to right, #ad71e9, #8f60f2);
    }
    &:nth-child(5) {
      background-color: #019b65;
      background: linear-gradient(to right, #0edd94, #019b65);
    }
    &:nth-child(6) {
      background-color: #e44c3e;
      background: linear-gradient(to right, #ec6955, #e44c3e);
    }
    h1{
      font-size: 48px;
      line-height: 1.3;
      margin: 0;
      font-weight: normal;
    }
    p{
      font-size: 16px;
      margin: 0;
    }
  }
}
.data-statistics {
  font-size: 0;
  padding: 20px 0;
  margin-left: -20px;
  .statistics-col {
    width: 100%;
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
