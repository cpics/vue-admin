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
        <el-col :span="16">
          <div class="grid-content">

            <el-input v-model="input" placeholder="请输入内容" style="width:80%" />
            <el-button>索引</el-button>
          </div>

        </el-col>
      </el-row>
    </div>
    <el-row>
      <el-table
        ref="multipleTable"
        border
        :data="tableData"
        tooltip-effect="dark"
        style="width: 100%"
      >
        <el-table-column
          prop="state"
          label="状态"
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
            <el-button>授权</el-button>
            <el-button>服务说明</el-button>
          </template>
        </el-table-column>

      </el-table>
    </el-row>
    <el-row>
      <el-pagination
        background
        layout="prev, pager, next"
        :total="1000"
      />
    </el-row>
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
      value: '',
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
      }]
    }
  }
}
</script>

<style>

</style>
