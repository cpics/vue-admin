<template>
  <div class="g-container">
    <div class="double-columns tem-rule-main">
      <div class="column-left">
        <div class="border-box tem-rule-tree">
          <el-input v-model="filterText" placeholder="按表名查询" />
          <el-tree ref="tree" class="filter-tree" :data="data" :props="defaultProps" default-expand-all :filter-node-method="filterNode" />
        </div>
      </div>
      <div class="column-right">
        <div class="border-box">
          <h4 class="common-h4-tit">主数据总体情况汇总（截止2019-06-21）</h4>
          <el-table ref="multipleTable" :data="tableData" tooltip-effect="dark" style="width: 100%" @selection-change="handleSelectionChange">
            <el-table-column prop="id" label="ID" />
            <el-table-column prop="tableCname" label="表中文名称" />
            <el-table-column prop="tableName" label="表名" />
            <el-table-column prop="count" label="数据记录数" />
            <el-table-column prop="wordCount" label="字段数" />
          </el-table>
        </div>
        <!--详情-->
        <div class="border-box">
          <div class="m-buttons-row">
            <el-button icon="el-icon-search" type="primary" @click="dialogSelectVisible = true">高级查询</el-button>
            <el-button icon="el-icon-delete" type="danger">删除</el-button>
            <el-button icon="el-icon-upload" type="success" @click="dialogImportVisible = true">导入</el-button>
            <el-button icon="el-icon-download" type="info">导出</el-button>
          </div>
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
              prop="id"
              label="GH工号"
            />
            <el-table-column
              prop="dwh"
              label="DWH单位号"
            />
            <el-table-column
              prop="xm"
              label="XM姓名"
            />
            <el-table-column
              prop="xbm"
              label="XBM性别码"
            />
            <el-table-column
              prop="sfzjlxm"
              label="SFZJLXM身份证件类型码"
            />
            <el-table-column
              prop="sfzjh"
              label="SFZJH身份证件号"
            />
            <el-table-column
              prop="zzmmm"
              label="ZZMMM政治面貌码"
            />
          </el-table>
        </div>
      </div>
    </div>
    <el-dialog title="高级查询" :visible.sync="dialogSelectVisible">
      <div>
        <el-row class="m-filter-row">
          <el-col class="filter-label" :span="2" align justify>选择条件：</el-col>
          <el-col class="mr-20" :span="6" align justify>
            <el-input v-model="input1" placeholder="请输入内容" />
          </el-col>
          <el-col class="filter-label w-60" :span="4" align justify>等于：</el-col>
          <el-col class="mr-20" :span="6" align justify>
            <el-select v-model="form.region" placeholder="请选择">
              <el-option label="1" value="1" />
              <el-option label="2" value="2" />
            </el-select>
          </el-col>
          <el-col class="mr-20" :span="6" align justify>
            <el-input v-model="input2" placeholder="请输入内容" />
          </el-col>
          <el-col :span="4" align justify>
            <el-button icon="el-icon-add" type="primary">添加</el-button>
          </el-col>
        </el-row>
        <el-table :data="tableData">
          <el-table-column property="id" label="序号" width="60" />
          <el-table-column property="tableCname" label="字段名称" />
          <el-table-column property="tableName" label="逻辑运算" />
          <el-table-column property="count" label="输入值" />
          <el-table-column property="wordCount" label="条件关系" />
          <el-table-column
            fixed="right"
            label="操作"
            width="80"
          >
            <template>
              <el-button class="mini-btn" type="primary" icon="el-icon-edit" circle title="XX" @click="dialogFormVisible = true" />
            </template>
          </el-table-column>
        </el-table>
      </div>
      <div slot="footer" class="dialog-footer el-dialog__footer">
        <el-button type="primary" @click="onSubmit">确定</el-button>
        <el-button>取消</el-button>
      </div>
    </el-dialog>
    <el-dialog title="导入数据对象" :visible.sync="dialogImportVisible">
      <el-form ref="form" :model="form" label-width="140px">
        <el-form-item label="本地文件">
          <el-upload
            class="upload-demo"
            action="https://jsonplaceholder.typicode.com/posts/"
            :on-change="handleChange"
            :file-list="fileList"
          >
            <el-button size="small" type="success">选择文件</el-button>
            <!--<div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>-->
          </el-upload>
        </el-form-item>
        <el-form-item label="关键字">
          <el-input autocomplete="off" />
        </el-form-item>
        <el-form-item>
          <el-button icon="el-icon-upload" type="primary">导入数据</el-button>
          <el-button icon="el-icon-download" type="info">模板下载</el-button>
        </el-form-item>
        <el-form-item label="导入日志">
          <div class="log-box">
            导入日志导入日志导入日志导入日志导入日志导入日志导入日志导入日志
          </div>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer el-dialog__footer">
        <el-button type="primary" @click="onSubmit">确定</el-button>
        <el-button>关闭</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {

  data() {
    return {
      filterText: '',
      dialogSelectVisible: false,
      dialogImportVisible: false,
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
      tableData: [{
        id: '1',
        tableCname: '学生课表数据',
        tableName: 'T_JW_XSKB',
        count: '12345',
        wordCount: '10',
        gh: '1',
        dwh: '000222',
        xm: '张三',
        xbm: '222',
        sfzjlxm: '33333333',
        sdzjh: '2222222',
        zzmmm: '1111'
      },
      {
        id: '2',
        tableCname: '学生课表数据',
        tableName: 'T_JW_XSKB',
        count: '12345',
        wordCount: '10',
        gh: '1',
        dwh: '000222',
        xm: '张三',
        xbm: '222',
        sfzjlxm: '33333333',
        sdzjh: '2222222',
        zzmmm: '1111'
      },
      {
        id: '3',
        tableCname: '学生课表数据',
        tableName: 'T_JW_XSKB',
        count: '12345',
        wordCount: '10',
        gh: '1',
        dwh: '000222',
        xm: '张三',
        xbm: '222',
        sfzjlxm: '33333333',
        sdzjh: '2222222',
        zzmmm: '1111'
      },
      {
        id: '4',
        tableCname: '学生课表数据',
        tableName: 'T_JW_XSKB',
        count: '12345',
        wordCount: '10',
        gh: '1',
        dwh: '000222',
        xm: '张三',
        xbm: '222',
        sfzjlxm: '33333333',
        sdzjh: '2222222',
        zzmmm: '1111'
      },
      {
        id: '5',
        tableCname: '学生课表数据',
        tableName: 'T_JW_XSKB',
        count: '12345',
        wordCount: '10',
        gh: '1',
        dwh: '000222',
        xm: '张三',
        xbm: '222',
        sfzjlxm: '33333333',
        sdzjh: '2222222',
        zzmmm: '1111'
      }
      ],
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
  .tem-rule-filter {
    height: 40px;
    margin-bottom: 20px;
    &:after {
      content: '';
      font-size: 0;
      display: block;
      height: 0;
      clear: both;
      visibility: hidden;
    }
    .el-form {
      float: left;
      width: 400px;
      .el-form-item {
        margin-bottom: 0;
      }
    }
    .tem-button {
      float: right;
    }
  }
}
</style>
