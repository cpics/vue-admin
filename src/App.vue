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
</style>
