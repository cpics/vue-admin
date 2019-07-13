<template>
  <div class="g-container">
    <div>
      <el-row>
        <el-col :span="4">
          <div class="grid-content">
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
          </div>
        </el-col>
        <el-col :span="12">
          <div class="grid-content">

            <el-input v-model="input" placeholder="请输入内容" style="width:80%" />
            <el-button>索引</el-button>
          </div>

        </el-col>
        <el-col :span="4">
          <div class="grid-content">
            <el-select
              v-model="value2"
              placeholder="操作"
            >
              <el-option
                v-for="item in options2"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              />
            </el-select>
          </div>

        </el-col>
      </el-row>
    </div>
    <div class="data-list">
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
          prop="state"
          label="状态"
        />
        <el-table-column
          prop="source"
          label="数据来源"
        />
        <el-table-column
          prop="name"
          label="服务名称"
        />
        <el-table-column
          prop="miaoshu"
          label="服务描述"
        />
        <el-table-column
          label="操作"
          width="300"
        >
          <template>
            <el-button>修改</el-button>
            <el-button>启用</el-button>
            <el-button>预览</el-button>
          </template>
        </el-table-column>
      </el-table>
      <div>
        <el-pagination
          background
          layout="prev, pager, next"
          :total="1000"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      input: '',
      options: [{
        value: '1',
        label: '自定义服务'
      }, {
        value: '2',
        label: '预加载服务'
      }],
      options2: [{
        value: '1',
        label: '新增'
      }, {
        value: '2',
        label: '删除'
      }],
      value: '',
      value2: '',
      tableData: [{
        state: '111',
        source: '222',
        name: '222',
        miaoshu: '333'
      }, {
        state: '111',
        source: '222',
        name: '222',
        miaoshu: '333'
      }, {
        state: '111',
        source: '222',
        name: '222',
        miaoshu: '333'
      }, {
        state: '111',
        source: '222',
        name: '222',
        miaoshu: '333'
      }],
      multipleSelection: []
    }
  }
}
</script>

<style>
</style>
