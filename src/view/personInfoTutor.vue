<style scoped>
  .chartTitle{
    border-bottom: 2px solid #E6E9ED;
    padding: 1px 17px 6px;
    margin-bottom: 10px;
    font-size: 18px;
    font-weight: 400;
    margin-top: 10px;
    color: grey;
  }
  .chartCollapse{
    text-align: center;
  }
  .fade-enter-active {
    transition: all .5s ease;
  }
  .fade-leave-active {
    transition: all .1s cubic-bezier(1.0, 0.5, 0.8, 1.0);
  }
  .fade-enter{
    transform: translateX(20px);
  }
  .fade-leave-to{
    transform: translateX(20px);
  }
</style>
<template>
  <div>
    <headDataShowPublic
      :getNumUrl="'json/Teacher_teacherInfo_teacherCount.json?typeName='"
      :orderText="orderText"
      part="4"></headDataShowPublic>
    <div class="layout-content">
      <div class="layout-content-main">
        <p class="chartTitle">基本信息</p>
        <Row type="flex" class="code-row-bg">
          <Col span="12" class="Pshadow">
          <!--人员信息：教师图表1column-->
          <chartx3 id="persontutor1_column"
                   :option="persontutor1_column"
                   :getchartUrl="persontutor1_column_url"
                   :chartTitleClass="'chatTitle_blue'"
                   :ctitle="ctitle.personTutorTitle1"></chartx3>
          </Col>
          <Col span="12" class="Pshadow">
          <chartx3 id="persontutor2_column"
                   :option="persontutor2_column"
                   :getchartUrl="persontutor2_column_url"
                   :chartTitleClass="'chatTitle_blue'"
                   :ctitle="ctitle.personTutorTitle2"></chartx3>
          </Col>
        </Row>
        <transition name="fade">
          <Row type="flex" class="code-row-bg" v-show="rstu.isshow">
            <!--学生图表4column-->
            <Col span="8" class="Pshadow">

            </Col>
          </Row>
        </transition>
        <Button large
                @click="fold(rstu)"
                class="longButton">
          {{rstu.text}}
        </Button>
        <!--<p class="chartTitle"style="margin-top:30px;">教职工信息</p>
        <Row type="flex"  class="code-row-bg">
          <Col span="8" class="Pshadow">

          </Col>
          <Col span="8" class="Pshadow">

          </Col>
          <Col span="8" class="Pshadow">

          </Col>
        </Row>
        <transition name="fade">
          <Row type="flex"  class="code-row-bg" v-show="rtutor.isshow">
            <Col span="8" class="Pshadow">

            </Col>
          </Row>
        </transition>
        <Button large
                @click="fold(rtutor)"
                class="longButton">
          {{rtutor.text}}
        </Button>-->
      </div>
    </div>
  </div>
</template>

<script>
  import headDataShowPublic from "../components/headDataShowPublic.vue"//头部数字组件
  import options from "../config/highcharts.config.js"//表格基本配置
  import chartx3 from "../components/chartx3.vue"//Highcharts基本架子
  export default {
    name:"personInfoTutor",
    data: function () {
      return {
        "rstu":{"text":"查看更多","isshow":true},
        "rtutor":{"text":"查看更多","isshow":true},
        //表头的数字块
        "orderText":[{Key:"zbjzg",Text:"教职工总人数"},{Key:"gjjj",Text:"高级教师数"},{Key:"xs",Text:"学士人数"},{Key:"yjs",Text:"研究生人数"},{Key:"ss",Text:"硕（博）士人数"}],
        "ctitle":options.ctitle,//图表的标题
        //图标基本数据
        "persontutor1_column":this.utils.deepCopy(options.column),
        "persontutor2_column":this.utils.deepCopy(options.column),
        //图表获取数据的路径
        "persontutor1_column_url":window.getHost+"json/Teacher_teacherInfo_teacherZGXLCount.json?typeName="+this.$route.name[1],
        "persontutor2_column_url":window.getHost+"json/Teacher_teacherInfo_teacherZGXWCount.json?typeName="+this.$route.name[1],
      }
    },
    methods:{
      "fold":function(now){
        now.text=now.isshow?'查看更多':'收起';
        now.isshow=!now.isshow;
      }
    },
    mounted:function(){
      this.rstu.isshow=false;
      this.rtutor.isshow=false;
    },
    components:{
      chartx3:chartx3,
      headDataShowPublic:headDataShowPublic
    }
  }
</script>
