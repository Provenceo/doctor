<template>
  <div id="doctor_login">
    <div class="herder">
      <img src="@/assets/images/doctor_login.png" alt="" />
    </div>
    <div class="main">
      <div class="welcome">
        欢迎您！主管医生
      </div>
      <div class="info">
        请输入您的账号和密码
      </div>
      <div class="form">
        <van-form @submit="Submit">
          <div class="username">
            账号
          </div>
          <div class="ipt">
            <van-field v-model="form.username" placeholder="请输入账号" />
          </div>
          <div class="password">
            密码
          </div>
          <div class="ipt">
            <van-field
              type="password"
              v-model="form.password"
              placeholder="请输入密码"
            />
          </div>
          <div class="login">
            <van-button round block type="info" native-type="submit">
              提交
            </van-button>
          </div>
        </van-form>
      </div>
    </div>
  </div>
</template>

<script>
import { login } from "@/apis/login";
export default {
  name: "doctor_login",
  data() {
    return {
      form: {
        username: "",
        password: "",
        ty: 1
      }
    };
  },
  methods: {
    Submit() {
      if (!this.form.username || !this.form.password) {
        this.$toast("请输入用户名和密码");
      } else {
        login(this.form)
          .then(res => {
            console.log(res);
            this.$router.push("/WechatAuthorization");
            // sessionStorage.setItem("token", res.data.token);
            // window.location.href = window.location.origin + window.location.pathname
          })
          .catch(err => {
            this.$toast(err.msg);
          });
      }
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style lang="less">
#doctor_login {
  position: relative;
  .herder {
    img {
      width: 100%;
      height: 250px;
    }
  }
  .main {
    position: absolute;
    top: 194px;
    left: 20px;
    right: 20px;
    height: 445px;
    background: rgba(255, 255, 255, 0.9);
    box-shadow: 0px 20px 20px 0px rgba(0, 0, 0, 0.05);
    border-radius: 10px;
    padding: 20px;
    .welcome {
      margin: auto;
      width: 295px;
      height: 40px;
      font-size: 22px;
      color: rgba(32, 49, 82, 1);
      line-height: 40px;
    }
    .info {
      margin: auto;
      width: 295px;
      height: 17px;
      font-size: 12px;
      color: rgba(124, 134, 152, 1);
      line-height: 17px;
    }
    .form {
      text-align: left;
      margin-top: 48px;
      .username {
        text-align-last: justify;
        text-align: justify;
        text-justify: distribute-all-lines;
        width: 28px;
        height: 20px;
        font-size: 14px;
        font-weight: 500;
        color: rgba(32, 49, 82, 1);
        line-height: 20px;
      }
      .ipt {
        margin-top: 13px;
        padding-bottom: 13px;
        border-bottom: 1px solid rgba(214, 214, 214, 1);
        input {
          // height: 18px;
          line-height: 18px;
          font-size: 18px;
          border: 0;
          background-color: transparent;
        }
      }
      .password {
        text-align-last: justify;
        text-align: justify;
        text-justify: distribute-all-lines;
        width: 28px;
        height: 20px;
        font-size: 14px;
        font-weight: 500;
        color: rgba(32, 49, 82, 1);
        line-height: 20px;
        margin-top: 20px;
      }
      .login {
        margin: 40px 16px 16px;
      }
      .van-button {
        margin: auto;
        // width: 295px;
        height: 55px;
        background: rgba(69, 137, 237, 1);
        box-shadow: 0px 10px 20px 0px rgba(0, 0, 0, 0.1),
          0px 20px 30px 0px rgba(86, 128, 250, 0.25);
        border-radius: 28px;
      }
    }
  }
}
</style>
