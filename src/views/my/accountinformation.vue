<template>
  <div id="accountinformation">
    <van-nav-bar
      title="账号信息"
      left-arrow
      @click-left="onClickLeft"
      class="nav"
    >
    </van-nav-bar>
    <div class="main">
      <van-cell title="头像" is-link class="avatar" center>
        <template #default>
          <img :src="require('@/assets/images/avatar.png')" alt="" />
        </template>
      </van-cell>
      <van-cell title="用户名" value="用户名" is-link center />
      <van-cell title="性别" value="性别" is-link center />
      <van-cell title="出生日期" value="出生日期" is-link center />
      <van-cell title="身份证号" value="身份证号" is-link center />
      <van-cell title="从业年限" value="从业年限" is-link center />
      <van-cell title="联系方式" value="联系方式" is-link center />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {};
  },
  methods: {
    onClickLeft() {
      this.$router.go(-1); //返回上一层
    }
  },
  mounted() {}
};
</script>

<style lang="less">
#accountinformation {
  text-align: left;
  height: 100%;
  .van-nav-bar {
    background: rgba(241, 241, 241, 1);
  }
  .van-nav-bar__left {
    .van-icon {
      color: #404040;
    }
  }
  .main {
    padding: 2px 20px;
    background-color: #fff;
    .van-cell {
      padding: 18px 0;
      &::after {
          left: 0;
          right: 0;
      }
      .van-cell__title {
        width: 35px;
      }
    }
  }
}
</style>
