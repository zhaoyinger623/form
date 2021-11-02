<template>
    <div class="modular-con01" :id="anchorId">
        <div class="sml-tit01">{{title}}</div>
        <div class="modular-box01">
            <div class="m-top01">
                <h5 class="top-tit01">项目名称：{{projectName}}</h5>
                <p class="top-info01">
                    <span>项目编号：{{id}}</span>
                    <span class="line01">｜</span>
                    <span>地市：{{address}}</span>
                    <span class="line01">｜</span>
                    <span>建设类型：{{type}}</span>
                </p>
            </div>
            <slot></slot>
        </div>
    </div>
</template>

<script>

export default {
  name: 'Plane',
  props: {
    title: {
      type: String,
      default: ''
    },
    projectName: {
      type: String,
      default: '厦门ICT大单导入'
    },
    id: {
      type: Number,
      default: 123456789
    },
    address: {
      type: String,
      default: '福州'
    },
    type: {
      type: String,
      default: '省管市建'
    },
    anchorId: {
      type: String,
      default: ''
    }
  }
}
</script>

<style scoped>

</style>