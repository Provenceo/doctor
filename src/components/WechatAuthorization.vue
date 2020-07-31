<template>
  <div>{{ parmas.code }}</div>
</template>

<script>
import { oauth } from "@/apis/login";
export default {
  data() {
    return {
      parmas: {
        code: "",
        ty: 1
      }
    };
  },

  /* var local = window.location.href; // 获取页面url
var appid = "wx0c5fe766d97cd585";
 window.location.href = `https://open.weixin.qq.com/connect/oauth2/authorize?appid=${appid}&redirect_uri=${encodeURIComponent(
          local
        )}&response_type=code&scope=snsapi_userinfo&state=123#wechat_redirect`; */

  methods: {
    getCode() {
      // 非静默授权，第一次有弹框
      this.parmas.code = "";
      var local = window.location.href; // 获取页面url
      var appid = "wx0c5fe766d97cd585";
      this.parmas.code = this.getUrlCode().code; // 截取code
      // alert(JSON.stringify(this.parmas.code));
      if (this.parmas.code == null || this.parmas.code === "") {
        // 如果没有code，则去请求
        window.location.replace(
          `https://open.weixin.qq.com/connect/oauth2/authorize?appid=${appid}&redirect_uri=${encodeURIComponent(
            local
          )}&response_type=code&scope=snsapi_userinfo&state=123#wechat_redirect`
        );
      } else {
        // 你自己的业务逻辑
        this.parmas.code = this.getUrlCode().code;
        // window.location.replace(
        //   `https://open.weixin.qq.com/connect/oauth2/authorize?appid=${appid}&redirect_uri=${encodeURIComponent(
        //     local
        //   )}&response_type=code&scope=snsapi_userinfo&state=123#wechat_redirect`
        // );
      }
    },
    getUrlCode() {
      // 截取url中的code方法
      var url = location.search;
      this.winUrl = url;
      var theRequest = new Object();
      if (url.indexOf("?") != -1) {
        var str = url.substr(1);
        var strs = str.split("&");
        for (var i = 0; i < strs.length; i++) {
          theRequest[strs[i].split("=")[0]] = strs[i].split("=")[1];
        }
      }
      return theRequest;
    }
  },

  mounted() {
    this.getCode();
  }
};
</script>

<style lang="less"></style>
