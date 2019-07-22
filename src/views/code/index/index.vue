<template>
  <div class="g-container">
    <div class="double-columns tem-rule-main">
      <div class="column-left">
        <div class="border-box tem-rule-tree">
          <el-input v-model="filterText" placeholder="请输入关键字" />
          <el-tree ref="tree" class="filter-tree" :data="data" :props="defaultProps" default-expand-all :filter-node-method="filterNode" @node-click="handleNodeClick" />
        </div>
      </div>
      <div v-if="pageType === 0" class="column-right">
        <el-form ref="formInline" v-model="formInline" :inline="true">
          <el-form-item label="查询类型:" prop="formInline.type">
            <el-select v-model="formInline.type" placeholder="请选择" clearable>
              <el-option label="全部" value="0" />
              <el-option label="表名或数据" value="1" />
              <el-option label="表名" value="2" />
              <el-option label="数据" value="3" />
            </el-select>
          </el-form-item>
          <el-form-item label="关键字:" prop="formInline.keyword">
            <el-input v-model="formInline.keyword" />
          </el-form-item>
          <el-form-item>
            <el-button type="primary" icon="el-icon-search" @click="handleSearch">查询</el-button>
          </el-form-item>
        </el-form>

        <div class="data-statistics">
          <div class="statistics-col">
            <div class="statistics-chart">
              <div ref="dmChart" style="height:90%;width:90%;" />
            </div>
          </div>
          <div class="statistics-col">
            <div class="statistics-chart">
              <div ref="dmChart2" style="height:90%;width:90%;" />
            </div>
          </div>
          <div class="statistics-col">
            <div class="statistics-chart">
              <div ref="dmChart3" style="height:90%;width:90%;" />
            </div>
          </div>
          <div class="statistics-col">
            <div class="statistics-chart">
              <div ref="dmChart4" style="height:90%;width:90%;" />
            </div>
          </div>
        </div>
      </div>

      <div v-if="pageType === 1" class="column-right">
        <el-tabs v-model="activeName" type="card">
          <el-tab-pane label="标准数据" name="first">
            <div class="m-buttons-row">
              <el-button type="primary">导入</el-button>
              <el-button type="primary">导出</el-button>
              <el-button icon="el-icon-circle-plus-outline" type="primary" @click="dialogFormVisible = true">新增</el-button>
              <el-button icon="el-icon-delete" type="danger">删除</el-button>
            </div>
            <div>
              <el-table ref="multipleTable" :data="tableData" tooltip-effect="dark" style="width: 100%">
                <el-table-column type="selection" width="55" />
                <el-table-column prop="id" label="ID" width="60" />
                <el-table-column prop="name" label="名称" />
                <el-table-column label="是否使用">
                  <template>
                    <el-switch v-model="isUse" active-color="#13ce66" inactive-color="#ff4949">
                      />
                    </el-switch>
                  </template>
                </el-table-column>
                <el-table-column prop="release" label="发布情况" />
                <el-table-column prop="lastEditTime" label="最后修改时间" />
                <el-table-column prop="source" label="标准来源" />
                <el-table-column fixed="right" label="操作" width="120">
                  <template>
                    <el-button class="mini-btn" type="primary" icon="el-icon-edit" circle title="编辑" @click="dialogFormVisible = true" />
                    <el-button class="mini-btn" type="success" icon="el-icon-time" circle title="排序" />
                  </template>
                </el-table-column>
              </el-table>
            </div>
          </el-tab-pane>
          <el-tab-pane label="标准模式" name="second">
            <el-row class="m-filter-row">
              <el-col class="filter-label" :span="2" align justify>标准名称：</el-col>
              <el-col class="mr-20" :span="6" align justify>
                <el-input v-model="form2.input1" :disabled="true" />
              </el-col>
              <el-col class="filter-label w-140" :span="4" align justify>英文标准名称：</el-col>
              <el-col class="mr-20" :span="6" align justify>
                <el-input v-model="form2.input2" :disabled="true" />
              </el-col>
            </el-row>
            <el-row class="m-filter-row">
              <el-col class="filter-label" :span="2" align justify>标准级别：</el-col>
              <el-col class="mr-20" :span="6" align justify>
                <el-input v-model="form2.input3" :disabled="true" />
              </el-col>
              <el-col class="filter-label w-140" :span="4" align justify>编码说明：</el-col>
              <el-col class="mr-20" :span="6" align justify>
                <el-input v-model="form2.input4" :disabled="true" />
              </el-col>
            </el-row>
            <el-row class="m-filter-row">
              <el-col class="filter-label" :span="2" align justify>收录日期：</el-col>
              <el-col class="mr-20" :span="6" align justify>
                <el-input v-model="form2.input5" :disabled="true" />
              </el-col>
            </el-row>
          </el-tab-pane>
          <el-tab-pane label="代码映射关系" name="third">
            <h3>表映射关系</h3>
            <el-table ref="form3" :data="tableData3" tooltip-effect="dark" style="width: 100%">
              <el-table-column prop="codeTable" label="标准代码表" />
              <el-table-column prop="dataFlow" label="数据流向" />
              <el-table-column prop="businessSys" label="业务系统" />
              <el-table-column prop="release" label="发布情况" />
            </el-table>
            <h3>字段映射关系（根据表映射联动获得）</h3>
            <el-table ref="form4" :data="tableData4" tooltip-effect="dark" style="width: 100%">
              <el-table-column prop="codeField" label="标准代码字段" />
              <el-table-column prop="codeFieldSimple" label="标准代码字段中文简称" />
              <el-table-column prop="businessCodeField" label="业务代码字段" />
              <el-table-column prop="businessCodeFieldSimple" label="业务代码字段中文简称" />
            </el-table>
            <h3>值映射关系（根据字段映射联动获得）</h3>
            <el-table ref="form5" :data="tableData5" tooltip-effect="dark" style="width: 100%">
              <el-table-column prop="codeValue" label="标准字段值" />
              <el-table-column prop="fieldValue" label="业务字段值" />
            </el-table>
          </el-tab-pane>
        </el-tabs>
      </div>
    </div>
    <el-dialog title="新增映射" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="业务表" :label-width="formLabelWidth">
          <el-input v-model="form.businessTable" autocomplete="off" />
        </el-form-item>
        <el-form-item label="业务表字段" :label-width="formLabelWidth">
          <el-input v-model="form.businessField" autocomplete="off" />
        </el-form-item>
        <el-form-item label="标准代码表" :label-width="formLabelWidth">
          <el-input v-model="form.codeTable" autocomplete="off" />
        </el-form-item>
        <el-form-item label="代码字段名称" :label-width="formLabelWidth">
          <el-input v-model="form.fieldName" autocomplete="off" />
        </el-form-item>
        <el-form-item label="显示字段名称" :label-width="formLabelWidth">
          <el-input v-model="form.showFieldName" autocomplete="off" />
        </el-form-item>
        <el-form-item label="数据流向" :label-width="formLabelWidth">
          <el-select v-model="form.dataFlow" placeholder="请选择" class="w-full">
            <el-option label="主数据库到业务表" value="1" />
            <el-option label="业务表到主数据库" value="2" />
          </el-select>
        </el-form-item>
      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
      </div>
    </el-dialog>
  </div>
</template>

<script>
import echarts from 'echarts'
require('echarts/theme/macarons') // echarts theme
export default {
  data() {
    return {
      dialogFormVisible: false,
      formLabelWidth: '140px',
      activeName: 'first',
      dmChart: null,
      isUse: true,
      filterText: '',
      formInline: {
        type: '',
        keyword: ''
      },
      form: {
        businessTable: '',
        businessField: '',
        codeTable: '',
        fieldName: '',
        showFieldName: '',
        dataFlow: ''
      },
      form2: {
        input1: '宗教',
        input2: 'T_ZXBZ_ZJ',
        input3: 'GB',
        input4: '1 位代码，8 种类别。',
        input5: '2019-06-21'
      },
      dmOptions: {
        title: {
          text: '代码标准(表数量)'
        },
        tooltip: {
          trigger: 'axis',
          axisPointer: {
            type: 'shadow'
          }
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: {
          type: 'value',
          boundaryGap: [0, 0.01]
        },
        yAxis: {
          type: 'category',
          data: ['学校管理类代码', '学生管理类代码', '教学管理类代码', '教职工管理类代码', '通用人员管理类代码', '科研管理类代码', '资产、图书、实验室管理类代码', '财务管理类代码']
        },
        series: [
          {
            name: '代码标准(表数量)',
            type: 'bar',
            data: [22, 42, 80, 60, 112, 120, 90, 110]
          }
        ]
      },
      data: [{
        id: 1,
        label: '代码标准',
        children: [{
          id: 4,
          label: '全局字典',
          children: [{
            id: 9,
            label: '国家地区[T_CODE_GJDQ]'
          }, {
            id: 10,
            label: '性别[T_CODE_XB]'
          }, {
            id: 11,
            label: '政治面貌[T_CODE_ZZMM]'
          }]
        },
        { id: 1, label: '人事', children: [
          { id: 1, label: '其他[T_CODE_OTHER]' }
        ] },
        { id: 1, label: '科研', children: [
          { id: 1, label: '其他[T_CODE_OTHER]' }
        ] },
        { id: 1, label: '学工', children: [
          { id: 1, label: '其他[T_CODE_OTHER]' }
        ] },
        { id: 1, label: '教学', children: [
          { id: 1, label: '其他[T_CODE_OTHER]' }
        ] },
        { id: 1, label: '资产', children: [
          { id: 1, label: '其他[T_CODE_OTHER]' }
        ] },
        { id: 1, label: '财务', children: [
          { id: 1, label: '其他[T_CODE_OTHER]' }
        ] },
        { id: 1, label: '外事', children: [
          { id: 1, label: '其他[T_CODE_OTHER]' }
        ] },
        { id: 1, label: '办公', children: [
          { id: 1, label: '其他[T_CODE_OTHER]' }
        ] },
        { id: 1, label: '档案', children: [
          { id: 1, label: '其他[T_CODE_OTHER]' }
        ] },
        { id: 1, label: '体育', children: [
          { id: 1, label: '其他[T_CODE_OTHER]' }
        ] },
        { id: 1, label: '党团组织', children: [
          { id: 1, label: '其他[T_CODE_OTHER]' }
        ] },
        { id: 1, label: '其他管理', children: [
          { id: 1, label: '其他[T_CODE_OTHER]' }
        ] }
        ]
      }],
      tableData: [
        {
          id: 1,
          name: '1级',
          isUse: true,
          release: '已发布',
          lastEditTime: '2018-04-02',
          source: 'GB'
        },
        {
          id: 2,
          name: '2级',
          isUse: true,
          release: '已发布',
          lastEditTime: '2018-04-02',
          source: 'GB'
        },
        {
          id: 3,
          name: '3级',
          isUse: true,
          release: '已发布',
          lastEditTime: '2018-04-02',
          source: 'GB'
        }
      ],
      tableData3: [
        {
          codeTable: 'T_ZXBZ_XB（性别）',
          dataFlow: '=>',
          businessSys: '人事系统',
          release: '已发布'
        },
        {
          codeTable: 'T_ZXBZ_XB（性别）',
          dataFlow: '=>',
          businessSys: '人事系统',
          release: '已发布'
        },
        {
          codeTable: 'T_ZXBZ_XB（性别）',
          dataFlow: '=>',
          businessSys: '人事系统',
          release: '已发布'
        }
      ],
      tableData4: [
        {
          codeField: '0',
          codeFieldSimple: '未知的性别',
          businessCodeField: 'A',
          businessCodeFieldSimple: '未知的性别'
        }, {
          codeField: '1',
          codeFieldSimple: '男性',
          businessCodeField: 'B',
          businessCodeFieldSimple: '男性'
        }, {
          codeField: '2',
          codeFieldSimple: '女性',
          businessCodeField: 'C',
          businessCodeFieldSimple: '女性'
        }
      ],
      tableData5: [
        {
          codeValue: '0',
          fieldValue: 'A'
        }, {
          codeValue: '1',
          fieldValue: 'B'
        }, {
          codeValue: '2',
          fieldValue: 'C'
        }
      ],
      defaultProps: {
        children: 'children',
        label: 'label'
      },
      pageType: 0
    }
  },
  mounted() {
    this.initDmChart()
  },
  methods: {
    initDmChart() {
      this.dmChart = echarts.init(this.$refs.dmChart)
      this.dmChart.setOption(this.dmOptions)

      this.dmChart2 = echarts.init(this.$refs.dmChart2)
      this.dmChart2.setOption(this.dmOptions)

      this.dmChart3 = echarts.init(this.$refs.dmChart3)
      this.dmChart3.setOption(this.dmOptions)

      this.dmChart4 = echarts.init(this.$refs.dmChart4)
      this.dmChart4.setOption(this.dmOptions)
    },
    handleNodeClick(node, data, value) {
      this.pageType = 1
    },
    filterNode(value, data) {
      if (!value) return true
      return data.label.indexOf(value) !== -1
    },
    handleSearch() {
      this.$message({
        message: '查询成功',
        type: 'success'
      })
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
.data-statistics {
  font-size: 0;
  padding: 20px 0;
  margin-left: -20px;
  .statistics-col {
    width: 46%;
    min-width: 450px;
    color: #333;
    font-size: 16px;
    display: inline-block;
    margin-left: 20px;
    .statistics-tit {
      padding: 0 0 10px;
    }
    .statistics-chart {
      width: 100%;
      height: 280px;
      margin-bottom: 15px;
    }
  }
}
</style>
