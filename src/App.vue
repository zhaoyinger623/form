<template>
  <div id="app">
    <div class="modular-tit01">
      <h5>填写周报</h5><span>（2021年大单项目管控周报20211021）</span>
    </div>
    <div class="m-nav01" ref="m-nav">
      <div :class="['nav-wrap', fixed?'navFix':'']">
        <ul class="menuList clearfix" @click="handleClickMenu">
          <li id="zx"><a class="active" href="#modular-zx">专线</a></li>
          <li id="ict"><a href="#modular-ict">ICT</a></li>
          <li id="yw"><a href="#modular-yw">云网</a></li>
          <li id="5g"><a href="#modular-5g">5G</a></li>
        </ul>
      </div>
    </div>
    <div class="form-container">
      <Plane title="专线" anchorId="modular-zx">
        <Form ref="specialForm"/>
      </Plane>
      <Plane title="ICT" anchorId="modular-ict">
        <Form ref="ictForm"/>
      </Plane>
      <Plane title="云网" anchorId="modular-yw">
        <Form ref="cloudForm"/>
      </Plane>
      <Plane title="5G" anchorId="modular-5g">
        <Form ref="netForm"/>
      </Plane>
    </div>
    <div class="operation-button">
      <el-button type="primary" size="medium" @click="handleSubmit">提交</el-button>
      <el-button size="medium">存草稿</el-button>
      <el-button size="medium">取消</el-button>
    </div>
  </div>
</template>

<script>
import Plane from '@/components/plane'
import Form from '@/components/form'
export default {
  name: 'App',
  components: {
    Plane,
    Form
  },
  data() {
    return {
      fixed: false
    }
  },
  mounted() {
    const navHeight = this.$refs['m-nav'].offsetTop
    window.addEventListener('scroll', () => {
      if (window.pageYOffset > navHeight) {
        this.fixed = true
      } else {
        this.fixed = false
      }
    })
  },
  methods: {
    handleClickMenu(e) {
      console.log(document.getElementsByClassName('menuList')[0].childNodes)
      document.getElementsByClassName('menuList')[0].childNodes.forEach(item => {
        item.firstChild.classList.remove('active')
      })
      e.srcElement.classList.add('active')
    },
    handleSubmit() {
      const specialForm = this.$refs.specialForm
      const ictForm = this.$refs.ictForm
      const cloudForm = this.$refs.cloudForm
      const netForm = this.$refs.netForm

      const p1=new Promise((resolve,reject)=>{
        specialForm.$refs.form.validate(valid=>{
          if(valid) {
            resolve()
          } else {
            reject()
          }
        })
      })
      const p2=new Promise((resolve,reject)=>{
        ictForm.$refs.form.validate(valid=>{
          if(valid) {
            resolve()
          } else {
            reject()
          }
        })
      })
      const p3=new Promise((resolve,reject)=>{
        cloudForm.$refs.form.validate(valid=>{
          if(valid) {
            resolve()
          } else {
            reject()
          }
        })
      })
      const p4=new Promise((resolve,reject)=>{
        netForm.$refs.form.validate(valid=>{
          if(valid) {
            resolve()
          } else {
            reject()
          }
        })
      })
      Promise.all([p1,p2,p3,p4]).then(()=>{
        const data = {
          specialForm: specialForm.formData,
          ictForm: ictForm.formData,
          cloudForm: cloudForm.formData,
          netForm: netForm.formData
        }
        console.log(data)
      })
    }
  }

}
</script>

<style>
#app {
  background: #fff;
  margin: 16px 15px 0;
  border-radius: 2px;
}
</style>
