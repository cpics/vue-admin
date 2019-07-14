<template>
  <div class="g-container">
    <div class="double-columns">
      <div class="column-left">
        <div class="border-box">
          <div class="common-title">发件箱配置信息</div>
          <el-form
            ref="form"
            :model="form"
            label-width="80px"
          >
            <el-form-item label="SMTP服务器">
              <el-input v-model="form.name" />
            </el-form-item>
            <el-form-item label="SMTP端口">
              <el-input v-model="form.name" />
            </el-form-item>
            <el-form-item label="发件箱地址">
              <el-input v-model="form.name" />
            </el-form-item>
            <el-form-item label="发件箱密码">
              <el-input v-model="form.name" />
            </el-form-item>
            <el-form-item label="是否启用">
              <el-switch
                v-model="value1"
                style="display: block"
                active-text="YES"
                inactive-text="NO"
              />
            </el-form-item>
            <el-form-item class="txt-c">
              <el-button
                type="primary"
                @click="onSubmit"
              >保 存</el-button>
            </el-form-item>
          </el-form>
          <el-alert
            title="注：“YES”启用邮件功能；“NO”停用邮件功能"
            type="error"
            :closable="false"
          />
        </div>
      </div>
      <div class="column-right">
        <div class="border-box">
          <div class="common-title">指定接收人群</div>
          <div class="m-buttons-row">
            <el-button icon="el-icon-plus" type="primary" @click="dialogFormVisible = true">添加</el-button>
            <el-button
              icon="el-icon-message"
              type="warning"
              @click="sendEmail"
            >发送邮件</el-button>
            <el-button
              icon="el-icon-chat-round"
              type="success"
              @click="sendWx"
            >微信推送</el-button>
            <el-button icon="el-icon-delete" type="danger" @click="del">删除</el-button>
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
              label="用户"
            />
            <el-table-column
              prop="send"
              label="发送类型"
            />
            <el-table-column
              prop="remind"
              label="业务类型"
            />
            <el-table-column
              fixed="right"
              label="操作"
              width="100"
            >
              <template>
                <el-button class="mini-btn" type="primary" icon="el-icon-edit" circle title="编辑" @click="dialogFormVisible = true" />
              </template>
            </el-table-column>
          </el-table>
        </div>
        <div class="border-box">
          <div class="common-title">应用质量反馈</div>
          <div class="more-button txt-c">
            <el-button type="warning" @click="sendEmail">发送邮件</el-button>
          </div>
        </div>
      </div>
    </div>
    <el-dialog title="添加接收人群" :visible.sync="dialogFormVisible">
      <el-form :model="form">
        <el-form-item label="用户" :label-width="formLabelWidth">
          <el-input v-model="form.name" class="w-200" autocomplete="off" />
        </el-form-item>
        <el-form-item label="发送类型" :label-width="formLabelWidth">
          <el-select v-model="form.region" placeholder="请选择">
            <el-option label="质量报告" value="shanghai" />
            <el-option label="质量报告" value="beijing" />
          </el-select>
        </el-form-item>
        <el-form-item label="业务类型" :label-width="formLabelWidth">
          <el-select v-model="form.region" placeholder="请选择">
            <el-option label="GXJX教学管理数据" value="shanghai" />
            <el-option label="GXJX教学管理数据" value="beijing" />
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
export default {
  data() {
    return {
      dialogFormVisible: false,
      formLabelWidth: '120px',
      multipleSelection: [],
      value1: true,
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
      tableData: [{
        id: 0,
        user: 'admin',
        send: '质量报告',
        remind: 'GXJX 教学管理数据'
      }, {
        id: 1,
        user: 'admin',
        send: '质量报告',
        remind: 'GXJX 教学管理数据'
      }, {
        id: 2,
        user: 'admin',
        send: '质量报告',
        remind: 'GXJX 教学管理数据'
      }, {
        id: 3,
        user: 'admin',
        send: '质量报告',
        remind: 'GXJX 教学管理数据'
      }, {
        id: 4,
        user: 'admin',
        send: '质量报告',
        remind: 'GXJX 教学管理数据'
      }, {
        id: 5,
        user: 'admin',
        send: '质量报告',
        remind: 'GXJX 教学管理数据'
      }]

    }
  },
  methods: {
    handleSelectionChange(val) {
      this.multipleSelection = val
    },
    del() {
      if (this.multipleSelection.length == 0) {
        this.$message({
          message: '请勾选你需要删除的数据',
          type: 'warning'
        })
      } else {
        console.log(1)
        this.multipleSelection.forEach(item => {
          this.tableData.forEach((d, i) => {
            if (item.id == d.id) {
              this.tableData.splice(i, 1)
            }
          })
        })
      }
    },
    onSubmit() {
      this.$message({
        message: '保存成功',
        type: 'success'
      })
    },
    sendEmail() {
      this.$message({
        message: '邮件发送成功',
        type: 'success'
      })
    },
    sendWx() {
      this.$message({
        message: '微信推送成功',
        type: 'success'
      })
    }
  }
}
</script>

<style scoped="scoped" lang="scss">
</style>
