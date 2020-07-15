<template>
  <div class="my">
    <div class="myinfo">
      <img :src="avator">
      <button class="login" @click="toLogin">点击登录</button>
    </div>
    <div class="tools">
      <div class="tool-item" @click="goTo(item.url)" v-for="(item, index) in listData" :key="index">
        <span class="iconfont" :class="[item.icon, 'icon']"></span>
        <span class="icon-title">{{item.title}}</span>
      </div>
    </div>
  </div>
</template>

<script>
  import {
    get,
    toLogin,
    login
  } from "../../utils";
  export default {
    onShow() {
      // 可以通过 wx.getSetting 先查询一下用户是否授权了 "scope.record" 这个 scope
      if (login()) {
        this.userInfo = login();
        console.log(this.userInfo);
        this.avator = this.userInfo.avatarUrl;
      }
    },
    created() {},
    mounted() {},
    data() {
      return {
        avator: "http://yanxuan.nosdn.127.net/8945ae63d940cc42406c3f67019c5cb6.png",
        allcheck: false,
        listData: [],
        Listids: [],
        userInfo: {},
        listData: [
          {
            title: "收藏",
            icon: "icon-shoucang",
            url: "/pages/collectlist/main"
          },
            {
            title: "相册",
            icon: "icon-unie64a",
            url: ""
          },
          {
            title: "联系方式",
            icon: "icon-youhuiquan",
            url: ""
          },
        ]
      };
    },
    components: {},
    methods: {
      goTo(url) {
        if (toLogin()) {
          wx.navigateTo({
            url: url
          });
        }
      },
      toLogin() {
        if (!this.userInfo.avatarUrl) {
          wx.navigateTo({
            url: "/pages/login/main"
          });
        }
      }
    },
    computed: {}
  };

</script>
<style lang='scss' scoped>
  @import "./style1";

</style>
