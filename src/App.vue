<template>
  <el-row type="flex" class="row-bg" justify="center">
    <el-col :span="3"><div class="grid-content bg-purple"></div></el-col>
    <el-col :span="18"><i-form></i-form></el-col>
    <el-col :span="3"><div class="grid-content bg-purple"></div></el-col>
  </el-row>
</template>

<script>
import IForm from './Form'
export default {
  components: {
    IForm
  },
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style>
</style>
