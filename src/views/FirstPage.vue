<template>
  <div v-loading.fullscreen.lock="fullscreenLoading">
    <b-navbar toggleable="sm" type="light" variant="light" fixed="top">
    <b-navbar-brand href="#"><img src="https://en.gravatar.com/userimage/166672495/d485dfa59c424c88e29cea7ba6dc4390.jpg"
                                       class="d-inline-block align-top" alt="Kitten"
                                       style="width: 32px; height: 32px">
      <span style="margin-left: 5px">范希晨</span></b-navbar-brand>

    <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

    <b-collapse id="nav-collapse" is-nav>
      <b-navbar-nav>
<!--        <b-nav-item href="#p5">电话</b-nav-item>-->
<!--        <b-nav-item href="#p6">邮箱</b-nav-item>-->
        <b-nav-item  v-on:click="changePoint(1)">教育经历</b-nav-item>
        <b-nav-item  v-on:click="changePoint(4)">项目经验</b-nav-item>
        <b-nav-item  v-on:click="changePoint(2)">开发技能</b-nav-item>
        <b-nav-item  v-on:click="changePoint(3)">工作经历</b-nav-item>
        <b-nav-item  v-on:click="changePoint(3)">联系方式</b-nav-item>
      </b-navbar-nav>
    </b-collapse>
  </b-navbar>
    <div class="content" style="margin-top: -5px">
  <!--    <div>-->
  <!--    </div>-->
      <el-row>
        <el-col>
          <el-container>
  <!--          <el-header>-->
  <!--             </el-header>-->
            <el-main style="margin-top: -10px">
              <p class="subTitle" style="margin-bottom: -8px" id="p1">教育经历</p>
              <div v-for="item in educationData" v-bind:key="item.id" style="margin-top: 15px">
                  <el-row>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"><span class="schoolName">{{item.name}}</span></el-col>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"> <span>{{item.date}}</span></el-col>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"><span>{{item.major}}</span></el-col>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"><li class="schoolOtherInfo" style="margin-top: 5px">{{item.otherInfo}}</li></el-col>
                </el-row>
              </div>
              <el-divider></el-divider>
              <p class="subTitle" style="margin-bottom: -8px" id="p4">项目经验</p>
              <div v-for="(item) in projectData" v-bind:key="item.id" style="margin-top: 15px">
                <el-row>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"><span class="schoolName">{{item.name}}</span></el-col>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"> <span>{{item.date}}</span></el-col>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"><span>{{item.position}}</span></el-col>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"><li v-for = "(item1, index) in item.workContent" v-bind:key="index" style="line-height: 30px">{{item1}} </li></el-col>
                </el-row>
              </div>
              <el-divider></el-divider>
              <div>
                <p class="subTitle" id="p2">开发技能</p>
                  <li v-for="item in skillData" v-bind:key="item.id" style="line-height: 30px">{{item.name}}</li>
                <el-divider></el-divider>
              </div>
              <p class="subTitle" style="margin-bottom: -8px" id="p3">工作经历</p>
              <div v-for="item in companyData" v-bind:key="item.id" style="margin-top: 15px">
                <el-row>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"><span class="schoolName">{{item.name}}</span></el-col>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"> <span>{{item.date}}</span></el-col>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"><span>{{item.position}}</span></el-col>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"><li style="margin-top: 5px">{{item.workContent}}</li></el-col>
                </el-row>
              </div>
              <el-divider></el-divider>
              <p class="subTitle" style="margin-bottom: -8px">英语水平</p>
              <div style="margin-top: 15px">
                <el-row>
                  <el-col :xs="24" :sm="24" :md="24" :lg="24"><span >IELTS: 6</span></el-col>
                </el-row>
              </div>
            </el-main>
            <el-footer>
              <p style="font-size: 14px; text-align: center" id="p5"> 电话:15602321825 </p>
              <p style="font-size: 14px; text-align: center" id="p6"> 邮件:2568681147@qq.com</p>
            </el-footer>
          </el-container>
        </el-col>
      </el-row>
    </div>
</div>
</template>

<script>
import https from '../http'
export default {
  name: 'Index',
  data () {
    return {
      projectData: [],
      skillData: [],
      educationData: [],
      companyData: [],
      fullscreenLoading: false
    }
  },
  mounted () {
    this.fullscreenLoading = true
    this.getData()
  },
  methods: {
    getData: function () {
      https.fetchGet('/allData').then((data) => {
        this.projectData = data.data[0].project
        this.educationData = data.data[0].education
        this.skillData = data.data[0].skill
        this.companyData = data.data[0].company
        this.fullscreenLoading = false
      })
    },
    changePoint: function (item) {
      if (item === 1) {
        window.scrollTo(0, 0)
      } else if (item === 2) {
        window.scrollTo(0, 890)
      } else if (item === 3) {
        window.scrollTo(0, 1300)
      } else if (item === 4) {
        window.scrollTo(0, 330)
      }
    }
  }
}

// style="background: rgb(249, 250, 252)"
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
  .subTitle {
    font-weight:bold;
    color:black;
    text-decoration:underline
  }
  .schoolName {
    font-weight:bold;
    color: #000;
  }
  .schoolOtherInfo {
    color: gray;
  }
  span {
    line-height: 30px;
  }
</style>
