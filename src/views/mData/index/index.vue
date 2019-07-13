<template>
  <div class="g-container">
    <el-row>
      <el-col
        :span="4"
        align
        justify
      >
        注册系统名：
      </el-col>
      <el-col
        :span="6"
        align
        justify
      >
        <el-input
          v-model="input1"
          placeholder="请输入内容"
        />
      </el-col>
      <el-col
        :span="4"
        align
        justify
      >
        数据库连接用户名：
      </el-col>
      <el-col
        :span="6"
        align
        justify
      >
        <el-input
          v-model="input2"
          placeholder="请输入内容"
        />
      </el-col>
      <el-col
        :span="4"
        align
        justify
      >
        <el-button>查询</el-button>
      </el-col>
    </el-row>
    <div>
      <el-button>注册</el-button>
      <el-button>删除</el-button>
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
          <template slot-scope="sope">
            <el-switch
              v-model="sope.row.isUse"
              active-color="#13ce66"
              inactive-color="#ff4949"
            />
          </template>
        </el-table-column>
        <el-table-column
          label="操作"
        >
          <template>
            <el-button>测试</el-button>
            <el-button>编辑</el-button>
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
