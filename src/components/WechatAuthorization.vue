<template>
  <div></div>
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
  methods: {
    getCode() {
      // 非静默授权，第一次有弹框
      this.parmas.code = "";
      var local = window.location.href; // 获取页面url
      var appid = "wx0c5fe766d97cd585";
      this.parmas.code = this.getUrlCode("code"); // 截取code
      if (this.parmas.code == null || this.parmas.code === "") {
        // 如果没有code，则去请求
        window.location.replace(
          `https://open.weixin.qq.com/connect/oauth2/authorize?appid=${appid}&redirect_uri=${encodeURIComponent(
            local
          )}&response_type=code&scope=snsapi_userinfo&state=123#wechat_redirect`
        );
      } else {
        // 你自己的业务逻辑
        this.parmas.code = this.getUrlCode("code");
      }
    },

    getUrlCode(name) {
      var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
      var r = window.location.search.substr(1).match(reg);
      if (r != null) return unescape(r[2]);
      return null;
    }
  },
  watch: {
    "parmas.code": {
      handler(newName, oldName) {
        if (newName) {
          oauth({ code: newName, ty: 1 })
            .then(res => {
              if (res.data.hasOwnProperty(token)) {
                sessionStorage.setItem("token", res.data.token);
                window.location.href =
                  window.location.origin + window.location.pathname;
              } else {
                window.location.href =
                  window.location.origin + window.location.pathname + "#/login";
              }
            })
            .catch(err => {
              if (err.codes == 404) {
                console.log(window.location.origin, window.location.pathname);
                window.location.href =
                  window.location.origin + window.location.pathname + "#/login";
              }
              // this.$toast(err);
            });
        }
      },
      immediate: true,
      deep: true
    }
  },
  mounted() {
    this.getCode();
  }
};
</script>

<style lang="less"></style>
