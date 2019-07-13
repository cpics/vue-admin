<template>
  <div>
    <el-tabs v-model="activeName" type="card">
      <el-tab-pane label="定时配置" name="first">
        <el-form ref="form" label-width="100px">
          <el-form-item label="周期：">
            <el-col :span="12">
              <el-checkbox-group v-model="form.cycle">
                <el-checkbox label="每天" />
                <el-checkbox label="每周" />
                <el-checkbox label="每月" />
                <el-checkbox label="每年" />
              </el-checkbox-group>
            </el-col>
          </el-form-item>
          <el-form-item label="状态：">
            <el-col :span="4">
              <el-select v-model="form.status" placeholder="请选择状态" clearable>
                <el-option label="暂停" value="0" />
                <el-option label="开始" value="1" />
              </el-select>
            </el-col>
          </el-form-item>
          <el-form-item label="日期：">
            <el-col :span="4">
              <el-date-picker v-model="form.selectDate" type="date" placeholder="选择日期" style="width: 100%;" />
            </el-col>
          </el-form-item>
          <el-form-item label="星期：">
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
          <el-form-item label="时间：">
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
      <el-tab-pane label="任务日志" name="second">任务日志</el-tab-pane>
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
      activeName: 'first'
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
    }
  }
}
</script>

<style>
</style>
