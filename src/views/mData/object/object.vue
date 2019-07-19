<template>
  <div class="g-container">
    <div class="double-columns">
      <div class="column-left">
        <div class="border-box">
          <el-input v-model="filterText" placeholder="按表名查询" />
          <el-tree ref="tree" class="filter-tree" :data="data" :props="defaultProps" default-expand-all :filter-node-method="filterNode" />
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
            <el-button icon="el-icon-plus" type="primary" @click="toggleVisible('add')">新增数据对象</el-button>
            <el-button icon="el-icon-delete" type="danger" @click="handleDelete">删除</el-button>
            <el-button icon="el-icon-refresh" type="warning" @click="dialogSetVisible = true">变更数据分类</el-button>
            <el-button icon="el-icon-upload" type="success" @click="dialogImportVisible = true">导入</el-button>
            <el-button icon="el-icon-download" type="info">导出</el-button>
            <el-button icon="el-icon-check" @click="outerVisible = true">数据表实体检查</el-button>
          </div>
          <el-table ref="multipleTable" :data="tableData" tooltip-effect="dark" style="width: 100%" @selection-change="handleSelectionChange">
            <el-table-column type="selection" width="55" />
            <el-table-column :key="Math.random()" prop="user" label="数据对象名" width="130" />
            <el-table-column :key="Math.random()" prop="name" label="数据对象中文名" />
            <el-table-column :key="Math.random()" prop="category" label="数据对象分类" />
            <el-table-column :key="Math.random()" prop="lastEditTime" label="最后修改时间" />
            <el-table-column label="是否启用" width="150">
              <template>
                <el-switch v-model="isUse" style="display: block" active-color="#13ce66" inactive-color="#ff4949" active-text="YES" inactive-text="NO" />
              </template>
            </el-table-column>
            <el-table-column fixed="right" label="操作" width="130">
              <template>
                <el-button class="mini-btn" type="primary" icon="el-icon-edit" circle title="编辑" @click="toggleVisible('edit')" />
                <el-button class="mini-btn" type="success" icon="el-icon-view" circle title="预览" @click="toggleVisible('preview')" />
                <el-button class="mini-btn" type="warning" icon="el-icon-success" circle title="生成" @click="dialogCreateVisible = true" />
              </template>
            </el-table-column>
          </el-table>
          <el-pagination background layout="prev, pager, next" :total="1000" />
        </div>
      </div>
    </div>
    <el-dialog title="变更数据分类" :visible.sync="dialogSetVisible">
      <el-tree :data="data" show-checkbox node-key="id" :default-expanded-keys="[2, 3]" :default-checked-keys="[5]" :props="defaultProps" />

      <div slot="footer" class="dialog-footer el-dialog__footer">
        <el-button type="primary" @click="dialogSetVisible = false">确定</el-button>
        <el-button @click="dialogSetVisible = false">取消</el-button>
      </div>
    </el-dialog>
    <el-dialog :visible.sync="dialogVisible" :title="optionType === 'add' ? '新增数据对象' : '修改数据对象'">
      <el-tabs v-model="activeName" type="card" @tab-click="handleClick">
        <el-tab-pane label="对象基本信息" name="first">
          <div>
            <el-form :model="form" label-width="130px">
              <el-form-item label="*数据对象大类">
                <el-radio-group v-model="form.resource">
                  <el-radio label="主数据" />
                  <el-radio label="代码表" />
                </el-radio-group>
              </el-form-item>
              <el-form-item label="*数据对象类型">
                <el-select v-model="form.region" placeholder="请选择">
                  <el-option label="表" value="shanghai" />
                  <el-option label="表2" value="beijing" />
                </el-select>
              </el-form-item>
              <el-form-item label="数据对象中文名">
                <el-input v-model="form.name" />
              </el-form-item>
              <el-form-item label="*数据对象名">
                <el-input v-model="form.name" />
              </el-form-item>
              <el-form-item label="最后修改人">
                <el-input v-model="form.name" />
              </el-form-item>
              <el-form-item label="最后修改时间">
                <el-input v-model="form.name" />
              </el-form-item>
              <el-form-item label="数据对象描述">
                <el-input v-model="form.desc" type="textarea" />
              </el-form-item>
            </el-form>
            <div slot="footer" class="dialog-footer el-dialog__footer">
              <el-button v-if="optionType !== 'preview'" type="primary" @click="onSubmit(optionType)">确定</el-button>
              <el-button v-if="optionType !== 'preview'" type="warning" @click="onApply">应用</el-button>
              <el-button @click="toggleVisible">取消</el-button>
            </div>
          </div>
        </el-tab-pane>
        <el-tab-pane label="字段属性" name="second">
          <div>
            <div class="m-buttons-row">
              <el-button v-if="optionType !== 'preview'" icon="el-icon-plus" type="primary">新建</el-button>
              <el-button v-if="optionType !== 'preview'" icon="el-icon-delete" type="danger">删除</el-button>
            </div>
            <el-table ref="multipleTable" :data="tableData" tooltip-effect="dark" style="width: 100%" @selection-change="handleSelectionChange">
              <el-table-column type="selection" width="55" />
              <el-table-column :key="Math.random()" prop="num" label="索引" width="80" />
              <el-table-column :key="Math.random()" prop="name" label="字段名" />
              <el-table-column :key="Math.random()" prop="english" label="中文简称" />
              <el-table-column :key="Math.random()" prop="type" label="字段类型" />
              <el-table-column :key="Math.random()" prop="idefault" label="默认值" />
              <el-table-column :key="Math.random()" prop="name" label="是否主键" />
              <el-table-column :key="Math.random()" prop="isNull" label="是否允许空" />
              <el-table-column :key="Math.random()" prop="isSole" label="是否唯一" />
              <el-table-column label="是否启用" width="150">
                <template>
                  <el-switch v-model="isUse" style="display: block" active-color="#13ce66" inactive-color="#ff4949" active-text="YES" inactive-text="NO" />
                </template>
              </el-table-column>
              <el-table-column v-if="optionType !== 'preview'" fixed="right" label="操作" width="140">
                <template>
                  <el-button class="mini-btn" circle title="编辑" icon="el-icon-edit" type="primary" />
                  <el-button class="mini-btn" circle title="添加" icon="el-icon-plus" type="success" />
                  <el-button class="mini-btn" circle title="导入" icon="el-icon-upload" type="danger" />
                  <!--<el-button  class="mini-btn" circle title="导出" icon="el-icon-download" type="info"></el-button>-->
                </template>
              </el-table-column>
            </el-table>
            <div slot="footer" class="dialog-footer el-dialog__footer">
              <el-button v-if="optionType !== 'preview'" type="primary" @click="onSubmit">确定</el-button>
              <el-button v-if="optionType !== 'preview'" type="warning">应用</el-button>
              <el-button @click="toggleVisible">取消</el-button>
            </div>
          </div>
        </el-tab-pane>
        <el-tab-pane label="引用关系" name="third">
          <div>
            <div class="m-buttons-row">
              <el-button v-if="optionType !== 'preview'" icon="el-icon-delete" type="danger">删除</el-button>
            </div>
            <el-table ref="multipleTable" :data="tableData" tooltip-effect="dark" style="width: 100%" @selection-change="handleSelectionChange">
              <el-table-column type="selection" width="55" />
              <el-table-column :key="Math.random()" prop="name" label="字段名" />
              <el-table-column :key="Math.random()" prop="chinese" label="字段中文简称" />
              <el-table-column :key="Math.random()" prop="obj" label="引用对象" />
              <el-table-column :key="Math.random()" prop="name" label="引用对象中文名" />
              <el-table-column :key="Math.random()" prop="name" label="引用代码表字段" />
              <el-table-column :key="Math.random()" prop="name" label="引用代码表显示字段" />
              <el-table-column v-if="optionType !== 'preview'" fixed="right" label="操作" width="100">
                <template>
                  <el-button class="mini-btn" circle title="导出" icon="el-icon-download" type="info" />
                </template>
              </el-table-column>
            </el-table>
            <div slot="footer" class="dialog-footer el-dialog__footer">
              <el-button v-if="optionType !== 'preview'" type="primary" @click="onSubmit">确定</el-button>
              <el-button v-if="optionType !== 'preview'" type="warning">应用</el-button>
              <el-button @click="toggleVisible">取消</el-button>
            </div>
          </div>
        </el-tab-pane>
      </el-tabs>
    </el-dialog>
    <!--数据库实体检查-->
    <el-dialog title="确认" :visible.sync="outerVisible">
      <div class="dialog-txt">
        即将要对主数据库和代码标准库的全部数据对象进行检查，可能需要较长时间，需要您耐心等待。您确定要进行检查吗?
      </div>
      <el-dialog width="80%" title="数据库实体检查" :visible.sync="innerVisible" append-to-body>
        <el-table :data="tableData" stripe style="width: 100%">
          <el-table-column prop="type" label="类别" width="180" />
          <el-table-column prop="name" label="desc" />
          <el-table-column prop="handle" label="操作" />
          <el-table-column prop="lastEditTime" label="检测时间" />
        </el-table>
      </el-dialog>
      <div slot="footer" class="dialog-footer">
        <el-button @click="outerVisible = false">否</el-button>
        <el-button type="primary" @click="innerVisible = true">是</el-button>
      </div>
    </el-dialog>
    <el-dialog title="导入数据对象" :visible.sync="dialogImportVisible">
      <el-form ref="form" :model="form" label-width="140px">
        <el-form-item label="导入类型">
          <el-select v-model="form.region" placeholder="请选择">
            <el-option label="表" value="1" />
            <el-option label="表2" value="2" />
          </el-select>
          <el-button icon="el-icon-upload">模板下载</el-button>
        </el-form-item>
        <el-form-item label="是否导入技术属性">
          <el-radio-group v-model="form.resource">
            <el-radio label="是" />
            <el-radio label="否" />
          </el-radio-group>
        </el-form-item>
        <el-form-item label="本地文件">
          <el-upload class="upload-demo" action="https://jsonplaceholder.typicode.com/posts/" :on-change="handleChange" :file-list="fileList">
            <el-button size="small" type="success">点击上传</el-button>
            <el-button icon="el-icon-upload">导入数据</el-button>
            <!--<div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>-->
          </el-upload>
        </el-form-item>
        <el-form-item label="导入日志">
          <div class="log-box">
            导入日志导入日志导入日志导入日志导入日志导入日志导入日志导入日志
          </div>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer el-dialog__footer">
        <el-button type="primary" @click="dialogImportVisible = false">确定</el-button>
        <el-button @click="dialogImportVisible = false">关闭</el-button>
      </div>
    </el-dialog>
    <el-dialog title="同步数据对象T_JZG" class="dialog-big" :visible.sync="dialogCreateVisible">
      <div class="double-columns">
        <div class="column-left">
          <div class="common-title">建表脚本</div>
          <div class="script-txt">
            <el-input v-model="form.script" type="textarea" />
          </div>
        </div>
        <div class="column-right">
          <div class="common-title">同步信息</div>
          <el-table :data="tableData" style="width: 100%" max-height="250">
            <el-table-column :key="Math.random()" fixed prop="id" label="ID" width="80" />
            <el-table-column :key="Math.random()" prop="model" label="模型" />
            <el-table-column :key="Math.random()" prop="desc1" label="描述" />
            <el-table-column fixed="right" label="操作" width="100">
              <template>
                <el-button class="mini-btn" type="primary" icon="el-icon-refresh" circle title="同步" />
              </template>
            </el-table-column>
          </el-table>
        </div>
      </div>
      <div slot="footer" class="dialog-footer el-dialog__footer">
        <el-button type="primary" @click="onSubmit2">应用</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
export default {
  data() {
    return {
      multipleSelection: [],
      dialogVisible: false,
      dialogSetVisible: false,
      outerVisible: false,
      innerVisible: false,
      dialogImportVisible: false,
      dialogCreateVisible: false,
      optionType: 'add',
      activeName: 'first',
      filterText: '',
      input1: '',
      input2: '',
      isUse: true,
      region: '',
      data: [
        {
          id: 1,
          label: '数据中心',
          children: [

            {
              id: 4,
              label: '基础类',
              children: [
                {
                  id: 9,
                  label: '教职工基础信息表'
                },
                {
                  id: 10,
                  label: '本科生基础信息表'
                },
                {
                  id: 11,
                  label: '研究生基础信息'
                },
                {
                  id: 12,
                  label: '学校基础信息'
                }
              ]
            },
            {
              id: 2,
              label: '科研类',
              children: [{
                id: 5,
                label: '科研成果'
              }, {
                id: 6,
                label: '科研项目'
              }, {
                id: 6,
                label: '科研考核'
              }, {
                id: 6,
                label: '科研经费'
              }, {
                id: 6,
                label: '学术团体'
              }, {
                id: 6,
                label: '科研交流'
              }, {
                id: 6,
                label: '科研基地'
              }

              ]
            },

            {
              id: 3,
              label: '人事类',
              children: [{
                id: 7,
                label: '聘用管理'
              }, {
                id: 8,
                label: '考核管理'
              }, {
                id: 8,
                label: '异动管理'
              }, {
                id: 8,
                label: '师资管理'
              }, {
                id: 8,
                label: '高级人才'
              }

              ]
            },

            {
              id: 3,
              label: '教务类',
              children: [{
                id: 7,
                label: '培养计划'
              }, {
                id: 8,
                label: '学生项目'
              }, {
                id: 8,
                label: '学籍管理'
              }, {
                id: 8,
                label: '培养管理'
              }, {
                id: 8,
                label: '学生成果'
              }, {
                id: 8,
                label: '教师管理'
              }, {
                id: 8,
                label: '创新管理'
              }, {
                id: 8,
                label: '排课选课'
              }, {
                id: 8,
                label: '教学成果'
              }, {
                id: 8,
                label: '考试考务'
              }, {
                id: 8,
                label: '论文管理'
              }, {
                id: 8,
                label: '成绩管理'
              }

              ]
            },
            {
              id: 3,
              label: '学工类',
              children: [{
                id: 7,
                label: '招生管理'
              }, {
                id: 8,
                label: '招生计划'
              }, {
                id: 8,
                label: '资助管理'
              }, {
                id: 8,
                label: '学工管理'
              }, {
                id: 8,
                label: '录取管理'
              }, {
                id: 8,
                label: '思想教育'
              }, {
                id: 8,
                label: '社会实践'
              }, {
                id: 8,
                label: '迎新管理'
              }, {
                id: 8,
                label: '离校管理'
              }, {
                id: 8,
                label: '综合管理'
              }, {
                id: 8,
                label: '就业管理'
              }, {
                id: 8,
                label: '成绩管理'
              }

              ]
            },
            {
              id: 3,
              label: '财务类',
              children: [{
                id: 7,
                label: '一卡通'
              }, {
                id: 8,
                label: '网络计费'
              }, {
                id: 8,
                label: '网络支付'
              }, {
                id: 8,
                label: '住房补贴'
              }, {
                id: 8,
                label: '学生缴费'
              }, {
                id: 8,
                label: '教工薪资'
              }, {
                id: 8,
                label: '科目凭证'
              }, {
                id: 8,
                label: '票据管理'
              }, {
                id: 8,
                label: '项目经费'
              }

              ]
            },
            {
              id: 3,
              label: '资产类',
              children: [{
                id: 7,
                label: '房产'
              }, {
                id: 8,
                label: '设备'
              }, {
                id: 8,
                label: '基础'
              }

              ]
            },

            {
              id: 3,
              label: '研工类',
              children: [{
                id: 7,
                label: '培养计划'
              }, {
                id: 8,
                label: '学科建设'
              }, {
                id: 8,
                label: '学籍管理'
              }, {
                id: 8,
                label: '招生管理'
              }, {
                id: 8,
                label: '招生计划'
              }, {
                id: 8,
                label: '资助管理'
              }, {
                id: 8,
                label: '导师管理'
              }, {
                id: 8,
                label: '录取管理'
              }, {
                id: 8,
                label: '教师管理'
              }, {
                id: 8,
                label: '学位管理'
              }, {
                id: 8,
                label: '排课选课'
              }, {
                id: 8,
                label: '教学教务'
              }, {
                id: 8,
                label: '社会实践'
              }, {
                id: 8,
                label: '学位学科'
              }, {
                id: 8,
                label: '综合管理'
              }, {
                id: 8,
                label: '考试考务'
              }, {
                id: 8,
                label: '成绩管理'
              },
              {
                id: 8,
                label: '研工管理'
              }

              ]
            },

            {
              id: 3,
              label: '其他类',
              children: [{
                id: 7,
                label: '校友信息'
              }, {
                id: 8,
                label: '医疗卫生'
              }, {
                id: 8,
                label: '大数据综合实训室'
              },
              {
                id: 8,
                label: '智慧资助管理'
              },
              {
                id: 8,
                label: '核心素质管理'
              }, {
                id: 8,
                label: '高校审计数据管理'
              },
              {
                id: 8,
                label: '高职类专用管理'
              }

              ]
            }

          ]
        }

      ],
      tableData: [
        {
          user: 'T_JZG',
          name: '教职工基本信息',
          category: '人员基础信息/教职工基础信息',
          lastEditTime: '2012-11-13',
          num: '1',
          english: 'SSDDD',
          type: '人事系统',
          idefault: '1',
          isKey: '是',
          isNull: '否',
          isSole: '是',
          chinese: '工人技术等级代码',
          obj: 'SDDDD',
          handle: '建议更新元数据建议更新数据库表',
          desc: 'T_JZG(教职工基本信息)表 PRZTDM(聘任状态代码)字段元数据表字段存在，但在数据库中不存在',
          id: '1',
          model: 'MZ VARCHAR2(50)',
          desc1: '数据库表字段不存在'
        },
        {
          user: 'T_XK',
          name: '教务选课基础信息',
          category: '教务系统/选课基础信息',
          lastEditTime: '2012-10-13',
          num: '1',
          english: 'SSDDD',
          type: '教务系统',
          idefault: '1',
          isKey: '是',
          isNull: '否',
          isSole: '是',
          chinese: '工人技术等级代码',
          obj: 'SDDDD',
          handle: '建议更新元数据建议更新数据库表',
          desc: 'T_XK(教职工基本信息)表 PRZTDM(聘任状态代码)字段元数据表字段存在，但在数据库中不存在',
          id: '2',
          model: 'MZ VARCHAR2(50)',
          desc1: '数据库表字段不存在'
        },
        {
          user: 'T_CW',
          name: '财务报销信息',
          category: '财务系统/财务报销信息',
          lastEditTime: '2012-11-13',
          num: '1',
          english: 'SSDDD',
          type: '财务系统',
          idefault: '1',
          isKey: '是',
          isNull: '否',
          isSole: '是',
          chinese: '工人技术等级代码',
          obj: 'SDDDD',
          handle: '建议更新元数据建议更新数据库表',
          desc: 'T_CW(教职工基本信息)表 PRZTDM(聘任状态代码)字段元数据表字段存在，但在数据库中不存在',
          id: '3',
          model: 'MZ VARCHAR2(50)',
          desc1: '数据库表字段不存在'
        }
      ],
      form: {
        name: '',
        region: '',
        date1: '',
        date2: '',
        delivery: false,
        type: [],
        resource: '',
        desc: '',
        script: 'CREATE TABLE T_JZG()'
      },
      defaultProps: {
        children: 'children',
        label: 'label'
      },
      fileList: []
    }
  },
  methods: {
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    handleChange() {

    },
    filterNode(value, data) {
      if (!value) return true
      return data.label.indexOf(value) !== -1
    },
    handleClick(tab, event) {
      console.log(tab, event)
    },
    onSubmit(optionType = 'add') {
      if (optionType === 'add') {
        this.tableData.push({
          user: 'T_JZG',
          name: '教职工基本信息',
          category: '人员基础信息/教职工基础信息',
          lastEditTime: '2012-11-13',
          isUse: true
        })
        this.$message({
          message: '新增成功',
          type: 'success'
        })
      } else if (optionType === 'edit') {
        this.$message({
          message: '修改成功',
          type: 'success'
        })
      }
      this.dialogVisible = false
    },
    onSubmit2() {
      this.$message({
        message: '应用成功',
        type: 'success'
      })
      this.dialogCreateVisible = false
    },
    onApply() {
      this.dialogVisible = false
      this.$message({
        message: '应用成功',
        type: 'success'
      })
    },
    toggleVisible(type) {
      if (type === 'add') {
        this.optionType = 'add'
      } else if (type === 'edit') {
        this.optionType = 'edit'
      } else if (type === 'preview') {
        this.optionType = 'preview'
      }
      this.dialogVisible = !this.dialogVisible
    },
    handleDelete() {
      if (this.multipleSelection.length == 0) {
        this.$message({
          message: '请勾选你需要删除的数据',
          type: 'warning'
        })
      } else {
        this.multipleSelection.forEach(item => {
          this.tableData.forEach((d, i) => {
            if (item.id == d.id) {
              this.tableData.splice(i, 1)
            }
          })
        })
      }
    }
  }
}
</script>

<style>
</style>
