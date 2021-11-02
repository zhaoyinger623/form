<template>
  <el-form ref="elForm" :model="formData" size="medium" label-width="100px">
    <div style="margin: 0 15px">
      <div class="m-modular01">
        <div class="modular-tit01">
          <h5>填写周报</h5>
          <span>({{ projectWeeklyDetailData.title }})</span>
        </div>
        <div class="m-nav01" ref="mNav">
          <div
            class="nav-wrap"
            ref="navWrap"
            :class="navFixShow ? 'navFix' : ''"
          >
            <ul class="clearfix">
              <li><a class="active" href="#modular-zx">专线</a></li>
              <li><a href="#modular-ict">ICT</a></li>
              <li><a href="#modular-yw">云网</a></li>
              <li><a href="#modular-5g">5G</a></li>
            </ul>
          </div>
        </div>
        <div class="modular-con01" id="modular-zx">
          <div class="sml-tit01">专线</div>
          <div class="modular-box01">
            <div v-for="(item, index) in projectWeeklyDetailData.specialLine">
              <div class="m-top01">
                <h5 class="top-tit01">项目名称:{{ item.projectName }}</h5>
                <p class="top-info01">
                  <span>项目编号:{{ item.projectCode }}</span>
                  <span class="line01">｜</span>
                  <span>地市:{{ item.areaName }}</span>
                  <span class="line01">｜</span>
                  <span
                    >建设类型:{{
                      item.buildType === 1 ? "省管市建" : "市管市建"
                    }}</span
                  >
                </p>
              </div>
              <div style="height: 300px">
                <el-form-item label="项目状态" prop="businessType">
                  <el-radio-group v-model="item.businessType" size="medium">
                    <el-radio
                      v-for="(item2, index2) in projectStatusOptions"
                      :key="index2"
                      :label="item2.value"
                    >
                      {{ item2.label }}
                    </el-radio>
                  </el-radio-group>
                </el-form-item>
                <el-form-item label="进展情况:">
                  <el-input
                    v-model="item.progress"
                    type="textarea"
                    :autosize="{ minRows: 4, maxRows: 4 }"
                    :style="{ width: '100%' }"
                  ></el-input>
                </el-form-item>
                <el-form-item label="需协调问题:">
                  <el-input
                    v-model="item.needHelp"
                    type="textarea"
                    :autosize="{ minRows: 4, maxRows: 4 }"
                    :style="{ width: '100%' }"
                  ></el-input>
                </el-form-item>
              </div>
            </div>
          </div>
        </div>
        <div class="modular-con01" id="modular-ict">
          <div class="sml-tit01">ICT</div>
          <div class="modular-box01">
            <div class="m-top01">
              <h5 class="top-tit01">项目名称：厦门ICT大单导入</h5>
              <p class="top-info01">
                <span>项目编号：123456789</span>
                <span class="line01">｜</span>
                <span>地市：福州</span>
                <span class="line01">｜</span>
                <span>建设类型：省管市建</span>
              </p>
            </div>
            <div style="height: 300px"></div>
          </div>
        </div>
        <div class="modular-con01" id="modular-yw">
          <div class="sml-tit01">云网</div>
          <div class="modular-box01">
            <div class="m-top01">
              <h5 class="top-tit01">项目名称：厦门ICT大单导入</h5>
              <p class="top-info01">
                <span>项目编号：123456789</span>
                <span class="line01">｜</span>
                <span>地市：福州</span>
                <span class="line01">｜</span>
                <span>建设类型：省管市建</span>
              </p>
            </div>
            <div style="height: 300px"></div>
          </div>
        </div>
        <div class="modular-con01" id="modular-5g">
          <div class="sml-tit01">5G</div>
          <div class="modular-box01">
            <div class="m-top01">
              <h5 class="top-tit01">项目名称：厦门ICT大单导入</h5>
              <p class="top-info01">
                <span>项目编号：123456789</span>
                <span class="line01">｜</span>
                <span>地市：福州</span>
                <span class="line01">｜</span>
                <span>建设类型：省管市建</span>
              </p>
            </div>
            <div style="height: 300px"></div>
          </div>
        </div>
      </div>
      <!--      <el-button type="primary" @click="editAll(1)">保存草稿</el-button>
      <el-button type="primary" @click="editAll(2)">提交</el-button>-->
    </div>
  </el-form>
</template>

<script>
import {
  list,
  exportData,
  saveRecordDetailApi,
} from "@/api/scdd/large-amount-project/weekly";

export default {
  props: ["recordInfo"],
  data() {
    return {
      navFixShow: false,
      projectStatusOptions: [
        {
          label: "正常推进",
          value: 0,
        },
        {
          label: "存在延期风险",
          value: 1,
        },
        {
          label: "已延期",
          value: 2,
        },
        {
          label: "已交付",
          value: 3,
        },
      ],
      zxData: [],
      fiveGData: [],
      ictData: [],
      ywData: [],
      formData: [],
      projectWeeklyDetailData: {
        recordId: null,
        title: "2021年大单项目管控周报20211021",
        status: null,
        specialLine: [
          {
            detailId: 1,
            recordId: 2,
            bpId: 3,
            buildType: 1,
            businessType: 1,
            projectName: "测试",
            areaName: "福州",
            projectCode: "1111",
            progress: "dddd",
            projectStatus: "e345",
            needHelp: "2233",
          },
          {
            detailId: 1,
            recordId: 2,
            bpId: 3,
            buildType: 1,
            businessType: 1,
            projectName: "测试",
            areaName: "福州",
            projectCode: "1111",
            progress: "dddd",
            projectStatus: "e345",
            needHelp: "2233",
          },
        ],
        ict: [],
        five_5g: [],
        cloudNetwork: [],
      },
    };
  },
  created() {
    var that = this;
  },
  mounted() {
    this.navScropll();
  },
  methods: {
    editAll(value) {
      var that = this;
      this.formData.map((i, index) => {
        debugger;
        console.log("i");
      });
    },
    navScropll() {
      debugger;
      const navHeight = this.$refs.mNav.offsetTop;
      window.addEventListener("scroll", function () {
        debugger;
        if (window.scrollTop() > navHeight) {
          this.navFixShow = true;
        } else {
          this.navFixShow = false;
        }
      });
    },
  },
};
</script>

<style lang="scss" scoped>
.before {
  content: "";
  width: 3px;
  height: 17px;
  background: #3eb4fa;
  position: absolute;
  left: 10px;
}

.detail {
  font-size: 15px;
  padding-left: 20px;
  color: #666666;
}
</style>

<style src="../../../../styles/bigprojectweekly/css/base.css" scoped></style>
