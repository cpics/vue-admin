<template>
  <div class="g-container">
    <el-row class="m-filter-row">
      <el-col class="filter-label" :span="2" align justify>类型代码：</el-col>
      <el-col class="mr-20" :span="6" align justify>
        <el-input v-model="input1" placeholder="请输入内容" />
      </el-col>
      <el-col class="filter-label" :span="2" align justify>类型名称：</el-col>
      <el-col class="mr-20" :span="6" align justify>
        <el-input v-model="input2" placeholder="请输入内容" />
      </el-col>
      <el-col :span="4" align justify>
        <el-button icon="el-icon-search" type="primary">查询</el-button>
      </el-col>
    </el-row>
    <div class="m-buttons-row">
      <el-button icon="el-icon-plus" type="primary">添加</el-button>
      <el-button icon="el-icon-edit" type="success">编辑</el-button>
      <el-button icon="el-icon-delete" type="danger">删除</el-button>
      <el-button icon="el-icon-upload">导出</el-button>
    </div>
    <el-table
      ref="multipleTable"
      :data="tableData"
      tooltip-effect="dark"
      style="width: 100%"
    >
      <el-table-column
        type="selection"
        width="55"
      />
      <el-table-column
        prop="code"
        label="类型代码"
      />
      <el-table-column
        prop="name"
        label="类型名称"
      />
    </el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [{
        code: 'ABVVSVVSDD',
        name: '休学类型'
      }, {
        code: 'ABVVSVVSDD',
        name: '休学类型'
      }, {
        code: 'ABVVSVVSDD',
        name: '休学类型'
      }, {
        code: 'ABVVSVVSDD',
        name: '休学类型'
      }, {
        code: 'ABVVSVVSDD',
        name: '休学类型'
      }, {
        code: 'ABVVSVVSDD',
        name: '休学类型'
      }]
    }
  }
}
</script>

<style>

</style>
