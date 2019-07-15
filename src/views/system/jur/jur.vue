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
    <div>
      <el-table
        :data="tableData"
        style="width: 100%"
      >
        <el-table-column
          prop="code"
          label="角色代码"
        />
        <el-table-column
          prop="name"
          label="角色名称"
        />
        <el-table-column
          fixed="right"
          label="授权配置"
          width="120"
        >
          <template>
            <el-button class="mini-btn" type="primary" icon="el-icon-setting" circle title="配置" @click="dialogSetVisible = true" />
          </template>
        </el-table-column>
      </el-table>
      <el-pagination background layout="prev, pager, next" :total="1000" />
    </div>
    <el-dialog title="配置" :visible.sync="dialogSetVisible">
      <el-row class="m-filter-row">
        <el-col class="mr-20" :span="4" align justify>
          <el-button icon="el-icon-document" type="primary" @click="save">保存</el-button>
        </el-col>
        <el-col class="filter-label" :span="2" align justify>查询条件：</el-col>
        <el-col class="mr-20" :span="6" align justify>
          <el-input v-model="input2" placeholder="请输入查询条件" />
        </el-col>
        <el-col :span="4" align justify>
          <el-button icon="el-icon-search" type="primary">查询</el-button>
        </el-col>
      </el-row>
      <el-tree
        :data="data"
        show-checkbox
        node-key="id"
        :default-expanded-keys="[2, 3]"
        :default-checked-keys="[5]"
        :props="defaultProps"
      />
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input1: '',
      input2: '',
      dialogSetVisible: false,

      tableData: [{
        code: 'sysadmin',
        name: '系统管理员'
      }, {
        code: 'guide_mg',
        name: '指南管理'
      }, {
        code: 'sysadmin',
        name: '系统管理员'
      }, {
        code: 'guide_mg',
        name: '指南管理'
      }, {
        code: 'sysadmin',
        name: '系统管理员'
      }, {
        code: 'guide_mg',
        name: '指南管理'
      }],
      data: [{
        id: 1,
        label: '业务平台',
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
  methods: {
    save() {
      this.$message({
        message: '保存成功',
        type: 'success'
      })
      this.dialogSetVisible = false
    }
  }
}
</script>

<style>

</style>
