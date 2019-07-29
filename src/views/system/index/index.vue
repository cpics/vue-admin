<template>
  <div class="g-container">
    <el-row class="m-filter-row">
      <el-col class="filter-label" :span="2" align justify>角色代码：</el-col>
      <el-col class="mr-20" :span="6" align justify>
        <el-input v-model="input1" placeholder="请输入内容" />
      </el-col>
      <el-col class="filter-label" :span="2" align justify>角色名称：</el-col>
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
          prop="jsdm"
          label="角色代码"
        />
        <el-table-column
          prop="name"
          label="角色名称"
        />
        <el-table-column
          prop="miaoshu"
          label="角色描述"
        />
      </el-table>
      <el-pagination background layout="prev, pager, next" :total="1000" />
    </div>
    <el-dialog :title="`${type == 1?'添加':'修改'}角色`" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="角色代码" :label-width="formLabelWidth">
          <el-input v-model="form.code" autocomplete="off" />
        </el-form-item>
        <el-form-item label="角色名称" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off" />
        </el-form-item>
        <el-form-item label="角色描述" :label-width="formLabelWidth">
          <el-input v-model="form.disc" autocomplete="off" />
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
      dialogFormVisible: false,
      type: '1',
      input1: '',
      input2: '',
      formLabelWidth: '120px',
      form: {
        name: '',
        code: '',
        disc: ''
      },
      tableData: [
        {
          id: 0,
          jsdm: 'sysadmin',
          name: '系统管理员',
          miaoshu: '系统管理员'
        },
        {
          id: 2,
          jsdm: 'teacher',
          name: '教职工',
          miaoshu: '教职工'
        },
        {
          id: 3,
          jsdm: 'develop',
          name: '开发者',
          miaoshu: '开发者'
        },
        {
          id: 4,
          jsdm: 'test',
          name: '测试',
          miaoshu: '测试'
        }
      ]
    }
  },
  methods: {
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    showDialog(type) {
      if (type) {
        this.type = type
      }
      this.dialogFormVisible = !this.dialogFormVisible
    },
    save() {
      if (this.type == 1) {
        this.tableData.push({
          id: this.tableData.length,
          jsdm: 'system',
          name: '系统管理员',
          miaoshu: '角色描述'
        })
      } else if (this.type == 2) {
        this.$message({
          message: '修改成功',
          type: 'success'
        })
      }
      this.showDialog()
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
    }
  }
}
</script>

<style>

</style>
