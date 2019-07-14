<template>
  <div class="g-container">
    <el-row class="m-filter-row">
      <el-col class="filter-label" :span="2" align justify>角色代码：</el-col>
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
      <el-button icon="el-icon-circle-plus-outline" type="primary">注册</el-button>
      <el-button icon="el-icon-delete" type="danger">删除</el-button>
    </div>
    <div>
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
          prop="index"
          label="索引"
        />
        <el-table-column
          prop="xtName"
          label="注册系统名"
        />
        <el-table-column
          prop="type"
          label="数据库类型"
        />
        <el-table-column
          prop="xtString"
          label="数据库连接字符串"
        />
        <el-table-column
          prop="sqlName"
          label="数据库连接用户名"
        />
        <el-table-column
          prop="lastEditTime"
          label="最后修改时间"
        />
        <el-table-column
          label="是否启用"
        >
          <template>
            <el-switch
              v-model="isUse"
              active-color="#13ce66"
              inactive-color="#ff4949"
            >
              />
            </el-switch>
          </template>
        </el-table-column>
        <el-table-column
          fixed="right"
          label="操作"
          width="120"
        >
          <template>
            <el-button class="mini-btn" type="success" icon="el-icon-time" circle title="测试" />
            <el-button class="mini-btn" type="primary" icon="el-icon-edit" circle title="编辑" />
          </template>
        </el-table-column>
      </el-table>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input1: '',
      input2: '',
      isUse: true,
      tableData: [
        {
          index: 1,
          xtName: '主数据系统',
          type: 'ORacle',
          xtString: 'jdbc:oracle:thin:@192.168.XXX.XXX:XXXX:zsjpt',
          sqlName: 'usr_zsj',
          lastEditTime: '2018-04-02 11:00:05',
          isUse: true
        },
        {
          index: 1,
          xtName: '主数据系统',
          type: 'ORacle',
          xtString: 'jdbc:oracle:thin:@192.168.XXX.XXX:XXXX:zsjpt',
          sqlName: 'usr_zsj',
          lastEditTime: '2018-04-02 11:00:05',
          isUse: true
        },
        {
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
  }
}
</script>

<style>
</style>
