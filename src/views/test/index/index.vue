<template>
  <div class="g-container">
    <el-collapse accordion>
      <el-collapse-item title="按规则统计检测项">
        <div class="rule-chart" />
      </el-collapse-item>
      <el-collapse-item title="按规则统计违规率">
        <div class="violation-chart">
          <div class="violation-col">
            <div class="violation-tit">空值</div>
            <div class="viol-chart" />
          </div>
          <div class="violation-col">
            <div class="violation-tit">编号不是纯数字</div>
            <div class="viol-chart" />
          </div>
          <div class="violation-col">
            <div class="violation-tit">数字超出正常范围</div>
            <div class="viol-chart" />
          </div>
          <div class="violation-col">
            <div class="violation-tit">不唯一</div>
            <div class="viol-chart" />
          </div>
        </div>
      </el-collapse-item>
      <el-collapse-item title="数TOP10表">
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
      }]
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
