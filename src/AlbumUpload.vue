<template>
  <div>
    <el-form-item
      :prop="path"
      :rules="{
      required: true, type: 'array', min: 1, message: 'file不能为空', trigger: 'blur'
      }">
      <el-upload
        class="upload-demo"
        action="https://jsonplaceholder.typicode.com/posts/"
        :on-preview="handlePreview"
        :on-remove="handleRemove"
        :before-remove="beforeRemove"
        :limit="1"
        :on-change="handleChange"
        :on-exceed="handleExceed"
        :file-list="fileList">
        <el-button size="small" type="primary">点击上传</el-button>
        <div slot="tip" class="el-upload__tip">只能上传jpg/png文件，且不超过500kb</div>
      </el-upload>
    </el-form-item>

     <el-form-item
      :prop="`${path}.${index}.cover`"
      v-for="(file, index) in fileList"
      :key="index"
      :rules="[
        { required: true, min: 1, message: 'please select a picture as cover', trigger: 'blur' }
      ]"
    >
      <el-input v-model="file.cover" placeholder="please select a picture as cover" />
    </el-form-item>
  </div>
</template>

<script>
export default {
  model: {
    prop: 'fileList',
    event: 'change'
  },
  props:{
    fileList: {
      type: Array,
      default: []
    },
    path: {
      type: String
    }
  },
  methods: {
    handleRemove(file, fileList) {
      console.log(this.fileList.filter(v => v.name === file.name))
      // this.$emit('change', this.fileList.filter(v => v.name !== file.name))
      this.$emit('change', [])
    },
    handlePreview(file) {
      console.log(file);
    },
    handleChange(file, fileList) {
      this.$emit('change', fileList.slice(-1))
    },
    handleExceed(files, fileList) {
      this.$message.warning(
        `当前限制选择 1 个文件，本次选择了 ${
          files.length
        } 个文件，共选择了 ${files.length + fileList.length} 个文件`
      );
    },
    beforeRemove(file, fileList) {
      return this.$confirm(`确定移除 ${file.name}？`);
    }
  }
};
</script>

<style scoped>

</style>
