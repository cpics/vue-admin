<template>
  <div class="g-container">
    <div class="double-columns tem-rule-main">
      <div class="column-left">
        <div class="border-box tem-rule-tree">
          <el-input v-model="filterText" placeholder="请输入关键字" />
          <el-tree ref="tree" class="filter-tree" :data="data" :props="defaultProps" default-expand-all :filter-node-method="filterNode" />
        </div>
      </div>
      <div class="column-right">
        <div class="border-box">
          <div class="tem-rule-filter">
            <div class="tem-button">
              <el-button type="success" @click="dialogFormVisible = true">增加映射</el-button>
              <el-button type="danger">删除映射</el-button>
            </div>
          </div>
          <el-table ref="multipleTable" :data="tableData" tooltip-effect="dark" style="width: 100%" @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="55" />
            <el-table-column prop="businessTable" label="业务表" />
            <el-table-column prop="businessField" label="业务表字段" />
            <el-table-column prop="codeTable" label="标准代码表" />
            <el-table-column prop="codeFieldName" label="代码字段名称" />
            <el-table-column prop="showFieldName" label="显示字段名称" />
            <el-table-column prop="dataFlow" label="数据流向" />
            <el-table-column fixed="right" label="操作" width="200">
              <template>
                <el-button type="text" size="small" @click="dialogFormVisible = true">编辑</el-button>
              </template>
            </el-table-column>
          </el-table>
        </div>
      </div>
    </div>
    <el-dialog title="增加映射" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="业务表:" :label-width="formLabelWidth">
          <el-input v-model="form.businessTable" />
        </el-form-item>
        <el-form-item label="业务表字段:" :label-width="formLabelWidth">
          <el-input v-model="form.businessField" />
        </el-form-item>
        <el-form-item label="标准代码表:" :label-width="formLabelWidth">
          <el-input v-model="form.codeTable" />
        </el-form-item>
        <el-form-item label="代码字段名称:" :label-width="formLabelWidth">
          <el-input v-model="form.codeFieldName" />
        </el-form-item>
        <el-form-item label="显示字段名称:" :label-width="formLabelWidth">
          <el-input v-model="form.showFieldName" />
        </el-form-item>
        <el-form-item label="数据流向:" prop="form.dataFlow" :label-width="formLabelWidth">
          <el-select v-model="form.source" placeholder="请选择" clearable>
            <el-option label="主数据库到业务库" value="0" />
            <el-option label="业务库到主数据库" value="1" />
          </el-select>
        </el-form-item>
      </el-form>
      <div class="dialog-footer form-button">
        <el-button type="primary" @click="dialogFormVisible = false">确定</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">取消</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {

  data() {
    return {
      filterText: '',
      form: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        content: '',
        desc: '',
        businessTable: '',
        businessField: '',
        codeTable: '',
        codeFieldName: '',
        showFieldName: '',
        source: ''
      },
      formLabelWidth: '120px',
      tableData: [{
        businessTable: '学校基本数据子类表',
        businessField: '985GCYXZK',
        codeTable: 'SFBZ',
        codeFieldName: 'DM(代码)',
        showFieldName: 'GCYXZK',
        dataFlow: '代码表到业务表'
      },
      {
        businessTable: '学校基本数据子类表',
        businessField: '985GCYXZK',
        codeTable: 'SFBZ',
        codeFieldName: 'DM(代码)',
        showFieldName: 'GCYXZK',
        dataFlow: '代码表到业务表'
      },
      {
        businessTable: '学校基本数据子类表',
        businessField: '985GCYXZK',
        codeTable: 'SFBZ',
        codeFieldName: 'DM(代码)',
        showFieldName: 'GCYXZK',
        dataFlow: '代码表到业务表'
      },
      {
        businessTable: '学校基本数据子类表',
        businessField: '985GCYXZK',
        codeTable: 'SFBZ',
        codeFieldName: 'DM(代码)',
        showFieldName: 'GCYXZK',
        dataFlow: '代码表到业务表'
      }],
      dialogFormVisible: false,
      data: [{
        id: 1,
        label: '一级 1',
        children: [{
          id: 4,
          label: '二级 1-1',
          children: [{
            id: 9,
            label: '三级 1-1-1'
          }, {
            id: 10,
            label: '三级 1-1-2'
          }]
        }]
      }, {
        id: 2,
        label: '一级 2',
        children: [{
          id: 5,
          label: '二级 2-1'
        }, {
          id: 6,
          label: '二级 2-2'
        }]
      }, {
        id: 3,
        label: '一级 3',
        children: [{
          id: 7,
          label: '二级 3-1'
        }, {
          id: 8,
          label: '二级 3-2'
        }]
      }],
      defaultProps: {
        children: 'children',
        label: 'label'
      }
    }
  },
  watch: {
    filterText(val) {
      this.$refs.tree.filter(val)
    }
  },

  methods: {
    filterNode(value, data) {
      if (!value) return true
      return data.label.indexOf(value) !== -1
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
.tem-rule-main {
  .tem-rule-tree {
    .el-input {
      margin-bottom: 10px;
    }
  }
}
</style>
