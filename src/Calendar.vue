<template>
    <div>
    <el-form-item
      :prop="path + '.y'"
      label="Year"
      :rules="{
      required: true, message: 'amtf不能为空', trigger: 'blur'
    }">
      <el-input v-model="calendar.y"></el-input>
    </el-form-item>
        <el-form-item
      :prop="path + '.m'"
      label="Month"
      :rules="{
      required: true, message: 'amtf不能为空', trigger: 'blur'
    }">
      <el-input v-model="calendar.m"></el-input>
    </el-form-item>
        <el-form-item
      :prop="path + '.d'"
      label="Day"
      :rules="{
      required: true, message: 'amtf不能为空', trigger: 'blur'
    }">
      <el-input v-model="calendar.d"></el-input>
    </el-form-item>
    </div>
</template>

<script>
export default {
  model: {
    prop: 'calendar',
    event: 'change'
  },
  props: {
    path: {
      type: String
    },
    calendar: {
      type: Object
    }
  }
}
</script>
