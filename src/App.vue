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
    padding: 20px;
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
    .double-columns {
      min-width: 300px;
      .column-right{
        .el-textarea{
          &.min-h140{
            .el-textarea__inner{
              min-height: 140px !important;
            }
          }
          &.w-200{
            width: 200px;
          }
        }
      }
      .form-item__label{
        float: none;
      }
      .el-form{
        padding-right: 0;
      }

    }
  }
  .double-columns {
    min-width: 920px;
    overflow-x: auto;
    &:after {
      content: "";
      font-size: 0;
      display: block;
      height: 0;
      clear: both;
      visibility: hidden;
    }
    .column-left {
      width: 20%;
      float: left;
      .el-form-item__label {
        float: none;
      }
      .el-form-item__content {
        margin-left: 0 !important;
      }
    }
    .column-right {
      width: 77%;
      float: left;
      margin-left: 20px;
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
  .txt-c{
    text-align: center;
    padding-top: 20px;
  }
  .common-title{
    font-size: 16px;
    padding-bottom: 20px;
    .el-icon-plus,
    .el-icon-minus{
      color: #67c23a;
      margin: 0 5px;
      cursor: pointer;
    }
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
  .el-pagination{
    padding: 20px 0;
  }
  .tem-rule-filter {
    height: 40px;
    margin-bottom: 20px;
    &:after {
      content: "";
      font-size: 0;
      display: block;
      height: 0;
      clear: both;
      visibility: hidden;
    }
    .el-form {
      float: left;
      width: 400px;
      .el-form-item {
        margin-bottom: 0;
      }
    }
    .tem-button {
      float: right;
    }
  }

  .m-filter-row{
    padding-bottom: 20px;
    .filter-label{
      min-width: 80px;
      font-size: 14px;
      line-height: 36px;
      &.w-140{
        width: 140px;
      }
    }
  }
  .m-buttons-row{
    padding-bottom: 20px;
  }
  .mr-20{
    margin-right: 20px;
  }
  .u-handle-icon{
    font-size: 18px;
    cursor: pointer;
    color: #1890ff;
    &:hover{
      color: #46a6ff;
    }
  }
  .el-button--medium.is-circle{
   &.mini-btn{
     padding: 4px;
   }
  }

</style>
