<template>
  <div class="g-container">
    <div class="tem-handle-btn">
      <el-button type="primary">添加</el-button>
      <el-button type="danger">删除</el-button>
    </div>
    <el-table
      ref="multipleTable"
      :data="tableData"
      style="width: 100%"
    >
      <el-table-column
        type="selection"
        width="55"
      />
      <el-table-column
        prop="template"
        label="规则模板"
      />
      <el-table-column
        prop="type"
        label="规则类型"
      />
      <el-table-column
        prop="useType"
        label="使用类型"
      />
      <el-table-column
        prop="email"
        label="邮件提醒"
      >
        <template>
          <el-switch
            v-model="value1"
            active-color="#13ce66"
            inactive-color="#ff4949"
            active-text="YES"
            inactive-text="NO"
          />
        </template>
      </el-table-column>
      <el-table-column
        fixed="right"
        label="操作"
        width="100"
      >
        <template>
          <el-button type="text" size="small" @click="dialogFormVisible = true">编辑</el-button>
        </template>
      </el-table-column>
    </el-table>
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
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">保 存</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value1: true,
      tableData: [{
        template: '不在代码表',
        type: '唯一性',
        useType: '单字段'
      }, {
        template: '不在代码表',
        type: '唯一性',
        useType: '单字段'
      }, {
        template: '不在代码表',
        type: '唯一性',
        useType: '单字段'
      }, {
        template: '不在代码表',
        type: '唯一性',
        useType: '单字段'
      }, {
        template: '不在代码表',
        type: '唯一性',
        useType: '单字段'
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
  }
}
</script>

<style scoped="scoped" lang="scss">
.tem-handle-btn{
  padding-bottom: 30px;
}
</style>
