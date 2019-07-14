<template>
  <div class="g-container">
    <div class="double-columns">
      <div class="column-left">
        <div class="border-box">
          <el-input
            v-model="filterText"
            placeholder="按表名查询"
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
          <el-row class="m-filter-row">
            <el-col class="filter-label" :span="2" align justify>查询类型：</el-col>
            <el-col class="mr-20" :span="6" align justify>
              <el-select v-model="region" placeholder="请选择" class="w-full">
                <el-option label="表" value="1" />
                <el-option label="视图" value="2" />
                <el-option label="模糊查询(表视图或者字段)" value="3" />
              </el-select>
            </el-col>
            <el-col class="filter-label" :span="2" align justify>名称：</el-col>
            <el-col class="mr-20" :span="6" align justify>
              <el-input v-model="input2" placeholder="请输入内容" />
            </el-col>
            <el-col :span="4" align justify>
              <el-button icon="el-icon-search" type="primary">查询</el-button>
            </el-col>
          </el-row>
          <div class="m-buttons-row">
            <el-button icon="el-icon-plus" type="primary">新增数据对象</el-button>
            <el-button icon="el-icon-delete" type="danger">删除</el-button>
            <el-button icon="el-icon-refresh" type="warning" @click="dialogSetVisible = true">变更数据分类</el-button>
            <el-button icon="el-icon-upload" type="success">导入</el-button>
            <el-button icon="el-icon-download" type="info">导出</el-button>
            <el-button icon="el-icon-check">数据表实体检查</el-button>
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
              prop="user"
              label="数据对象名"
              width="130"
            />
            <el-table-column
              prop="name"
              label="数据对象中文名"
            />
            <el-table-column
              prop="category"
              label="数据对象分类"
            />
            <el-table-column
              prop="lastEditTime"
              label="最后修改时间"
            />
            <el-table-column
              label="是否启用"
              width="150"
            >
              <template>
                <el-switch
                  v-model="isUse"
                  style="display: block"
                  active-color="#13ce66"
                  inactive-color="#ff4949"
                  active-text="YES"
                  inactive-text="NO"
                />
              </template>
            </el-table-column>
            <el-table-column
              fixed="right"
              label="操作"
              width="130"
            >
              <template>
                <el-button class="mini-btn" type="primary" icon="el-icon-edit" circle title="编辑" @click="dialogFormVisible = true" />
                <el-button class="mini-btn" type="success" icon="el-icon-view" circle title="预览" />
                <el-button class="mini-btn" type="warning" icon="el-icon-success" circle title="生成" />
              </template>
            </el-table-column>
          </el-table>
        </div>
      </div>
    </div>
    <el-dialog title="变更数据分类" :visible.sync="dialogSetVisible">
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
      dialogSetVisible: false,
      filterText: '',
      input1: '',
      input2: '',
      isUse: true,
      data: [
        {
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
        },
        {
          id: 2,
          label: '一级 2',
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
          label: '一级 3',
          children: [{
            id: 7,
            label: '二级 3-1'
          }, {
            id: 8,
            label: '二级 3-2'
          }]
        }
      ],
      tableData: [
        {
          user: 'T_JZG',
          name: '教职工基本信息',
          category: '人员基础信息/教职工基础信息',
          lastEditTime: '2012-11-13'
        },
        {
          user: 'T_JZG',
          name: '教职工基本信息',
          category: '人员基础信息/教职工基础信息',
          lastEditTime: '2012-11-13'
        },
        {
          user: 'T_JZG',
          name: '教职工基本信息',
          category: '人员基础信息/教职工基础信息',
          lastEditTime: '2012-11-13'
        }
      ]
    }
  }
}
</script>

<style>
</style>
