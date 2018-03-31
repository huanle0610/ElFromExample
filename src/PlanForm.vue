<template>
  <div class="subForm">
    <el-form-item
      :prop="path + '.name'"
      label="活动名称"
      :rules="{
      required: true, message: 'amtf不能为空', trigger: 'blur'
    }">
      <el-input v-model="form.name"></el-input>
    </el-form-item>
    <el-form-item
      label="特殊资源"
      :prop="path + '.resource'"
      :rules="{
      required: true, message: 'amtf不能为空', trigger: 'blur'
    }"
    >
      <el-radio-group v-model="form.resource">
        <el-radio label="线上品牌商赞助"></el-radio>
        <el-radio label="线下场地免费"></el-radio>
      </el-radio-group>
    </el-form-item>
    <el-form-item>
      <album-upload v-model="form.fileList" :path="path + '.fileList'"></album-upload>
    </el-form-item>
    <el-form-item
    :prop="path + '.calendar'"
    >
      <calendar v-model="form.calendar" :path="path + '.calendar'"></calendar>
    </el-form-item>
    <el-form-item
    label="活动形式"
    :prop="path + '.desc'"
      :rules="{
      required: true, message: 'amtf不能为空', trigger: 'blur'
    }"
    >
      <el-input type="textarea" v-model="form.desc"></el-input>
    </el-form-item>
  </div>
</template>

<script>
import planDataConstructor from './plan.js'
import AlbumUpload from './AlbumUpload'
import Calendar from './Calendar'
export default {
  components: {
    Calendar,
    AlbumUpload
  },
  model: {
    prop: 'form',
    event: 'change'
  },
  props: {
    path: {
      type: String
    },
    index: {
      type: Number
    },
    form: {
      type: Object,
      default: planDataConstructor()
    }
  }
}
</script>

<style scoped>
.el-form-item .subForm .el-form-item {
    margin-bottom: 22px;
}
</style>

