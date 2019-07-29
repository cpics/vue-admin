<template>
  <div class="g-container">
    <div class="monitor-chart">
      <div class="monitor-chart-col">
        <div class="monitor-inner">
          <div class="m-second-tit">数据库连接数</div>
          <div class="monitor-count">
            <span>当前数据库连接数：175个</span>
            <span>最大连接数：10000个</span>
          </div>
          <div class="monitor-chart">
            <div ref="mChart1" style="width:90%;height:90%;" />
          </div>
        </div>
      </div>
      <div class="monitor-chart-col">
        <div class="monitor-inner">
          <div class="m-second-tit">数据库表空间（主数据）</div>
          <div class="monitor-count">
            <span>已使用容量：1686M</span>
            <span>表空间总容量：2048M</span>
          </div>
          <div class="monitor-chart">
            <div ref="mChart2" style="width:90%;height:90%;" />
          </div>
        </div>
      </div>
      <div class="monitor-chart-col">
        <div class="monitor-inner">
          <div class="m-second-tit">数据库表空间（数据集成库）</div>
          <div class="monitor-count">
            <span>已使用容量：16286M</span>
            <span>表空间总容量：22048M</span>
          </div>
          <div class="monitor-chart">
            <div ref="mChart3" style="width:90%;height:90%;" />
          </div>
        </div>
      </div>
    </div>
    <div class="double-average">
      <div class="average-col">
        <div class="average-box">
          <div class="m-second-tit">数据库死锁</div>
          <el-table
            :data="tableData"
            style="width: 100%"
            max-height="250"
          >
            <el-table-column
              prop="user"
              label="数据库用户"
              width="100"
            />
            <el-table-column
              prop="desc"
              label="死锁内容描述"
            />
            <el-table-column
              prop="state"
              label="死锁状态"
              width="100"
            />
            <el-table-column
              prop="machine"
              label="机器"
              width="80"
            />
            <el-table-column
              prop="program"
              label="应用程序"
              width="100"
            />
            <el-table-column
              prop="order"
              label="顺序号"
              width="80"
            />
          </el-table>
        </div>
        <div class="average-box">
          <div class="m-second-tit">归档日志</div>
          <el-table
            :data="tableData3"
            style="width: 100%"
            max-height="250"
          >
            <el-table-column
              prop="time"
              label="归档日期"
            />
            <el-table-column
              prop="count"
              label="日志总数"
            />
            <el-table-column
              prop="size"
              label="日志大小(M)"
            />
          </el-table>
        </div>
      </div>
      <div class="average-col">
        <div class="average-box">
          <div class="m-second-tit">总耗时最大前十条SQL</div>
          <el-table
            :data="tableData2"
            style="width: 100%"
            max-height="520"
          >
            <el-table-column
              prop="user"
              label="用户名"
              width="100"
            />
            <el-table-column
              prop="desc"
              label="SQL语句"
            />
            <el-table-column
              prop="time"
              label="耗时"
              width="100"
            />
            <el-table-column
              prop="cpu"
              label="CPU时间"
              width="100"
            />
            <el-table-column
              prop="rate"
              label="磁盘读写速率"
              width="100"
            />
            <el-table-column
              prop="sort"
              label="消耗排名"
              width="80"
            />
          </el-table>
        </div>
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
      mChart1: null,
      mChart2: null,
      mChart3: null,
      mOptions1: {
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
            radius: '100%',
            detail: { formatter: '{value}%' },
            data: [{ value: 50 }]
          }
        ]
      },
      mOptions2: {
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
            radius: '100%',
            detail: { formatter: '{value}%' },
            data: [{ value: 60 }]
          }
        ]
      },
      mOptions3: {
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
            radius: '100%',
            detail: { formatter: '{value}%' },
            data: [{ value: 70 }]
          }
        ]
      },
      tableData: [],
      tableData2: [{
        user: 'admin',
        desc: 'select * from base_resources where isValid=1 order by sort',
        time: '175ms',
        cpu: '160ms',
        rate: '20.1MB/s',
        sort: '1'
      }, {
        user: 'admin',
        desc: 'select * from task_schedule',
        time: '150ms',
        cpu: '140ms',
        rate: '19.6MB/s',
        sort: '2'
      }, {
        user: 'admin',
        desc: 'select * from base_account_role',
        time: '145ms',
        cpu: '140ms',
        rate: '20.2MB/s',
        sort: '3'
      }, {
        user: 'admin',
        desc: 'select * from tb_rpt_dbcfg',
        time: '100ms',
        cpu: '98ms',
        rate: '24.4MB/s',
        sort: '4'
      }, {
        user: 'admin',
        desc: 'select count(*) from standard_log',
        time: '68ms',
        cpu: '60ms',
        rate: '22.8MB/s',
        sort: '5'
      }],
      tableData3: [{
        time: '2019-06-29',
        count: '20',
        size: '414'
      }, {
        time: '2019-07-06',
        count: '22',
        size: '464'
      }, {
        time: '2019-07-13',
        count: '23',
        size: '511'
      }, {
        time: '2019-07-20',
        count: '26',
        size: '534'
      }]
    }
  },
  mounted() {
    this.initDmChart()
  },
  methods: {
    initDmChart() {
      console.log(this.$refs.mChart1)
      this.mChart1 = echarts.init(this.$refs.mChart1)
      this.mChart1.setOption(this.mOptions1)

      this.mChart2 = echarts.init(this.$refs.mChart2)
      this.mChart2.setOption(this.mOptions2)

      this.mChart3 = echarts.init(this.$refs.mChart3)
      this.mChart3.setOption(this.mOptions3)
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
  .double-average,
  .monitor-chart {
    &:after {
      content: "";
      font-size: 0;
      display: block;
      height: 0;
      clear: both;
      visibility: hidden;
    }
  }

  .m-second-tit {
    position: relative;
    font-size: 16px;
    padding: 5px 0 5px 13px;
    &:before {
      position: absolute;
      left: 0;
      top: 50%;
      width: 3px;
      height: 14px;
      content: "";
      margin-top: -7px;
      background: #409eff;
    }
  }

  .monitor-chart {
    .monitor-chart-col {
      width: 33.33%;
      padding-right: 20px;
      float: left;
      margin-bottom: 20px;
      box-sizing: border-box;
      .monitor-inner{
        min-width: 280px;
        padding: 15px;
        border: 1px solid #e4e4e4;
        border-radius: 5px;
      }
    }
    .monitor-count {
      color: #555;
      text-align: center;
      line-height: 24px;
      min-height: 48px;
      padding-top: 5px;
      span {
        font-size: 14px;
        display: inline-block;
        margin: 0 15px;
      }
    }
    .monitor-chart {
      width: 100%;
      height: 200px;
    }
  }

  .double-average {
    margin-bottom: 20px;
    .average-col {
      width: 50%;
      padding-right: 20px;
      float: left;
      box-sizing: border-box;
    }
    .average-box {
      padding: 20px;
      border: 1px solid #e4e4e4;
      border-radius: 5px;
      margin-bottom: 20px;
    }
  }
</style>
