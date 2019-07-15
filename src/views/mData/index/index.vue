<template>
  <div class="g-container">
    <el-row class="m-filter-row">
      <el-col class="filter-label" :span="2" align justify>注册系统名：</el-col>
      <el-col class="mr-20" :span="6" align justify>
        <el-input v-model="input1" placeholder="请输入内容" />
      </el-col>
      <el-col class="filter-label w-140" :span="4" align justify>数据库连接用户名：</el-col>
      <el-col class="mr-20" :span="6" align justify>
        <el-input v-model="input2" placeholder="请输入内容" />
      </el-col>
      <el-col :span="4" align justify>
        <el-button icon="el-icon-search" type="primary">查询</el-button>
      </el-col>
    </el-row>
    <div class="m-buttons-row">
      <el-button icon="el-icon-circle-plus-outline" type="primary" @click="showDialog(1)">注册</el-button>
      <el-button icon="el-icon-delete" type="danger" @click="del">删除</el-button>
    </div>
    <div>
      <el-table ref="multipleTable" :data="tableData" tooltip-effect="dark" style="width: 100%" @selection-change="handleSelectionChange">
        <el-table-column type="selection" width="55" />
        <el-table-column prop="index" label="索引" width="60" />
        <el-table-column prop="xtName" label="注册系统名" />
        <el-table-column prop="type" label="数据库类型" />
        <el-table-column prop="xtString" label="数据库连接字符串" />
        <el-table-column prop="sqlName" label="数据库连接用户名" />
        <el-table-column prop="lastEditTime" label="最后修改时间" />
        <el-table-column label="是否启用">
          <template slot-scope="scope">
            <el-switch v-model="scope.row.isUse" active-color="#13ce66" inactive-color="#ff4949">
              />
            </el-switch>
          </template>
        </el-table-column>
        <el-table-column fixed="right" label="操作" width="120">
          <template>
            <el-button class="mini-btn" type="success" icon="el-icon-time" circle title="测试" />
            <el-button class="mini-btn" type="primary" icon="el-icon-edit" circle title="编辑" @click="showDialog(2)" />
          </template>
        </el-table-column>
      </el-table>
      <el-pagination background layout="prev, pager, next" :total="1000" />
    </div>
    <el-dialog title="修改数据源" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="注册系统名" :label-width="formLabelWidth">
          <el-input v-model="form.sysName" autocomplete="off" />
        </el-form-item>
        <el-form-item label="注册系统英文名" :label-width="formLabelWidth">
          <el-input v-model="form.sysEnglish" autocomplete="off" />
        </el-form-item>
        <el-form-item label="ODI数据源名称" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off" />
        </el-form-item>
        <el-form-item label="数据库类型" :label-width="formLabelWidth">
          <el-select v-model="form.region" placeholder="请选择" class="w-full">
            <el-option label="Oracle" value="1" />
            <el-option label="Mysql" value="2" />
            <el-option label="postgreSql" value="3" />
            <el-option label="SQL Server" value="4" />
          </el-select>
        </el-form-item>
        <el-form-item label="数据库驱动" :label-width="formLabelWidth">
          <el-input v-model="form.database" autocomplete="off" />
        </el-form-item>
        <el-form-item label="数据库连接字符串" :label-width="formLabelWidth">
          <el-input v-model="form.connect" autocomplete="off" />
        </el-form-item>
        <el-form-item label="数据库连接用户名" :label-width="formLabelWidth">
          <el-input v-model="form.connectName" autocomplete="off" />
        </el-form-item>
        <el-form-item label="数据库连接用户密码" :label-width="formLabelWidth">
          <el-input v-model="form.pwd" autocomplete="off" />
        </el-form-item>
        <el-form-item label="数据库对象所有者" :label-width="formLabelWidth">
          <el-input v-model="form.own" autocomplete="off" />
        </el-form-item>
        <el-form-item label="最后修改时间" :label-width="formLabelWidth">
          <el-input v-model="form.time" autocomplete="off" />
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
      type: 1, // 1添加，2修改
      input1: '',
      input2: '',
      isUse: true,
      dialogFormVisible: false,
      form: {
        sysName: '',
        sysEnglish: '',
        name: '',
        database: '',
        delivery: false,
        type: [],
        connect: '',
        connectName: '',
        pwd: '',
        own: '',
        time: ''
      },
      formLabelWidth: '140px',
      tableData: [
        {
          id: 0,
          index: 1,
          xtName: '主数据系统',
          type: 'ORacle',
          xtString: 'jdbc:oracle:thin:@192.168.XXX.XXX:XXXX:zsjpt',
          sqlName: 'usr_zsj',
          lastEditTime: '2018-04-02 11:00:05',
          isUse: true
        },
        {
          id: 1,
          index: 1,
          xtName: '主数据系统',
          type: 'ORacle',
          xtString: 'jdbc:oracle:thin:@192.168.XXX.XXX:XXXX:zsjpt',
          sqlName: 'usr_zsj',
          lastEditTime: '2018-04-02 11:00:05',
          isUse: true
        },
        {
          id: 2,
          index: 1,
          xtName: '主数据系统',
          type: 'ORacle',
          xtString: 'jdbc:oracle:thin:@192.168.XXX.XXX:XXXX:zsjpt',
          sqlName: 'usr_zsj',
          lastEditTime: '2018-04-02 11:00:05',
          isUse: true
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
          index: 1,
          xtName: '主数据系统',
          type: 'ORacle',
          xtString: 'jdbc:oracle:thin:@192.168.XXX.XXX:XXXX:zsjpt',
          sqlName: 'usr_zsj',
          lastEditTime: '2018-04-02 11:00:05',
          isUse: true
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
