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
          <div class="monitor-chart" />
        </div>
      </div>
      <div class="monitor-chart-col">
        <div class="monitor-inner">
          <div class="m-second-tit">数据库表空间（主数据）</div>
          <div class="monitor-count">
            <span>已使用容量：1686M</span>
            <span>表空间总容量：2048M</span>
          </div>
          <div class="monitor-chart" />
        </div>
      </div>
      <div class="monitor-chart-col">
        <div class="monitor-inner">
          <div class="m-second-tit">数据库表空间（数据集成库）</div>
          <div class="monitor-count">
            <span>已使用容量：16286M</span>
            <span>表空间总容量：22048M</span>
          </div>
          <div class="monitor-chart" />
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
            :data="tableData"
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
            :data="tableData"
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
              prop="state"
              label="耗时"
              width="100"
            />
            <el-table-column
              prop="machine"
              label="CPU时间"
              width="100"
            />
            <el-table-column
              prop="program"
              label="磁盘读写速率"
              width="100"
            />
            <el-table-column
              prop="order"
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
export default {
  data() {
    return {
      tableData: [{
        user: 'user',
        desc: '描述描述描述',
        state: 'xx',
        machine: 'xxx',
        program: 'xxx',
        order: 'xxxx'
      }, {
        user: 'user',
        desc: '描述描述描述',
        state: 'xx',
        machine: 'xxx',
        program: 'xxx',
        order: 'xxxx',
        time: '2019-02-04 19:22:11',
        count: '20',
        size: '1000'
      }, {
        user: 'user',
        desc: '描述描述描述',
        state: 'xx',
        machine: 'xxx',
        program: 'xxx',
        order: 'xxxx',
        time: '2019-02-04 19:22:11',
        count: '20',
        size: '1000'
      }, {
        user: 'user',
        desc: '描述描述描述',
        state: 'xx',
        machine: 'xxx',
        program: 'xxx',
        order: 'xxxx',
        time: '2019-02-04 19:22:11',
        count: '20',
        size: '1000'
      }, {
        user: 'user',
        desc: '描述描述描述',
        state: 'xx',
        machine: 'xxx',
        program: 'xxx',
        order: 'xxxx',
        time: '2019-02-04 19:22:11',
        count: '20',
        size: '1000'
      }]
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
      height: 160px;
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
