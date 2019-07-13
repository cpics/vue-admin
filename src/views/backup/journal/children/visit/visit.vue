<template>
  <div class="app-container">
    <el-form ref="formInline" v-model="formInline" :inline="true">
      <el-form-item label="日期:" prop="formInline.date">
        <el-date-picker v-model="formInline.date" type="daterange" range-separator="至" start-placeholder="开始日期" end-placeholder="结束日期" />
      </el-form-item>
      <el-form-item>
        <el-button type="primary" icon="el-icon-search" @click="handleSearch">查询</el-button>
      </el-form-item>
    </el-form>

    <el-tabs v-model="activeName" type="card">
      <el-tab-pane label="模块访问统计" name="first">
        1
      </el-tab-pane>
      <el-tab-pane label="平台访问日志" name="second">
        2
      </el-tab-pane>
      <el-tab-pane label="平台操作日志" name="third">
        3
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeName: 'first',
      formInline: {
        date: ''
      }
    }
  },
  methods: {
    handleSearch() {
      this.$message({
        message: '查询成功',
        type: 'success'
      })
    }
  }
}
</script>

<style>
</style>
