<template>
  <div id="app">
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App'
}
</script>
<style lang="scss">
  .g-container{
    padding: 30px;
  }
  .el-dialog {
    .el-form {
      padding-right: 40px;
      max-height: 500px;
      overflow-y: auto;
      .el-input {
        &.w-200 {
          width: 200px;
        }
      }
      .el-date-editor.el-input,
      .el-date-editor.el-input__inner,
      .el-select {
        &.w-full {
          width: 100%;
        }
      }
    }
    .form-button{
      text-align: right;
      padding-right: 40px;
    }
    .el-table{
      &::before{
        height: 0;
      }
    }
  }
  .double-columns {
    &:after {
      content: "";
      font-size: 0;
      display: block;
      height: 0;
      clear: both;
      visibility: hidden;
    }
    .column-left {
      width: 300px;
      float: left;
      .el-form-item__label {
        float: none;
      }
      .el-form-item__content {
        margin-left: 0 !important;
      }
    }
    .column-right {
      margin-left: 340px;
    }
    .more-button {
      margin-bottom: 20px;
      &.txt-c{
        text-align: center;
      }
    }
  }
  .column-left{
    .el-form-item__label{
      float: none;
    }
    .el-form-item__content{
      margin-left: 0 !important;
    }
  }
  .el-form-item{
    &.txt-c{
      text-align: center;
    }
  }
  .common-title{
    font-size: 16px;
    padding-bottom: 20px;
  }
  .border-box{
    padding: 20px;
    border-radius:5px;
    border: 1px solid #dcdfe6;
    margin-bottom: 20px;
  }
  .common-h1-tit{
    color: #333;
    font-size: 24px;
    font-weight: normal;
    margin: 0;
    padding: 10px 0;
  }
</style>
