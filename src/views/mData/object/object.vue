<template>
  <div class="g-container">
    <div class="double-columns">
      <div class="column-left">
        <div class="border-box">
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
          <div>
            <el-button>新增数据对象</el-button>
            <el-button>删除</el-button>
            <el-button>变更数据分类</el-button>
            <el-button>导入</el-button>
            <el-button>导出</el-button>
            <el-button>数据表实体检查</el-button>
          </div>
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
              prop="user"
              label="数据对象名"
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
            >
              <template>
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
                <el-button>修改</el-button>
                <el-button>预览</el-button>
                <el-button>生成</el-button>
              </template>
            </el-table-column>
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
          lastEditTime: '2012-11-13',
          isUse: true
        },
        {
          user: 'T_JZG',
          name: '教职工基本信息',
          category: '人员基础信息/教职工基础信息',
          lastEditTime: '2012-11-13',
          isUse: true
        },
        {
          user: 'T_JZG',
          name: '教职工基本信息',
          category: '人员基础信息/教职工基础信息',
          lastEditTime: '2012-11-13',
          isUse: true
        }
      ]
    }
  }
}
</script>

<style>
</style>
