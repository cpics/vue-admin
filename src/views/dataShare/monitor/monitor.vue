<template>
  <div class="g-container">
    <div class="double-columns tem-rule-main">
      <div class="column-left">
        <div class="border-box tem-rule-tree">
          <el-input
            v-model="filterText"
            placeholder="数据目录"
          />
          <el-tree
            ref="tree"
            class="filter-tree"
            :data="data"
            :props="defaultProps"
            :filter-node-method="filterNode"
          />
        </div>
      </div>
      <div class="column-right">
        <div class="border-box">
          <el-row class="m-filter-row">
            <el-col class="filter-label w-60" :span="2">状态：</el-col>
            <el-col class="mr-20" :span="6">
              <el-select
                v-model="form.template"
                placeholder="请选择"
              >
                <el-option
                  label="成功"
                  value="1"
                />
                <el-option
                  label="失败"
                  value="2"
                />
                <el-option
                  label="违法"
                  value="3"
                />
              </el-select>
            </el-col>
            <el-col class="filter-label w-60" :span="4">日期：</el-col>
            <el-col :span="12">
              <el-date-picker
                v-model="form.date"
                type="daterange"
                range-separator="至"
                start-placeholder="开始日期"
                end-placeholder="结束日期"
              />
            </el-col>
          </el-row>
          <div class="m-buttons-row">
            <el-button type="primary" icon="el-icon-search">查询</el-button>
            <el-button type="success" icon="el-icon-eye" @click="showDia">监控</el-button>
          </div>
          <el-table
            ref="multipleTable"
            :data="tableData"
            tooltip-effect="dark"
            style="width: 100%"
            @selection-change="wFilterTableData"
          >
            <el-table-column
              type="selection"
              width="55"
            />
            <el-table-column
              prop="id"
              label="ID"
            />
            <el-table-column
              prop="fwName"
              label="服务名"
            />
            <el-table-column
              prop="ywy"
              label="业务域"
            />
            <el-table-column
              prop="sqID"
              label="申请ID"
            />
            <el-table-column
              prop="state"
              label="调用状态"
            />
            <el-table-column
              prop="rzxx"
              label="日志信息"
            />
            <el-table-column
              prop="date"
              label="调用日期"
            />
          </el-table>
          <el-pagination background layout="prev, pager, next" :total="1000" />
        </div>
      </div>
    </div>
    <el-dialog
      title="监控"
      :visible.sync="dialogFormVisible"
    >
      <div class="jk-pop">
        <div ref="jkPopChart" style="width:90%;height:90%" />
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
      jkPopChart: null,
      jkOptions: {
        color: ['#3398DB'],
        tooltip: {
          trigger: 'axis',
          axisPointer: { // 坐标轴指示器，坐标轴触发有效
            type: 'shadow' // 默认为直线，可选为：'line' | 'shadow'
          }
        },
        grid: {
          left: '3%',
          right: '4%',
          bottom: '3%',
          containLabel: true
        },
        xAxis: [
          {
            type: 'category',
            data: ['成功', '失败', '非法'],
            axisTick: {
              alignWithLabel: true
            }
          }
        ],
        yAxis: [
          {
            type: 'value'
          }
        ],
        series: [
          {
            name: '直接访问',
            type: 'bar',
            barWidth: '60%',
            data: [10, 52, 200]
          }
        ]
      },
      type: 1, // 1代表添加，2代表修改
      multipleSelection: [],
      popSelection: [],
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
      formLabelWidth: '120px',
      tableData: [
        {
          id: 0,
          fwName: '人员基本信息',
          ywy: '人事',
          sqID: '001',
          state: '200',
          rzxx: 'successful',
          date: '2019-06-20 17:28:37.0'
        },
        {
          id: 2,
          fwName: '人员基本信息',
          ywy: '人事',
          sqID: '001',
          state: '200',
          rzxx: 'successful',
          date: '2019-06-20 17:28:37.0'
        }
      ],
      dialogFormVisible: false,
      data: [{
        id: 1,
        label: '数据中心',
        children: [{
          id: 4,
          label: '基础类',
          children: [{
            id: 9,
            label: '学校基础信息',
            children: [{
              id: 10,
              label: '学校信息'
            }, {
              id: 11,
              label: '校区信息'
            }]
          }, {
            id: 10,
            label: '本科生基础信息',
            children: [{ id: 20, label: '本专科生基础信息' }, { id: 21, label: '本专科生工作信息' },
              { id: 20, label: '本专科生家庭信息' }, { id: 21, label: '本专科生培训信息' },
              { id: 20, label: '本专科生通讯信息' }, { id: 21, label: '本专科生奖励信息' },
              { id: 20, label: '本专科生政治面貌' }

            ]
          }, {
            id: 10,
            label: '教职工基础信息',
            children: [
              { id: 30, label: '工作简历' },
              { id: 30, label: '奖励荣誉' },
              { id: 30, label: '家庭成员' },
              { id: 30, label: '通讯信息' },
              { id: 30, label: '学历学位' },
              { id: 30, label: '政治面貌' }

            ]
          }, {
            id: 10,
            label: '研究生基础信息',
            children: [
              { id: '40', label: '基础信息' },
              { id: '40', label: '工作经历' },
              { id: '40', label: '奖励信息' },
              { id: '40', label: '家庭成员' },
              { id: '40', label: '培训信息' },
              { id: '40', label: '通讯信息' },
              { id: '40', label: '学习信息' },
              { id: '40', label: '政治面貌' }
            ]
          }

          ]
        }, {
          id: 2,
          label: '科研类',
          children: [
            {
              id: 20,
              label: '科研成果',
              children: [
                { id: 10, label: '学术论文' },
                { id: 10, label: '科研著作' },
                { id: 10, label: '科研专利' },
                { id: 10, label: '获奖成果' },
                { id: 10, label: '鉴定成果' },
                { id: 10, label: '软件著作权' },
                { id: 10, label: '咨询报告' },
                { id: 10, label: '信息标准' }
              ]

            }, {
              id: 20,
              label: '科研项目',
              children: [
                { id: 10, label: '科研附件' },
                { id: 10, label: '项目信息' },
                { id: 10, label: '项目人员' },
                { id: 10, label: '课题信息' },
                { id: 10, label: '协作单位' },
                { id: 10, label: '软件著作权' },
                { id: 10, label: '咨询报告' },
                { id: 10, label: '信息标准' }
              ]

            },
            {
              id: 20,
              label: '科研考核',
              children: [
                { id: 10, label: '考核明细' }
              ]

            },
            {
              id: 20,
              label: '科研经费',
              children: [
                { id: 10, label: '经费到账' },
                { id: 10, label: '经费提扣' },
                { id: 10, label: '经费虚分' },
                { id: 10, label: '经费认领' },
                { id: 10, label: '经费预算' },
                { id: 10, label: '经费支出' },
                { id: 10, label: '咨询报告' },
                { id: 10, label: '信息标准' }
              ]

            },
            {
              id: 20,
              label: '学术团体',
              children: [
                { id: 10, label: '基础信息' }
              ]

            },
            {
              id: 20,
              label: '科研交流',
              children: [
                { id: 10, label: '学术报告' },
                { id: 10, label: '学术会议' },
                { id: 10, label: '学术交流' }
              ]

            },
            {
              id: 20,
              label: '科研基地',
              children: [
                { id: 10, label: '科研机构' },
                { id: 10, label: '机构经费' },
                { id: 10, label: '机构学术委员会' }
              ]

            }

          ]

        },
        {
          id: 50,
          label: '人事类',
          children: [
            { id: 10, label: '聘用管理', children: [
              { id: 10, label: '教职工合同' },
              { id: 10, label: '教职工来源' }

            ] },
            { id: 10, label: '考核管理', children: [
              { id: 10, label: '考技考工' },
              { id: 10, label: '资格考试' },
              { id: 10, label: '考核信息' },
              { id: 10, label: '考核信息' },
              { id: 10, label: '组织考核' }

            ] },
            { id: 10, label: '异动管理', children: [
              { id: 10, label: '部门调动' },
              { id: 10, label: '返聘信息' },
              { id: 10, label: '离岗信息' },
              { id: 10, label: '离退休信息' },
              { id: 10, label: '已故人员信息' },
              { id: 10, label: '补助金信息' },
              { id: 10, label: '延退信息' }

            ] }, { id: 10, label: '师资培养', children: [
              { id: 10, label: '干部任免' },
              { id: 10, label: '技术等级' },
              { id: 10, label: '岗位信息' },
              { id: 10, label: '技术职务' },
              { id: 10, label: '出境信息' },
              { id: 10, label: '进修信息' },
              { id: 10, label: '兼职信息' }

            ] }, { id: 10, label: '高级人才', children: [
              { id: 10, label: '博士后信息' },
              { id: 10, label: '专家信息' }

            ] }

          ]

        },
        {
          id: 50,
          label: '教务类',
          children: [
            { id: 10, label: '学籍管理', children: [
              { id: 10, label: '学业信息' },
              { id: 10, label: '异动信息' },
              { id: 10, label: '注册信息' }

            ] },
            { id: 10, label: '培养管理' },
            { id: 10, label: '创新管理' },
            { id: 10, label: '论文管理', children: [
              { id: 10, label: '答辩信息' },
              { id: 10, label: '成员信息' },
              { id: 10, label: '开题信息' },
              { id: 10, label: '学位论文' },
              { id: 10, label: '论文信息' },
              { id: 10, label: '中期考核' },
              { id: 10, label: '评审信息' }

            ] }, { id: 10, label: '本专科生培养计划', children: [
              { id: 10, label: '辅修学位' },
              { id: 10, label: '教学计划' },
              { id: 10, label: '课程信息' },
              { id: 10, label: '合作办学' },
              { id: 10, label: '培养计划' },
              { id: 10, label: '成员信息' },
              { id: 10, label: '学分要求' },
              { id: 10, label: '专业信息' },
              { id: 10, label: '方向信息' },
              { id: 10, label: '院系关系' }

            ] }, { id: 10, label: '教师管理', children: [
              { id: 10, label: '教师信息' },
              { id: 10, label: '教学任务' },
              { id: 10, label: '评教信息' }

            ] }, { id: 10, label: '排课选课', children: [
              { id: 10, label: '课程班级' },
              { id: 10, label: '课程教师' },
              { id: 10, label: '开课信息' },
              { id: 10, label: '课程安排' },
              { id: 10, label: '课程地点' },
              { id: 10, label: '选课信息' }

            ] }, { id: 10, label: '考试考务', children: [
              { id: 10, label: '考场安排' },
              { id: 10, label: '考生安排' }

            ] }, { id: 10, label: '成绩管理', children: [
              { id: 10, label: '等级考试' },
              { id: 10, label: '考试成绩' },
              { id: 10, label: '成绩检测' }

            ] }, { id: 10, label: '学生项目', children: [
              { id: 10, label: '创新项目' },
              { id: 10, label: '成员信息' },
              { id: 10, label: '指导教师' }

            ] }, { id: 10, label: '学生成果', children: [
              { id: 10, label: '获奖信息' },
              { id: 10, label: '专利信息' },
              { id: 10, label: '论文信息' }

            ] }, { id: 10, label: '教学项目', children: [
              { id: 10, label: '教改项目' },
              { id: 10, label: '成员信息' }

            ] }, { id: 10, label: '教学成果', children: [
              { id: 10, label: '精品课程' },
              { id: 10, label: '教学成果' },
              { id: 10, label: '获奖信息' },
              { id: 10, label: '教学著作' }

            ] }

          ]

        }, {
          id: 50,
          label: '学工类',
          children: [
            { id: 10, label: '招生管理' },
            { id: 10, label: '学工管理' },

            { id: 10, label: '迎新管理', children: [
              { id: 10, label: '办理环节' },
              { id: 10, label: '迎新批次' },
              { id: 10, label: '批次成员' },
              { id: 10, label: '批次环节' }

            ] }, { id: 10, label: '离校管理', children: [
              { id: 10, label: '离校办理' },
              { id: 10, label: '离校批次' },
              { id: 10, label: '批次成员' },
              { id: 10, label: '批次环节' }

            ] }, { id: 10, label: '就业管理', children: [
              { id: 10, label: '毕业去向' },
              { id: 10, label: '批次信息' },
              { id: 10, label: '批次成员' },
              { id: 10, label: '求职意愿' },
              { id: 10, label: '用人单位' },
              { id: 10, label: '招聘会信息' }

            ] }, { id: 10, label: '招生管理', children: [
              { id: 10, label: '招生计划' },
              { id: 10, label: '找人人数' },
              { id: 10, label: '招生简章' }

            ] }, { id: 10, label: '录取管理', children: [
              { id: 10, label: '录取信息' }
            ] }, { id: 10, label: '资助管理', children: [
              { id: 10, label: '补助信息' },
              { id: 10, label: '贷款信息' },
              { id: 10, label: '贷款发放' },
              { id: 10, label: '贷款还款' },
              { id: 10, label: '贷款违约' },
              { id: 10, label: '家庭经济' },
              { id: 10, label: '奖学金信息' },
              { id: 10, label: '困难生信息' },
              { id: 10, label: '绿色通道' },
              { id: 10, label: '勤工助学' },
              { id: 10, label: '勤工助学薪酬发放' },
              { id: 10, label: '勤工助学单位' },
              { id: 10, label: '勤工助学岗位' },
              { id: 10, label: '学费补偿与贷款代偿' },
              { id: 10, label: '学费补偿与贷款代偿发放' },
              { id: 10, label: '学费减免' },
              { id: 10, label: '助学金' }

            ] }, { id: 10, label: '思想教育', children: [
              { id: 10, label: '个人荣誉' },
              { id: 10, label: '集体荣誉' },
              { id: 10, label: '心里健康' },
              { id: 10, label: '心里咨询' },
              { id: 10, label: '学生处分' },
              { id: 10, label: '政工队伍' },
              { id: 10, label: '综合测评' }

            ] }, { id: 10, label: '社会实践', children: [
              { id: 10, label: '军训信息' },
              { id: 10, label: '课外赛事' },
              { id: 10, label: '实践活动' },
              { id: 10, label: '预征入伍' }

            ] }, { id: 10, label: '综合管理', children: [
              { id: 10, label: '乘车优惠' },
              { id: 10, label: '假日返校' },
              { id: 10, label: '返校批次' },
              { id: 10, label: '心理咨询师' },
              { id: 10, label: '学生证补办' },
              { id: 10, label: '证明信息' }

            ] }, { id: 10, label: '教学成果', children: [
              { id: 10, label: '精品课程' },
              { id: 10, label: '教学成果' },
              { id: 10, label: '获奖信息' },
              { id: 10, label: '教学著作' }

            ] }

          ]

        }, {
          id: 50,
          label: '财务类',
          children: [
            { id: 10, label: '一卡通', children: [
              { id: 10, label: '充值记录' },
              { id: 10, label: '交易信息' },
              { id: 10, label: '卡户信息' },
              { id: 10, label: '开户信息' },
              { id: 10, label: '操作信息' },
              { id: 10, label: '商户信息' },
              { id: 10, label: '商户报表' },
              { id: 10, label: '商户终端' },
              { id: 10, label: '补助领取' }

            ] },

            { id: 10, label: '网络计费', children: [
              { id: 10, label: '缴费信息' },
              { id: 10, label: '上网信息' },
              { id: 10, label: '账户信息' }

            ] }, { id: 10, label: '支付管理', children: [
              { id: 10, label: '缴费明细' },
              { id: 10, label: '退费明细' },
              { id: 10, label: '缴费项目' }

            ] }, { id: 10, label: '薪资管理', children: [
              { id: 10, label: '工资变动' },
              { id: 10, label: '工资明细' },
              { id: 10, label: '工资属性' },
              { id: 10, label: '年度总额' },
              { id: 10, label: '劳务补贴' }

            ] }, { id: 10, label: '凭证管理', children: [
              { id: 10, label: '科目信息' },
              { id: 10, label: '科目余额' }

            ] },
            { id: 10, label: '往来账务' },
            { id: 10, label: '票据管理' },
            { id: 10, label: '项目经费', children: [
              { id: 10, label: '个人往来款' },
              { id: 10, label: '财务项目' },
              { id: 10, label: '经费来源' },
              { id: 10, label: '项目往来款' },
              { id: 10, label: '项目余额' }

            ] },
            { id: 10, label: '住房补贴', children: [
              { id: 10, label: '购房补贴' },
              { id: 10, label: '租房补贴' }

            ] }

          ]

        }, {
          id: 50,
          label: '资产类',
          children: [
            { id: 10, label: '房产资产', children: [
              { id: 10, label: '资源管理', children: [
                { id: 10, label: '房间信息' },
                { id: 10, label: '房间分配' },
                { id: 10, label: '建筑物信息' },
                { id: 10, label: '建筑物位置' },
                { id: 10, label: '楼层信息' },
                { id: 10, label: '楼宇信息' },
                { id: 10, label: '土地信息' },
                { id: 10, label: '土地使用' },
                { id: 10, label: '土地使用权' }
              ] },
              { id: 10, label: '公用房管理', children: [
                { id: 10, label: '公用房安排' },
                { id: 10, label: '公用房定额' },
                { id: 10, label: '会议室' },
                { id: 10, label: '图书馆' },
                { id: 10, label: '体育场' }
              ] },
              { id: 10, label: '教师公寓管理', children: [
                { id: 10, label: '入住登记' },
                { id: 10, label: '租金缴纳' }
              ] },
              { id: 10, label: '宿舍管理', children: [
                { id: 10, label: '基本信息' },
                { id: 10, label: '宿舍安排' },
                { id: 10, label: '宿舍楼' },
                { id: 10, label: '宿舍区' },
                { id: 10, label: '卫生检查' },
                { id: 10, label: '日志表' }
              ] },
              { id: 10, label: '教室管理', children: [
                { id: 10, label: '基本信息' },
                { id: 10, label: '教学楼' },
                { id: 10, label: '教师使用' }
              ] },
              { id: 10, label: '实验室管理', children: [
                { id: 10, label: '基本信息' },
                { id: 10, label: '经费信息' },
                { id: 10, label: '使用信息' },
                { id: 10, label: '项目信息' }
              ] }

            ] },

            { id: 10, label: '设备资产', children: [
              { id: 10, label: '仪器管理', children: [
                { id: 10, label: '基本信息' },
                { id: 10, label: '处置信息' },
                { id: 10, label: '处置清单' },
                { id: 10, label: '附件信息' },
                { id: 10, label: '设备使用' },
                { id: 10, label: '设备参数' },
                { id: 10, label: '设备维修' }
              ] },
              { id: 10, label: '设施管理', children: [
                { id: 10, label: '基本信息' },
                { id: 10, label: '设施使用' }
              ] },
              { id: 10, label: '家具管理', children: [
                { id: 10, label: '基本信息' },
                { id: 10, label: '处置信息' },
                { id: 10, label: '处置清单' },
                { id: 10, label: '变更信息' },
                { id: 10, label: '变更清单' }
              ] },
              { id: 10, label: '文物管理', children: [
                { id: 10, label: '基本信息' },
                { id: 10, label: '处置信息' },
                { id: 10, label: '处置清单' },
                { id: 10, label: '变更信息' },
                { id: 10, label: '变更清单' }
              ] },
              { id: 10, label: '车辆信息', children: [
                { id: 10, label: '基本信息' },
                { id: 10, label: '处置信息' },
                { id: 10, label: '处置清单' },
                { id: 10, label: '变更信息' },
                { id: 10, label: '变更清单' }
              ] },
              { id: 10, label: '图书管理', children: [
                { id: 10, label: '基本信息' },
                { id: 10, label: '读者类型代码' },
                { id: 10, label: '馆藏地代码' },
                { id: 10, label: '图书资产处置清单' },
                { id: 10, label: '状态标识' },
                { id: 10, label: '读者信息' },
                { id: 10, label: '读者荐购' },
                { id: 10, label: '借阅信息' },
                { id: 10, label: '借阅历史' },
                { id: 10, label: '欠费信息' },
                { id: 10, label: '违章信息' },
                { id: 10, label: '遗失赔偿' },
                { id: 10, label: '预约到书' },
                { id: 10, label: '资产信息' },
                { id: 10, label: '处置信息' },
                { id: 10, label: '违章代码' },
                { id: 10, label: '证件状态' }
              ] },
              { id: 10, label: '无形资产', children: [
                { id: 10, label: '著作权基本信息' },
                { id: 10, label: '著作权处置信息' },
                { id: 10, label: '著作权处置清单' },
                { id: 10, label: '商标基本信息' },
                { id: 10, label: '商标处置信息' },
                { id: 10, label: '商标处置清单' },
                { id: 10, label: '土地使用权' },
                { id: 10, label: '专利基本信息' },
                { id: 10, label: '专利处置信息' },
                { id: 10, label: '专利处置清单' }
              ] }

            ] }, { id: 10, label: '基地平台', children: [
              { id: 10, label: '基地信息' },
              { id: 10, label: '安全评级' },
              { id: 10, label: '评估信息' },
              { id: 10, label: '人员信息' },
              { id: 10, label: '运行信息' }

            ] }

          ]

        }, { id: 10, label: '研工类', children: [
          { id: 10, label: '招生管理' },
          { id: 10, label: '学籍管理' },
          { id: 10, label: '教学教务' },
          { id: 10, label: '学位学科' },
          { id: 10, label: '研工管理' },
          { id: 10, label: '招生计划', children: [{ id: 10, label: '招生简章' }, { id: 10, label: '招生目录' }] },
          { id: 10, label: '录取管理', children: [{ id: 10, label: '录取信息' }, { id: 10, label: '考试成绩' }] },
          { id: 10, label: '学籍管理', children: [
            { id: 10, label: '结束学业信息' }, { id: 10, label: '学籍异动' }, { id: 10, label: '注册信息' }
          ] },
          { id: 10, label: '培养计划',
            children: [
              { id: 10, label: '课程信息' },
              { id: 10, label: '联合培养' },
              { id: 10, label: '培养方案' },
              { id: 10, label: '方案课程' },
              { id: 10, label: '培养计划' }
            ]
          },
          { id: 10, label: '教师管理', children: [
            { id: 10, label: '基本信息' },
            { id: 10, label: '教学任务量' },
            { id: 10, label: '课程酬金' },
            { id: 10, label: '评价信息' }
          ] },
          { id: 10, label: '排课选课', children: [
            { id: 10, label: '讲座信息' },
            { id: 10, label: '开课信息' },
            { id: 10, label: '排课信息' },
            { id: 10, label: '选课信息' }
          ] },
          { id: 10, label: '考试考务', children: [
            { id: 10, label: '考场安排' },
            { id: 10, label: '考生安排' }
          ] },
          { id: 10, label: '成绩管理', children: [
            { id: 10, label: '成绩转换' },
            { id: 10, label: '等级考试' },
            { id: 10, label: '考试成绩' }
          ] },
          { id: 10, label: '学科建设', children: [
            { id: 10, label: '基本信息' },
            { id: 10, label: '学科经费' },
            { id: 10, label: '专业信息' },
            { id: 10, label: '专业方向' },
            { id: 10, label: '专业与院系关系' }
          ] },
          { id: 10, label: '导师管理', children: [
            { id: 10, label: '指导学生' },
            { id: 10, label: '导师信息' },
            { id: 10, label: '招生资格' },
            { id: 10, label: '资助经费' },
            { id: 10, label: '经费发放' },
            { id: 10, label: '经费克扣' }
          ] },
          { id: 10, label: '学位管理', children: [
            { id: 10, label: '分委会信息' },
            { id: 10, label: '分委会成员' },
            { id: 10, label: '答辩信息' },
            { id: 10, label: '答辩成员' },
            { id: 10, label: '开题信息' },
            { id: 10, label: '评审信息' },
            { id: 10, label: '同等学历学位申请' },
            { id: 10, label: '校委会信息' },
            { id: 10, label: '校委会成员' },
            { id: 10, label: '学位论文' },
            { id: 10, label: '中期考核' }
          ] },
          { id: 10, label: '资助管理', children: [
            { id: 10, label: '贷款信息' },
            { id: 10, label: '贷款发放' },
            { id: 10, label: '贷款还贷' },
            { id: 10, label: '贷款合同' },
            { id: 10, label: '贷款违约' },
            { id: 10, label: '绿色通道' },
            { id: 10, label: '勤工助学' },
            { id: 10, label: '勤工助学薪酬发放' },
            { id: 10, label: '勤工助学单位' },
            { id: 10, label: '勤工助学岗位' },
            { id: 10, label: '学费补偿及贷款代偿' },
            { id: 10, label: '学费补偿及贷款代偿发放' },
            { id: 10, label: '学费补偿及贷款代偿发放账号' },
            { id: 10, label: '助学金' }
          ] },
          { id: 10, label: '思想教育', children: [
            { id: 10, label: '奖学金' },
            { id: 10, label: '荣誉称号' },
            { id: 10, label: '心理咨询' },
            { id: 10, label: '学生处分' },
            { id: 10, label: '行政班' },
            { id: 10, label: '政工队伍' }
          ] },
          { id: 10, label: '社会实践', children: [
            { id: 10, label: '实践活动' },
            { id: 10, label: '预征入伍' }
          ] },
          { id: 10, label: '综合管理', children: [
            { id: 10, label: '乘车优惠' },
            { id: 10, label: '证件补办' },
            { id: 10, label: '证明信息' }
          ] }

        ] }, { id: 10, label: '其他信息', children: [
          { id: 10, label: '智慧资助管理', children: [
            { id: 1, label: '贫困生基本信息' },
            { id: 1, label: '助学金发放流水' }
          ] },
          { id: 10, label: '核心素质管理', children: [
            { id: 1, label: '诚信记录' },
            { id: 1, label: '个人消费' },
            { id: 1, label: '学习情况' },
            { id: 1, label: '宿舍文明' },
            { id: 1, label: '体检报告' },
            { id: 1, label: '图书借阅' },
            { id: 1, label: '友善积分' }
          ] },
          { id: 10, label: '大数据综合实验室', children: [
            { id: 1, label: '实验进度' },
            { id: 1, label: '实验室课程' },
            { id: 1, label: '课程步骤实训' },
            { id: 1, label: '在线考试成绩' },
            { id: 1, label: '实验概况' },
            { id: 1, label: '进度班级' }
          ] },
          { id: 10, label: '高职类专用信息集', children: [
            { id: 1, label: '学校概况', children: [
              { id: 1, label: '办学条件信息' },
              { id: 1, label: '产学合作信息' }
            ] },
            { id: 1, label: '教学管理', children: [
              { id: 1, label: '课程/课题建设' },
              { id: 1, label: '校外课程成绩转换' },
              { id: 1, label: '重点专业情况' }
            ] },
            { id: 1, label: '教师管理', children: [
              { id: 1, label: '教师企业实践' }
            ] },
            { id: 1, label: '实训管理', children: [
              { id: 1, label: '顶岗实习' },
              { id: 1, label: '实训单元' },
              { id: 1, label: '实训室人员' },
              { id: 1, label: '基本信息' },
              { id: 1, label: '运行信息' },
              { id: 1, label: '项目信息' },
              { id: 1, label: '实训基地' }
            ] },
            { id: 1, label: '技能鉴定', children: [
              { id: 1, label: '技能鉴定信息' },
              { id: 1, label: '培训及鉴定机构' }
            ] }
          ] },
          { id: 10, label: '高校审计数据标准', children: [
            { id: 1, label: '财务核算系统', children: [
              { id: 1, label: '经济分类总账' },
              { id: 1, label: '科目余额表' },
              { id: 1, label: '凭证表' },
              { id: 1, label: '项目信息' },
              { id: 1, label: '项目预算' },
              { id: 1, label: '项目总账' }
            ] },
            { id: 1, label: '薪酬核算系统', children: [
              { id: 1, label: '薪酬信息表' }
            ] },
            { id: 1, label: '基金会核算系统', children: [
              { id: 1, label: '经济分类总账' },
              { id: 1, label: '科目余额表' },
              { id: 1, label: '凭证表' },
              { id: 1, label: '项目信息' },
              { id: 1, label: '项目分类总账' }
            ] },
            { id: 1, label: '资产管理系统', children: [
              { id: 1, label: '资产管理' }
            ] },
            { id: 1, label: '继续教育', children: [
              { id: 1, label: '非学历教育信息' }
            ] },
            { id: 1, label: '收费系统', children: [
              { id: 1, label: '收费信息' }
            ] },
            { id: 1, label: '设备共享系统', children: [
              { id: 1, label: '设备仪器共享信息' }
            ] },
            { id: 1, label: '学生工作系统', children: [
              { id: 1, label: '奖补类资金发放明细' },
              { id: 1, label: '家庭困难学生情况表' }
            ] },
            { id: 1, label: '本科学籍系统', children: [
              { id: 1, label: '本科学籍系统信息' }
            ] },
            { id: 1, label: '研究生学籍系统', children: [
              { id: 1, label: '研究生学籍系统信息' }
            ] },
            { id: 1, label: '留学生学籍系统', children: [
              { id: 1, label: '留学生学籍信息' }
            ] },
            { id: 1, label: '基建财务系统', children: [
              { id: 1, label: '基建科目总账' },
              { id: 1, label: '基建凭证' }
            ] },
            { id: 1, label: '出国系统', children: [
              { id: 1, label: '高校出国人员信息' },
              { id: 1, label: '出国团组信息' }
            ] },
            { id: 1, label: '科研系统', children: [
              { id: 1, label: '科研信息' }
            ] },
            { id: 1, label: '人事系统', children: [
              { id: 1, label: '高校人才引进' },
              { id: 1, label: '教职工信息' }
            ] }
          ] },
          { id: 10, label: '校友信息' },
          { id: 10, label: '医疗卫生', children: [
            { id: 1, label: '学生医疗保健', children: [
              { id: 1, label: '防疫注射' },
              { id: 1, label: '体检信息' },
              { id: 1, label: '体检明细' },
              { id: 1, label: '体检项目' }
            ] },
            { id: 1, label: '教职工医疗保健', children: [
              { id: 1, label: '就医诊断' },
              { id: 1, label: '体检信息' },
              { id: 1, label: '体检明细' },
              { id: 1, label: '体检项目' }
            ] }
          ] }
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
  watch: {
    filterText(val) {
      this.$refs.tree.filter(val)
    }
  },
  mounted() {
    // this.initJkChart()
  },
  methods: {
    initJkChart() {
      console.log(this.$refs.jkPopChart)
      this.jkPopChart = echarts.init(this.$refs.jkPopChart)
      this.jkPopChart.setOption(this.jkOptions)
    },
    showDia() {
      this.dialogFormVisible = !this.dialogFormVisible
      if (this.dialogFormVisible) {
        this.$nextTick(() => {
          this.initJkChart()
        })
      }
    },
    filterNode(value, data) {
      if (!value) return true
      return data.label.indexOf(value) !== -1
    },

    wFilterTableData(val) {
      this.multipleSelection = val
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
}
.jk-pop{
  width:600px;
  height:400px;
}
</style>
