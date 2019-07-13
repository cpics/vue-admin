<template>
  <div class="g-container">
    <div class="mb-20">
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
        style="width: 100%"
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
          width="200"
        >
          <template>
            <el-button type="text" size="small" @click="dialogFormVisible = true">修改</el-button>
            <el-button type="text" size="small" @click="dialogService2 = true">启用</el-button>
            <el-button type="text" size="small" @click="dialogService3 = true">预览</el-button>
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
    <el-dialog title="新增服务1" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="服务名称" :label-width="formLabelWidth">
          <el-input v-model="form.name" autocomplete="off" />
        </el-form-item>
        <el-form-item label="数据来源" :label-width="formLabelWidth">
          <el-select v-model="form.region" placeholder="请选择" class="w-full">
            <el-option label="真实数据" value="shanghai" />
            <el-option label="脱敏数据" value="beijing" />
          </el-select>
        </el-form-item>
        <el-form-item label="服务描述" :label-width="formLabelWidth">
          <el-input v-model="form.desc" type="textarea" />
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
      </div>
    </el-dialog>
    <el-dialog title="新增服务2" :visible.sync="dialogService2">
      <div class="double-columns">
        <div class="column-left">
          <div class="border-box">
            <el-input
              v-model="filterText"
              class="mb-10"
              placeholder="输入关键字进行过滤"
            />
            <el-select
              v-model="value"
              class="mb-10"
              placeholder="请选择"
            >
              <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              />
            </el-select>

            <el-tree
              ref="tree"
              class="filter-tree"
              :data="data"
              :props="defaultProps"
              default-expand-all
            />
          </div>
        </div>
        <div class="column-right">
          <div class="border-box">
            <el-form ref="form" :model="form">
              <el-form-item label="">
                <el-input v-model="form.desc" class="min-h140" type="textarea" />
              </el-form-item>
              <el-form-item label="WHERE子句">
                <el-input v-model="form.desc" type="textarea" />
              </el-form-item>
              <el-form-item class="txt-c">
                <el-button type="primary">确定</el-button>
                <el-button>取消</el-button>
              </el-form-item>
            </el-form>
          </div>
        </div>
      </div>
    </el-dialog>
    <el-dialog title="新增服务3" :visible.sync="dialogService3">
      <div class="double-columns">
        <div class="column-left">
          <div class="border-box">
            <el-tree
              :data="data"
              show-checkbox
              node-key="id"
              :default-expanded-keys="[2, 3]"
              :default-checked-keys="[5]"
              :props="defaultProps"
            />
          </div>
        </div>
        <div class="column-right">
          <div class="border-box">
            <div class="mb-20">
              <div class="common-title">
                出参
                <i class="el-icon-plus" />
                <i class="el-icon-minus" />
              </div>
              <el-table
                ref="multipleTable"
                :data="tableData"
                style="width: 100%"
                height="200"
              >
                <el-table-column
                  type="selection"
                  width="55"
                />
                <el-table-column
                  prop="state"
                  label="字段名"
                />
                <el-table-column
                  prop="name"
                  label="字段中文名"
                />
                <el-table-column
                  prop="miaoshu"
                  label="表达式"
                />
              </el-table>
            </div>
            <div>
              <div class="common-title">
                入参
                <i class="el-icon-plus" />
                <i class="el-icon-minus" />
              </div>
              <el-table
                ref="multipleTable"
                :data="tableData"
                style="width: 100%"
                height="200"
              >
                <el-table-column
                  type="selection"
                  width="55"
                />
                <el-table-column
                  prop="state"
                  label="字段名"
                />
                <el-table-column
                  prop="name"
                  label="字段中文名"
                />
                <el-table-column
                  prop="miaoshu"
                  label="关系式"
                />
              </el-table>
            </div>
            <div class="txt-c">
              <el-button type="primary">完成</el-button>
            </div>
          </div>
        </div>
      </div>
    </el-dialog>
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
      multipleSelection: [],
      dialogFormVisible: false,
      dialogService2: false,
      dialogService3: false,
      form: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: ''
      },
      formLabelWidth: '120px',
      filterText: '',
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
      },
      watch: {
        filterText(val) {
          this.$refs.tree.filter(val)
        }
      }
      //      methods: {
      //        filterNode(value, data) {
      //          if (!value) return true
      //          return data.label.indexOf(value) !== -1
      //        }
      //      }
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
  .grid-content {
    margin-right: 20px;
  }

  .mb-20 {
    margin-bottom: 20px;
  }

  .mb-10 {
    margin-bottom: 10px;
  }
</style>
