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
          <div class="tem-rule-filter" style="text-align:center">
            <h4>主数据总体情况汇总（截止2019-06-21）</h4>
          </div>
          <el-table ref="multipleTable" :data="tableData" tooltip-effect="dark" style="width: 100%" @selection-change="handleSelectionChange">
            <el-table-column prop="id" label="ID" />
            <el-table-column prop="tableCname" label="表中文名称" />
            <el-table-column prop="tableName" label="表名" />
            <el-table-column prop="count" label="数据记录数" />
            <el-table-column prop="wordCount" label="字段数" />
          </el-table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {

  data() {
    return {
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
      tableData: [{
        id: '1',
        tableCname: '学生课表数据',
        tableName: 'T_JW_XSKB',
        count: '12345',
        wordCount: '10'
      },
      {
        id: '2',
        tableCname: '学生课表数据',
        tableName: 'T_JW_XSKB',
        count: '12345',
        wordCount: '10'
      },
      {
        id: '3',
        tableCname: '学生课表数据',
        tableName: 'T_JW_XSKB',
        count: '12345',
        wordCount: '10'
      },
      {
        id: '4',
        tableCname: '学生课表数据',
        tableName: 'T_JW_XSKB',
        count: '12345',
        wordCount: '10'
      },
      {
        id: '5',
        tableCname: '学生课表数据',
        tableName: 'T_JW_XSKB',
        count: '12345',
        wordCount: '10'
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
