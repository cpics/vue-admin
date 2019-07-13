<template>
  <div class="g-container">
    <div class="dashboard-box">
      <h1 class="dashboard-tit">数据概览</h1>
      <div class="dashboard-data">
        <div class="dashboard-col">业务系统数量：50</div>
        <div class="dashboard-col">代码标准数量：300</div>
        <div class="dashboard-col">数据标准数量：200</div>
        <div class="dashboard-col">数据建设数量：80</div>
        <div class="dashboard-col">今日访客数量：300</div>
        <div class="dashboard-col">历史访问数量：100000</div>
      </div>
    </div>
    <div class="dashboard-box">
      <h1 class="dashboard-tit">数据统计</h1>
      <div class="data-statistics">
        <div class="statistics-col">
          <div class="statistics-tit">代码标准表统计</div>
          <div class="statistics-chart" />
        </div>
        <div class="statistics-col">
          <div class="statistics-tit">代码数据量统计</div>
          <div class="statistics-chart" />
        </div>
        <div class="statistics-col">
          <div class="statistics-tit">主数据标准统计</div>
          <div class="statistics-chart" />
        </div>
        <div class="statistics-col">
          <div class="statistics-tit">主数据字段统计</div>
          <div class="statistics-chart" />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'Dashboard',
  data() {
    return {

    }
  },
  computed: {
    ...mapGetters([
      'roles'
    ])
  },
  created() {

  }
}
</script>
<style scoped="scoped" lang="scss">
  .dashboard-tit{
    color: #333;
    font-size: 24px;
    font-weight: normal;
    margin: 0;
    padding: 10px 0;
  }
  .dashboard-data{
    font-size: 0;
    padding: 20px 0;
    margin-left: -20px;
    max-width: 1000px;
    .dashboard-col{
      width: 300px;
      height: 160px;
      color: #fff;
      font-size: 18px;
      text-align: center;
      line-height: 160px;
      display: inline-block;
      margin: 0 0 20px 20px;
      word-break: keep-all;
      white-space: nowrap;
      overflow: hidden;
      border-radius: 5px;
      background-color: #5d95ff;
      background: linear-gradient(to right,#6bb5ff,#5d95ff);
      &:nth-child(2){
        background-color: #f08d36;
        background: linear-gradient(to right,#fab83b,#f08d36);
      }
      &:nth-child(3){
        background-color: #2f9fc9;
        background: linear-gradient(to right,#48c5bf,#2f9fc9);
      }
      &:nth-child(4){
        background-color: #8f60f2;
        background: linear-gradient(to right,#ad71e9,#8f60f2);
      }
      &:nth-child(5){
        background-color: #019b65;
        background: linear-gradient(to right,#0edd94,#019b65);
      }
      &:nth-child(6){
        background-color: #e44c3e;
        background: linear-gradient(to right,#ec6955,#e44c3e);
      }
    }
  }
  .data-statistics{
    font-size: 0;
    padding: 20px 0;
    margin-left: -20px;
    .statistics-col{
      width: 450px;
      color: #333;
      font-size: 16px;
      display: inline-block;
      margin-left: 20px;
      .statistics-tit{
        padding: 0 0 10px;
      }
      .statistics-chart{
        width: 450px;
        height: 280px;
        margin-bottom: 15px;
      }
    }
  }
</style>
