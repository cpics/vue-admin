<template>
  <div class="g-container">
    <el-row class="m-filter-row">
      <el-col class="mr-20" :span="4" align justify>
        <el-select
          v-model="value"
          placeholder="请选择"
        >
          <el-option
            v-for="item in options"
            :key="item.value"
            :label="item.label"
            :value="item.value"
          />
        </el-select>
      </el-col>
      <el-col class="mr-20" :span="6" align justify>
        <el-input v-model="input" placeholder="请输入内容" />
      </el-col>
      <el-col :span="4" align justify>
        <el-button icon="el-icon-search" type="primary">查询</el-button>
      </el-col>
    </el-row>
    <el-row>
      <el-table
        ref="multipleTable"
        :data="tableData"
        tooltip-effect="dark"
        style="width: 100%"
      >
        <el-table-column
          prop="state"
          label="状态"
          min-width="20%"
        />
        <el-table-column
          prop="name"
          label="服务名称"
          min-width="35%"
        />
        <el-table-column
          prop="miaoshu"
          label="服务描述"
          min-width="45%"
        />
        <el-table-column
          fixed="right"
          label="操作"
          width="150"
        >
          <template>
            <el-button type="text" @click="dialogImpowerVisible = true">授权</el-button>
            <el-button type="text" @click="dialogServiceVisible = true">服务说明</el-button>
          </template>
        </el-table-column>

      </el-table>
    </el-row>
    <el-row>
      <el-pagination
        background
        layout="sizes, prev, pager, next"
        :page-sizes="[10,15,30,50,100]"
        :total="1000"
      />
    </el-row>
    <el-dialog title="server1服务授权" :visible.sync="dialogImpowerVisible">
      <el-row class="m-filter-row">
        <el-col class="mr-20" :span="6" align justify>
          <el-select v-model="region" placeholder="业务区域选择">
            <el-option label="人事" value="1" />
            <el-option label="科研" value="2" />
            <el-option label="学工" value="3" />
            <el-option label="教务" value="4" />
            <el-option label="财务" value="5" />
            <el-option label="一卡通" value="6" />
            <el-option label="图书" value="7" />
            <el-option label="OA" value="8" />
            <el-option label="后勤" value="9" />
            <el-option label="外事" value="10" />
          </el-select>
        </el-col>
        <el-col :span="15" align justify>
          <el-button icon="el-icon-plus" type="success">添加</el-button>
          <el-button icon="el-icon-minus" type="danger">删除</el-button>
          <el-button icon="el-icon-document" type="primary">保存</el-button>
        </el-col>
      </el-row>
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
          prop="id"
          label="申请ID"
          width="100"
        />
        <el-table-column
          prop="token"
          label="申请TOKEN"
        />
        <el-table-column
          prop="ip"
          label="白名单IP"
        />
      </el-table>
    </el-dialog>
    <el-dialog title="服务说明" :visible.sync="dialogServiceVisible">
      <div class="explain-row">
        <div class="common-title-small">server1服务API</div>
        <div class="explain-box">
          服务编号(int_num)：364565761af094f7fa15ab91e68fdde59  (applyId、accessToken见授权)<br>
          服务名称：server<br>
          服务描述：教职工基础信息共享服务<br>
          服务URL(SOAP)：http://192.168.1.101:80/ars/ws/data?wsdl<br>
          服务URL(REST)：http://192.168.1.101:80/getDataInfo<br>
          文本数据接口地址：http://192.168.1.101:80/ars/file/down
        </div>
      </div>
      <div class="explain-row">
        <div class="common-title-small">服务参数：</div>
        <div class="explain-box">
          {
          "paramString":{
          "ZGH":"xxx"
          },
          "pagesize":10,
          "page":1
          }
        </div>
      </div>
      <div class="explain-row">
        <div class="common-title-small">返回格式：</div>
        <div class="explain-box">
          {
          "msg":"successful",
          "total":100,
          "data":[
          {
          "XM":"... ...",
          "ZGH":"... ..."
          }
          ],
          "pagesize":10,
          "page":1,
          "status":"200"
          }
        </div>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      dialogImpowerVisible: false,
      dialogServiceVisible: false,
      input: '',
      options: [{
        value: '1',
        label: '自定义服务'
      }, {
        value: '2',
        label: '预加载服务'
      }],
      value: '',
      tableData: [{
        state: '未启用',
        source: '真实数据',
        name: 'ryxx',
        miaoshu: '',
        id: '1',
        token: 'qwxrfwwefzdesaxasee',
        ip: '192.165.21.33/32'
      }, {
        state: '未启用',
        source: '真实数据',
        name: 'ueho',
        miaoshu: '',
        id: '2',
        token: 'arexareegeaetrddssa',
        ip: '192.165.21.33/32'
      }, {
        state: '已启用',
        source: '真实数据',
        name: '人员基本信息',
        miaoshu: '人员基本信息',
        id: '3',
        token: 'asdxxsweaawwddgaerr',
        ip: '192.165.21.33/32'
      }, {
        state: '已启用',
        source: '脱敏数据',
        name: '助学金发放流水信息',
        miaoshu: '助学金发放流水信息',
        id: '4',
        token: 'pliiaeerraxerwercxge',
        ip: '192.165.21.33/32'
      }, {
        state: '未启用',
        source: '真实数据',
        name: '图书借阅信息',
        miaoshu: '图书借阅信息',
        id: '5',
        token: 'asdxxsweaawwddgaerr',
        ip: '192.165.21.33/32'
      }, {
        state: '已启用',
        source: '真实数据',
        name: '学生信息',
        miaoshu: '学生信息',
        id: '6',
        token: 'pliiaeerraxerwercxge',
        ip: '192.165.21.33/32'
      }, {
        state: '已启用',
        source: '真实数据',
        name: '教职工信息',
        miaoshu: '教职工基本信息',
        id: '7',
        token: 'asdxxsweaawwddgaerr',
        ip: '192.165.21.33/32'
      }, {
        state: '已启用',
        source: '脱敏数据',
        name: '教师通讯信息',
        miaoshu: '教师通讯信息',
        id: '8',
        token: 'pliiaeerraxerwercxge',
        ip: '192.165.21.33/32'
      }, {
        state: '未启用',
        source: '真实数据',
        name: '数据服务',
        miaoshu: '数据服务',
        id: '9',
        token: 'asdxxsweaawwddgaerr',
        ip: '192.165.21.33/32'
      }, {
        state: '已启用',
        source: '真实数据',
        name: '贫困生信息',
        miaoshu: '贫困生信息',
        id: '10',
        token: 'pliiaeerraxerwercxge',
        ip: '192.165.21.33/32'
      }]
    }
  }
}
</script>

<style>

</style>
