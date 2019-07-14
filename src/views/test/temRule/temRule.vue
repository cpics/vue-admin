<template>
  <div class="g-container">
    <div class="double-columns tem-rule-main">
      <div class="column-left">
        <div class="border-box tem-rule-tree">
          <el-input
            v-model="filterText"
            placeholder="数据目录"
          />
          <el-tree
            ref="tree"
            class="filter-tree"
            :data="data"
            :props="defaultProps"
            default-expand-all
            :filter-node-method="filterNode"
          />
        </div>
      </div>
      <div class="column-right">
        <div class="border-box">
          <div class="tem-rule-filter">
            <el-form :model="form">
              <el-form-item
                label="规则模板"
                :label-width="formLabelWidth"
              >
                <el-select
                  v-model="form.template"
                  placeholder="请选择"
                >
                  <el-option
                    label="不符合身份证号规则"
                    value="shanghai"
                  />
                  <el-option
                    label="不唯一"
                    value="beijing"
                  />
                </el-select>
              </el-form-item>
            </el-form>
            <div class="tem-button">
              <el-button type="primary">查询</el-button>
              <el-button
                type="success"
                @click="showDia(1)"
              >添加</el-button>
              <el-button
                type="danger"
                @click="del"
              >删除</el-button>
            </div>
          </div>
          <el-table
            ref="multipleTable"
            :data="tableData"
            tooltip-effect="dark"
            style="width: 100%"
            @selection-change="wFilterTableData"
          >
            <el-table-column
              type="selection"
              width="55"
            />
            <el-table-column
              prop="object"
              label="检测对象"
            />
            <el-table-column
              prop="field"
              label="检测字段"
            />
            <el-table-column
              prop="rule"
              label="检测规则"
            />
            <el-table-column
              fixed="right"
              label="操作"
              width="200"
            >
              <template>
                <el-button
                  type="text"
                  size="small"
                  @click="showDia(2)"
                >修改</el-button>
                <el-button
                  type="text"
                  size="small"
                  @click="tiaoshi"
                >调试</el-button>
                <el-button
                  type="text"
                  size="small"
                >显示设置</el-button>
              </template>
            </el-table-column>
          </el-table>
        </div>
      </div>
    </div>
    <el-dialog
      title="编辑T_JZG检测规则"
      :visible.sync="dialogFormVisible"
    >
      <el-form :model="form">
        <el-form-item
          label="规则模板"
          :label-width="formLabelWidth"
        >
          <el-select
            v-model="form.region"
            placeholder="请选择"
          >
            <el-option
              label="不符合身份证号规则"
              value="shanghai"
            />
            <el-option
              label="不唯一"
              value="beijing"
            />
          </el-select>
        </el-form-item>
        <el-form-item
          label="检测数据范围"
          :label-width="formLabelWidth"
        >
          <el-input
            v-model="form.content"
            type="textarea"
          />
        </el-form-item>
      </el-form>
      <div class="dialog-footer form-button">
        <el-button
          type="primary"
          @click="save"
        >保 存</el-button>
      </div>
      <el-table
        ref="multipleTable"
        :data="tableData"
        height="300"
        style="width: 100%"
        @selection-change="handleSelectionChange"
      >
        <el-table-column
          type="selection"
          width="55"
        />
        <el-table-column
          prop="object"
          label="检测字段名"
        />
        <el-table-column
          prop="field"
          label="检测字段中文名"
        />
        <el-table-column
          prop="rule"
          label="说明"
        />
      </el-table>
    </el-dialog>
  </div>
</template>

<script>
export default {

  data() {
    return {
      type: 1, // 1代表添加，2代表修改
      multipleSelection: [],
      popSelection: [],
      filterText: '',
      form: {
        template: '',
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
      formLabelWidth: '120px',
      tableData: [{
        id: 0,
        object: 'T_JZG[教职工基本信息]',
        field: 'ZGH[职工号]',
        rule: '不唯一'
      }, {
        id: 1,
        object: 'T_JZG[教职工基本信息]',
        field: 'ZGH[身份证号]',
        rule: '不符合身份证号规则'
      }, {
        id: 2,
        object: 'T_JZG[教职工基本信息]',
        field: 'ZGH[职工号]',
        rule: '不唯一'
      }, {
        id: 3,
        object: 'T_JZG[教职工基本信息]',
        field: 'ZGH[职工号]',
        rule: '不唯一'
      }, {
        id: 4,
        object: 'T_JZG[教职工基本信息]',
        field: 'ZGH[身份证号]',
        rule: '不符合身份证号规则'
      }, {
        id: 5,
        object: 'T_JZG[教职工基本信息]',
        field: 'ZGH[身份证号]',
        rule: '不符合身份证号规则'
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
    showDia(type) {
      if (type) {
        this.type = type
      }
      this.dialogFormVisible = !this.dialogFormVisible
    },
    filterNode(value, data) {
      if (!value) return true
      return data.label.indexOf(value) !== -1
    },
    tiaoshi() {
      this.$confirm('是否启用调试', '提示', {
        confirmButtonText: '确定',
        cancelButtonText: '取消',
        type: 'warning',
        center: true
      }).then(() => {
        this.$message({
          type: 'success',
          message: '开启调试!'
        })
      })
    },
    save() {
      if (this.type == 1) {
        this.tableData.push({
          id: this.tableData.length,
          object: 'T_JZG[教职工基本信息]',
          field: 'ZGH[身份证号]',
          rule: '不符合身份证号规则'
        })
      } else if (this.type == 2) {

      }
      this.showDia()
    },
    wFilterTableData(val) {
      this.multipleSelection = val
    },
    handleSelectionChange(val) {
      this.popSelection = val
    },
    del() {
      if (this.multipleSelection.length == 0) {
        this.$message({
          message: '请勾选你需要删除的数据',
          type: 'warning'
        })
      } else {
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
.tem-rule-main {
    .tem-rule-tree {
        .el-input {
            margin-bottom: 10px;
        }
    }
}
</style>
