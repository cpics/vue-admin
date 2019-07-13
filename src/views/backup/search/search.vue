<template>
  <div class="app-container">
    <el-form ref="formInline" v-model="formInline" :inline="true">
      <el-form-item>
        <el-button type="primary">表格</el-button>
        <el-button type="primary" icon="el-icon-search" @click="handleGo">执行</el-button>
        <el-button type="primary" @click="handleSave">保存</el-button>
      </el-form-item>
    </el-form>
    <el-form ref="form" v-model="form">
      <el-form-item prop="form.content">
        <el-input v-model="form.content" type="textarea" :rows="10" />
      </el-form-item>
    </el-form>

    <h4>查询结果</h4>
    <el-table :data="searchData" fit highlight-current-row style="width: 100%">
      <div v-if="searchData.length > 0">
        <el-table-column prop="wid" label="WID" />
        <el-table-column prop="wname" label="WNAME" />
        <el-table-column prop="wdate" label="WDATE" />
        <el-table-column prop="wip" label="WIP" />
        <el-table-column prop="wurl" label="WURL" />
      </div>
    </el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      form: {
        content: ''
      },
      formInline: {

      },
      searchData: []
    }
  },
  methods: {
    handleSave() {
      this.$message({
        message: '保存成功',
        type: 'success'
      })
    },
    handleGo() {
      this.searchData = [{
        wid: '1001',
        wname: '小王',
        wdate: '2019-07-09 10:43:20',
        wip: '192.168.1.1',
        wurl: '/mdc/history/tableData'
      }, {
        wid: '1001',
        wname: '小王',
        wdate: '2019-07-09 10:43:20',
        wip: '192.168.1.1',
        wurl: '/mdc/history/tableData'
      },
      {
        wid: '1001',
        wname: '小王',
        wdate: '2019-07-09 10:43:20',
        wip: '192.168.1.1',
        wurl: '/mdc/history/tableData'
      },
      {
        wid: '1001',
        wname: '小王',
        wdate: '2019-07-09 10:43:20',
        wip: '192.168.1.1',
        wurl: '/mdc/history/tableData'
      },
      {
        wid: '1001',
        wname: '小王',
        wdate: '2019-07-09 10:43:20',
        wip: '192.168.1.1',
        wurl: '/mdc/history/tableData'
      }
      ]
    }
  }
}
</script>

<style>
</style>
