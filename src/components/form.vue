<template>
    <el-form :model="specialForm" :rules="specialFormRules" ref="specialForm" class="form" label-width="100px">
        <el-form-item label="项目状态" prop="projectType">
            <el-radio-group v-model="specialForm.projectType">
                <el-radio label="doing">正常推进</el-radio>
                <el-radio label="risk">存在延期风险</el-radio>
                <el-radio label="delay">已延期</el-radio>
                <el-radio label="done">已交付</el-radio>
            </el-radio-group>
        </el-form-item>
        <el-form-item label="进展情况" prop="process">
            <el-input type="textarea" v-model="specialForm.process"></el-input>
        </el-form-item>
        <el-form-item label="需协调问题" prop="problem">
            <el-input type="textarea" v-model="specialForm.problem"></el-input>
        </el-form-item>
    </el-form>
</template>

<script>

export default {
  name: 'SpecialForm',
  data() {
    return {
      specialForm: {
        projectType: '',
        process: '',
        problem: ''
      },
      specialFormRules: {
        projectType: [
          {required: true, message: '请选择项目状态', trigger: 'blur'},
        ],
        process: [
          {required: true, message: '请填写活动形式', trigger: 'blur'}
        ]
      }
    }
  },
  props: {
    value: {
      type: Object,
      default: () => {}
    }
  },
  watch: {
    specialForm: {
      handler: function (newVal) {
        console.log(newVal)
        this.$emit('update:value', newVal)
      },
      deep: true
    }
  }

}
</script>

<style scoped>

</style>