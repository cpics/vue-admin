<template>
  <div class="g-container">
    <el-row class="m-filter-row">
      <el-col class="filter-label" :span="2" align justify>角色代码：</el-col>
      <el-col class="mr-20" :span="6" align justify>
        <el-input v-model="input1" placeholder="请输入内容" />
      </el-col>
      <el-col class="filter-label" :span="2" align justify>角色名称：</el-col>
      <el-col class="mr-20" :span="6" align justify>
        <el-input v-model="input2" placeholder="请输入内容" />
      </el-col>
      <el-col :span="4" align justify>
        <el-button icon="el-icon-search" type="primary">查询</el-button>
      </el-col>
    </el-row>
    <div>
      <el-table
        :data="tableData"
        style="width: 100%"
      >
        <el-table-column
          prop="code"
          label="角色代码"
        />
        <el-table-column
          prop="name"
          label="角色名称"
        />
        <el-table-column
          fixed="right"
          label="授权配置"
          width="120"
        >
          <template>
            <el-button class="mini-btn" type="primary" icon="el-icon-setting" circle title="配置" @click="dialogSetVisible = true" />
          </template>
        </el-table-column>
      </el-table>
      <el-pagination background layout="prev, pager, next" :total="1000" />
    </div>
    <el-dialog title="配置" :visible.sync="dialogSetVisible">
      <el-row class="m-filter-row">
        <el-col class="mr-20" :span="4" align justify>
          <el-button icon="el-icon-document" type="primary" @click="save">保存</el-button>
        </el-col>
        <el-col class="filter-label" :span="2" align justify>查询条件：</el-col>
        <el-col class="mr-20" :span="6" align justify>
          <el-input v-model="input2" placeholder="请输入查询条件" />
        </el-col>
        <el-col :span="4" align justify>
          <el-button icon="el-icon-search" type="primary">查询</el-button>
        </el-col>
      </el-row>
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
      input1: '',
      input2: '',
      dialogSetVisible: false,

      tableData: [{
        code: 'sysadmin',
        name: '系统管理员'
      }, {
        code: 'guide_mg',
        name: '指南管理'
      }, {
        code: 'sysadmin',
        name: '系统管理员'
      }, {
        code: 'guide_mg',
        name: '指南管理'
      }, {
        code: 'sysadmin',
        name: '系统管理员'
      }, {
        code: 'guide_mg',
        name: '指南管理'
      }],
      data: [{
        id: 1,
        label: '主数据管理平台',
        children: [{
          id: 4,
          label: '元数据管理',
          children: [{
            id: 9,
            label: '数据源管理'
          }, {
            id: 10,
            label: '数据对象管理'
          }]
        }, {
          id: 4,
          label: '主数据管理',
          children: [{
            id: 9,
            label: '主数据概要'
          }, {
            id: 10,
            label: '主数据管理'
          }]
        }, {
          id: 4,
          label: '代码标准管理',
          children: [{
            id: 9,
            label: '标准管理'
          }, {
            id: 10,
            label: '映射管理'
          }, {
            id: 10,
            label: '一致性检查'
          }
          ]
        }, {
          id: 4,
          label: '运行监控管理',
          children: [{
            id: 9,
            label: '数据集成管理'
          }, {
            id: 10,
            label: '数据库监控'
          }
          ]
        }, {
          id: 4,
          label: '数据共享接口',
          children: [{
            id: 9,
            label: '共享服务'
          }, {
            id: 10,
            label: '服务管理'
          }, {
            id: 10,
            label: '服务运行'
          }, {
            id: 10,
            label: '运行监控'
          }, {
            id: 10,
            label: '调用统计'
          }
          ]
        }, {
          id: 4,
          label: '质量检测管理',
          children: [{
            id: 9,
            label: '质量检测'
          }, {
            id: 10,
            label: '检测模板'
          }, {
            id: 10,
            label: '规则配置'
          }, {
            id: 10,
            label: '质量查询'
          }, {
            id: 10,
            label: '质量提醒'
          }, {
            id: 10,
            label: '任务调度'
          }
          ]
        }, {
          id: 4,
          label: '数据备份管理',
          children: [{
            id: 9,
            label: '数据备份'
          }, {
            id: 10,
            label: '系统日志'
          }, {
            id: 10,
            label: '数据库查询'
          }
          ]
        }, {
          id: 4,
          label: '系统管理',
          children: [{
            id: 9,
            label: '角色管理'
          }, {
            id: 10,
            label: '菜单管理'
          }, {
            id: 10,
            label: '权限管理'
          }, {
            id: 10,
            label: '配置管理'
          }
          ]
        }

        ]
      }],
      defaultProps: {
        children: 'children',
        label: 'label'
      }
    }
  },
  methods: {
    save() {
      this.$message({
        message: '保存成功',
        type: 'success'
      })
      this.dialogSetVisible = false
    }
  }
}
</script>

<style>

</style>
