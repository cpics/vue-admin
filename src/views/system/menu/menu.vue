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
          <div class="tem-rule-filter">
            <div class="tem-button">
              <el-button type="primary">增加</el-button>
              <el-button type="success">编辑</el-button>
              <el-button type="danger">删除</el-button>
            </div>
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
          caidan: 'system_menu',
          name: '系统菜单',
          show: '系统菜单',
          is: '否',
          level: '1'
        },
        {
          caidan: 'system_menu',
          name: '系统菜单',
          show: '系统菜单',
          is: '否',
          level: '1'
        },
        {
          caidan: 'system_menu',
          name: '系统菜单',
          show: '系统菜单',
          is: '否',
          level: '1'
        }
      ]
    }
  }
}
</script>

<style>

</style>
