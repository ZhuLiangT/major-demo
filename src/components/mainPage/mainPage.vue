<template>
    <div class="mainPage">
      <div class="layout" :class="{'layout-hide-text': spanLeft < 4}">
        <Row type="flex">
          <i-col :span="spanLeft" class="layout-menu-left">
            <Menu active-name="1" theme="dark" width="auto">
              <div class="layout-logo-left"></div>
              <Menu-item name="1"  :class="{'centerClass': spanLeft < 4}"  @click.native="menuitem = menu[0]">
                <Icon class="animateClass1" type="ios-navigate" :size="iconSize"></Icon>
                <span class="layout-text">选项 1</span>
              </Menu-item>
              <Menu-item name="2"  :class="{'centerClass': spanLeft < 4}"   @click.native="menuitem = menu[1]">
                <Icon class="animateClass1" type="ios-keypad" :size="iconSize"></Icon>
                <span class="layout-text">选项 2</span>
              </Menu-item>
              <Menu-item name="3"  :class="{'centerClass': spanLeft < 4}"  @click.native="menuitem = menu[2]">
                <Icon class="animateClass1" type="ios-analytics" :size="iconSize"></Icon>
                <span class="layout-text">选项 3</span>
              </Menu-item>
            </Menu>
          </i-col>
          <i-col :span="spanRight">
            <div class="layout-header">
              <i-button type="text" @click="toggleClick">
                <Icon type="navicon" size="32"></Icon>
              </i-button>
              <Menu mode="horizontal" active-name="1">
                <div class="layout-assistant">
                  <Menu-item :name="index" v-for="(item,index) in menuitem"><router-link :to="item.link">{{item.name}}</router-link></Menu-item>
                </div>
              </Menu>
            </div>
            <!--<div class="layout-breadcrumb">
              <Breadcrumb>
                <Breadcrumb-item href="#">首页</Breadcrumb-item>
                <Breadcrumb-item href="#">应用中心</Breadcrumb-item>
                <Breadcrumb-item>某应用</Breadcrumb-item>
              </Breadcrumb>
            </div>-->
            <div class="layout-content">
              <router-view class="layout-content-main"></router-view>
             <!-- <div class="layout-content-main">内容区域</div>-->
            </div>
          </i-col>
        </Row>
      </div>
    </div>
</template>

<script>
import './mainPage.scss'
    export default{
        data(){
            return {
              spanLeft: 4,
              spanRight: 20,
              menu:[
                  [{name:'部门管理',link:'/departentManage'},{name:'课程模块管理',link:'/courseModule'},{name:'课程技能树',link:'/foo'}],
                  [{name:'课程库管理',link:'/courselibrarymanage'},{name:'专业管理',link:'/majormanage'},{name:'教师管理',link:'/teachermanage'}],
                  [{name:'专业培养方案',link:'/traningmainPage'}],
              ],
              menuitem:null,
            }
        },
        computed: {
          iconSize () {
            return this.spanLeft === 4 ? 14 : 24;
          }
        },
        components: {},
        created(){
            this.menuitem = this.menu[0]
        },
        mounted(){
        },
        methods: {
          toggleClick () {
            if (this.spanLeft === 4) {
              this.spanLeft = 2;
              this.spanRight = 22;
            } else {
              this.spanLeft = 4;
              this.spanRight = 20;
            }
          },
          push(val){
            this.$router.push({ path: val})
            return;
          }
        }
    }
</script>
