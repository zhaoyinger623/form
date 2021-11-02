<template>
    <el-form :model="formData" :rules="formRules" ref="form" class="form" label-width="100px">
        <el-form-item label="项目状态" prop="projectType">
            <el-radio-group v-model="formData.projectType">
                <el-radio label="doing">正常推进</el-radio>
                <el-radio label="risk">存在延期风险</el-radio>
                <el-radio label="delay">已延期</el-radio>
                <el-radio label="done">已交付</el-radio>
            </el-radio-group>
        </el-form-item>
        <el-form-item label="进展情况" prop="process">
            <el-input type="textarea" v-model="formData.process"></el-input>
        </el-form-item>
        <el-form-item label="需协调问题" prop="problem">
            <el-input type="textarea" v-model="formData.problem"></el-input>
        </el-form-item>
    </el-form>
</template>

<script>

export default {
  name: 'SpecialForm',
  data() {
    return {
      formData: {
        projectType: '',
        process: '',
        problem: ''
      },
      formRules: {
        projectType: [
          {required: true, message: '请选择项目状态', trigger: 'change'},
        ],
        process: [
          {required: true, message: '请填写活动形式', trigger: 'change'}
        ]
      }
    }
  },
}
</script>

<style scoped>

</style>