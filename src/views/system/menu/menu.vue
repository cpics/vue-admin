<template>
  <div class="g-container">
    <div class="double-columns">
      <div class="column-left">
        <div class="border-box">
          <div class="common-title">菜单管理</div>
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
          <div class="m-buttons-row">
            <el-button icon="el-icon-plus" type="primary" @click="showDialog(1)">添加</el-button>
            <!-- <el-button icon="el-icon-plus" type="waring">添加子类型</el-button> -->
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
                prop="caidan"
                label="菜单代码"
              />
              <el-table-column
                prop="name"
                label="菜单名称"
              />
              <el-table-column
                prop="show"
                label="菜单显示名称"
              />
              <el-table-column
                prop="is"
                label="是否叶子菜单"
              />
              <el-table-column
                prop="level"
                label="菜单层次"
              />
            </el-table>
            <el-pagination background layout="prev, pager, next" :total="1000" />
          </div>
        </div>
      </div>
    </div>
    <el-dialog :title="`${type == 1?'添加':'修改'}角色`" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="菜单代码" :label-width="formLabelWidth">
          <el-input v-model="form.code" autocomplete="off" />
        </el-form-item>
        <el-form-item label="菜单名称" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off" />
        </el-form-item>
        <el-form-item label="菜单显示名称" :label-width="formLabelWidth">
          <el-input v-model="form.disc" autocomplete="off" />
        </el-form-item>
        <el-form-item label="是否子菜单" :label-width="formLabelWidth">
          <el-input v-model="form.isnext" autocomplete="off" />
        </el-form-item>
        <el-form-item label="菜单层次" :label-width="formLabelWidth">
          <el-input v-model="form.level" autocomplete="off" />
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
      formLabelWidth: '120px',
      form: {
        cddm: '',
        cdname: '',
        cddisc: '',
        isnext: '',
        level: ''
      },
      type: 1, // 1添加，2修改
      data: [
        {
          id: 1,
          label: '应用菜单树',
          children: [{
            id: 4,
            label: '个人中心',
            children: [{
              id: 9,
              label: '三级 1-1-1'
            }, {
              id: 10,
              label: '三级 1-1-2'
            }]
          }]
        },
        {
          id: 2,
          label: '服务中心',
          children: [{
            id: 5,
            label: '二级 2-1'
          }, {
            id: 6,
            label: '二级 2-2'
          }]
        },
        {
          id: 3,
          label: '系统菜单',
          children: [{
            id: 7,
            label: '二级 3-1'
          }, {
            id: 8,
            label: '二级 3-2'
          }]
        }
      ],
      defaultProps: {
        children: 'children',
        label: 'label'
      },
      tableData: [
        {
          id: 0,
          caidan: 'system_menu',
          name: '系统菜单',
          show: '系统菜单',
          is: '否',
          level: '1'
        },
        {
          id: 2,
          caidan: 'system_menu',
          name: '系统菜单',
          show: '系统菜单',
          is: '否',
          level: '1'
        },
        {
          id: 3,
          caidan: 'system_menu',
          name: '系统菜单',
          show: '系统菜单',
          is: '否',
          level: '1'
        }
      ]
    }
  },
  methods: {
    handleSelectionChange(val) {
      this.multipleSelection = val
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
          caidan: 'system_menu',
          name: '系统菜单',
          show: '系统菜单',
          is: '否',
          level: '1'
        })
      } else if (this.type == 2) {
        this.$message({
          message: '修改成功',
          type: 'success'
        })
      }
      this.showDialog()
    },
    showDialog(type) {
      if (type) {
        this.type = type
      }
      this.dialogFormVisible = !this.dialogFormVisible
    },
    filterNode(value, data) {
      if (!value) return true
      return data.label.indexOf(value) !== -1
    }
  }
}
</script>

<style>

</style>
