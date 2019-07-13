<template>
  <div class="app-container">
    <el-tabs v-model="activeName" type="card">
      <el-tab-pane label="定时配置" name="first">
        <el-form ref="form" v-model="form" label-width="100px">
          <el-form-item label="周期:">
            <el-col :span="12">
              <el-checkbox-group v-model="form.cycle">
                <el-checkbox label="每天" />
                <el-checkbox label="每周" />
                <el-checkbox label="每月" />
                <el-checkbox label="每年" />
              </el-checkbox-group>
            </el-col>
          </el-form-item>
          <el-form-item label="状态:">
            <el-col :span="4">
              <el-select v-model="form.status" placeholder="请选择状态" clearable>
                <el-option label="暂停" value="0" />
                <el-option label="开始" value="1" />
              </el-select>
            </el-col>
          </el-form-item>
          <el-form-item label="日期:">
            <el-col :span="4">
              <el-date-picker v-model="form.selectDate" type="date" placeholder="选择日期" style="width: 100%;" />
            </el-col>
          </el-form-item>
          <el-form-item label="星期:">
            <el-col :span="18">
              <el-checkbox-group v-model="form.week">
                <el-checkbox label="星期一" />
                <el-checkbox label="星期二" />
                <el-checkbox label="星期三" />
                <el-checkbox label="星期四" />
                <el-checkbox label="星期五" />
                <el-checkbox label="星期六" />
                <el-checkbox label="星期日" />
              </el-checkbox-group>
            </el-col>
          </el-form-item>
          <el-form-item label="时间:">
            <el-col :span="4">
              <el-time-picker v-model="form.selectTime" placeholder="选择时间" style="width: 100%;" />
            </el-col>
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="onSubmit">保存</el-button>
            <el-button type="primary" @click="manualSubmit">手动执行</el-button>
          </el-form-item>
        </el-form>
      </el-tab-pane>
      <el-tab-pane label="任务日志" name="second">
        <el-form ref="formInline" v-model="formInline" :inline="true">
          <el-form-item label="备份日期:" prop="formInline.date">
            <el-date-picker v-model="formInline.date" type="daterange" range-separator="至" start-placeholder="开始日期" end-placeholder="结束日期" />
          </el-form-item>
          <el-form-item label="状态:" prop="formInline.status">
            <el-select v-model="formInline.status" clearable placeholder="请选择" style="width:160px;">
              <el-option label="暂停" value="0" />
              <el-option label="开始" value="1" />
            </el-select>
          </el-form-item>
          <el-form-item label="数据来源:" prop="formInline.source">
            <el-select v-model="formInline.source" placeholder="请选择" clearable>
              <el-option label="来源1" value="0" />
              <el-option label="来源2" value="1" />
            </el-select>
          </el-form-item>
          <el-form-item label="数据表名称(拼音)：" prop="formInline.tableName">
            <el-input v-model="formInline.tableName" placeholder="搜索..." />
          </el-form-item>
          <el-form-item>
            <el-button type="primary" icon="el-icon-search" @click="handleSearch">搜索</el-button>
          </el-form-item>
        </el-form>

        <el-table :data="tableData" fit highlight-current-row style="width: 100%">

          <el-table-column prop="tableName" label="数据表名" />
          <el-table-column prop="source" label="数据来源" />
          <el-table-column prop="date" label="备份日期" />
          <el-table-column prop="count" label="备份数目" />
          <el-table-column prop="isSuccess" label="是否成功" />
          <el-table-column prop="date2" label="执行时间" />
          <el-table-column prop="detail" label="详细信息" />
        </el-table>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        cycle: [],
        status: '',
        selectDate: '',
        selectTime: '',
        week: []
      },
      formInline: {
        status: '',
        date: '',
        source: '',
        tableName: ''
      },
      activeName: 'first',
      tableData: [{
        tableName: 'AJ_T_TABLE',
        source: '数据中心',
        date: '2019-05-02',
        count: '1',
        isSuccess: '执行成功',
        date2: '2019-05-02 11：10：34',
        detail: '信息信息信息信息信息'
      }, {
        tableName: 'AJ_T_TABLE',
        source: '数据中心',
        date: '2019-05-02',
        count: '1',
        isSuccess: '执行成功',
        date2: '2019-05-02 11：10：34',
        detail: '信息信息信息信息信息'
      }, {
        tableName: 'AJ_T_TABLE',
        source: '数据中心',
        date: '2019-05-02',
        count: '1',
        isSuccess: '执行成功',
        date2: '2019-05-02 11：10：34',
        detail: '信息信息信息信息信息'
      }, {
        tableName: 'AJ_T_TABLE',
        source: '数据中心',
        date: '2019-05-02',
        count: '1',
        isSuccess: '执行成功',
        date2: '2019-05-02 11：10：34',
        detail: '信息信息信息信息信息'
      }, {
        tableName: 'AJ_T_TABLE',
        source: '数据中心',
        date: '2019-05-02',
        count: '1',
        isSuccess: '执行成功',
        date2: '2019-05-02 11：10：34',
        detail: '信息信息信息信息信息'
      }]
    }
  },
  methods: {
    onSubmit() {
      this.$message({
        message: '保存成功',
        type: 'success'
      })
    },
    manualSubmit() {
      this.$message({
        message: '手动执行成功',
        type: 'success'
      })
    },
    handleSearch() {
      this.$message({
        message: '搜索成功',
        type: 'success'
      })
    }
  }
}
</script>

<style>
</style>
