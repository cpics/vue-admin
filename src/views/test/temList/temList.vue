<template>
  <div class="g-container">
    <div class="m-buttons-row">
      <el-button icon="el-icon-plus" type="primary" @click="showDialg(1)">添加</el-button>
      <el-button icon="el-icon-delete" type="danger" @click="del">删除</el-button>
    </div>
    <el-table ref="multipleTable" :data="tableData" style="width: 100%" @selection-change="handleSelectionChange($event)">
      <el-table-column type="selection" width="55" />
      <el-table-column prop="template" label="规则模板" />
      <el-table-column prop="type" label="规则类型" />
      <el-table-column prop="useType" label="使用类型" />
      <el-table-column label="邮件提醒">
        <template slot-scope="scope">
          <el-switch v-model="scope.row.email" active-color="#13ce66" inactive-color="#ff4949" />
        </template>
      </el-table-column>
      <el-table-column fixed="right" label="操作" width="100">
        <template>
          <el-button class="mini-btn" type="primary" icon="el-icon-edit" circle title="编辑" @click="showDialg(2)" />
        </template>
      </el-table-column>
    </el-table>
    <el-pagination background layout="prev, pager, next" :total="1000" />
    <el-dialog title="维护规则模板" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="规则类型" :label-width="formLabelWidth">
          <el-select v-model="form.region" placeholder="请选择">
            <el-option label="唯一性" value="shanghai" />
            <el-option label="完整性" value="beijing" />
            <el-option label="确定性" value="beijing" />
          </el-select>
        </el-form-item>
        <el-form-item label="使用类型" :label-width="formLabelWidth">
          <el-select v-model="form.region" placeholder="请选择">
            <el-option label="单字段" value="shanghai" />
            <el-option label="多字段" value="beijing" />
          </el-select>
        </el-form-item>
        <el-form-item label="规则模板名称" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off" />
        </el-form-item>
        <el-form-item label="模板内容" :label-width="formLabelWidth">
          <el-input v-model="form.content" type="textarea" />
        </el-form-item>
        <el-form-item label="描述" :label-width="formLabelWidth">
          <el-input v-model="form.desc" type="textarea" />
        </el-form-item>
        <el-form-item label="参数名1" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off" />
        </el-form-item>
        <el-form-item label="参数名2" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off" />
        </el-form-item>
        <el-form-item label="参数名3" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off" />
        </el-form-item>
        <el-form-item label="参数名4" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off" />
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="showDialg">取 消</el-button>
        <el-button type="primary" @click="save">保 存</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      type: 1, // 1代表添加，2代表修改
      value1: true,
      tableData: [{
        id: 0,
        template: '不在代码表',
        type: '唯一性',
        useType: '单字段',
        email: true
      }, {
        id: 1,
        template: '不在代码表',
        type: '唯一性',
        useType: '单字段',
        email: true
      }, {
        id: 2,
        template: '不在代码表',
        type: '唯一性',
        useType: '单字段',
        email: true
      }, {
        id: 3,
        template: '不在代码表',
        type: '唯一性',
        useType: '单字段',
        email: true
      }, {
        id: 4,
        template: '不在代码表',
        type: '唯一性',
        useType: '单字段',
        email: true
      }],
      multipleSelection: [],
      dialogFormVisible: false,
      form: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        content: '',
        desc: ''
      },
      formLabelWidth: '120px'
    }
  },
  methods: {
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    showDialg(type) {
      if (type) {
        this.type = type
      }
      this.dialogFormVisible = !this.dialogFormVisible
    },
    save() {
      if (this.type == 1) {
        this.tableData.push({
          id: this.tableData,
          template: '不在代码表',
          type: '唯一性',
          useType: '单字段',
          email: true
        })
      } else if (this.type == 2) {
        console.log(this.type)
      }
      this.showDialg()
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

<style scoped="scoped" lang="scss">
.tem-handle-btn {
  padding-bottom: 30px;
}
</style>
