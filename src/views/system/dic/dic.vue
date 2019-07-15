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
      <el-button icon="el-icon-plus" type="primary" @click="showDialog(1)">添加</el-button>
      <el-button icon="el-icon-edit" type="success" @click="showDialog(2)">编辑</el-button>
      <el-button icon="el-icon-delete" type="danger" @click="del">删除</el-button>
      <el-button icon="el-icon-upload" @click="daochu">导出</el-button>
    </div>
    <div>
      <el-table
        ref="multipleTable"
        :data="tableData"
        tooltip-effect="dark"
        style="width: 100%"
        @selection-change="handleSelectionChange"
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
      <el-pagination background layout="prev, pager, next" :total="1000" />
    </div>
    <el-dialog :title="`${type == 1?'添加':'修改'}业务字典项`" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="类型代码" :label-width="formLabelWidth">
          <el-input v-model="form.code" autocomplete="off" />
        </el-form-item>
        <el-form-item label="类型名称" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off" />
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="showDialog">取 消</el-button>
        <el-button type="primary" @click="save">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      multipleSelection: [],
      input1: '',
      input2: '',
      type: 1, // 1是添加 2是修改
      dialogFormVisible: false,
      formLabelWidth: '120px',
      form: {
        name: '',
        code: ''
      },
      tableData: [{
        id: 0,
        code: 'ABVVSVVSDD',
        name: '休学类型'
      }, {
        id: 1,
        code: 'ABVVSVVSDD',
        name: '休学类型'
      }, {
        id: 3,
        code: 'ABVVSVVSDD',
        name: '休学类型'
      }, {
        id: 4,
        code: 'ABVVSVVSDD',
        name: '休学类型'
      }, {
        id: 5,
        code: 'ABVVSVVSDD',
        name: '休学类型'
      }, {
        id: 6,
        code: 'ABVVSVVSDD',
        name: '休学类型'
      }]
    }
  },
  methods: {
    daochu() {
      this.$message({
        message: '导出成功',
        type: 'success'
      })
    },
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    showDialog(type) {
      if (type) {
        this.type = type
      }
      this.dialogFormVisible = !this.dialogFormVisible
    },
    del() {
      if (this.multipleSelection.length == 0) {
        this.$message({
          message: '请勾选你需要删除的数据',
          type: 'warning'
        })
      } else {
        console.log(1)
        this.multipleSelection.forEach(item => {
          this.tableData.forEach((d, i) => {
            if (item.id == d.id) {
              this.tableData.splice(i, 1)
            }
          })
        })
      }
    },
    save() {
      if (this.type == 1) {
        this.tableData.push({
          id: this.tableData.length,
          code: 'ABVVSVVSDD',
          name: '休学类型'
        })
      } else if (this.type == 2) {
        this.$message({
          message: '修改成功',
          type: 'success'
        })
      }
      this.showDialog()
    }
  }
}
</script>

<style>

</style>
