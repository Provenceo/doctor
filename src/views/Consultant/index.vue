<template>
  <div id="consultant">
    <van-nav-bar title="营养顾问">
      <template #right>
        <span @click="$router.push('/remind')">选择</span>
      </template>
    </van-nav-bar>
    <van-tabs @click="onClick">
      <van-tab title="全部">
        <div class="content">
          <div class="gw">
            <van-row type="flex" align="center">
              <van-col span="3" class="avatar">
                <img :src="require('@/assets/images/avatar.png')" alt="" />
              </van-col>
              <van-col span="14" :offset="2">
                <h1 class="name">李某某</h1>
                <h1 class="tag">
                  <van-tag plain type="primary">管理患者10人</van-tag>
                  <van-tag plain type="warning">年限10年</van-tag>
                </h1>
              </van-col>
            </van-row>
            <van-divider
              :style="{
                borderColor: '#F3F3F3'
              }"
            >
            </van-divider>
            <div style="text-align: right">
              <span class="date"
                >已完成
                <h2>3</h2>
              </span>
              <span class="date"
                >未完成
                <h2 style="color:rgba(250,91,87,1);">3</h2>
              </span>
            </div>
          </div>
          <div class="gw">
            <van-row type="flex" align="center">
              <van-col span="3" class="avatar">
                <img :src="require('@/assets/images/avatar.png')" alt="" />
              </van-col>
              <van-col span="14" :offset="2">
                <h1 class="name">李某某</h1>
                <h1 class="tag">
                  <van-tag plain type="primary">管理患者10人</van-tag>
                  <van-tag plain type="warning">年限10年</van-tag>
                </h1>
              </van-col>
            </van-row>
            <van-divider
              :style="{
                borderColor: '#F3F3F3'
              }"
            >
            </van-divider>
            <div style="text-align: right">
              <span class="date"
                >已完成
                <h2>3</h2>
              </span>
              <span class="date"
                >未完成
                <h2 style="color:rgba(250,91,87,1);">3</h2>
              </span>
            </div>
          </div>
          <div class="gw">
            <van-row type="flex" align="center">
              <van-col span="3" class="avatar">
                <img :src="require('@/assets/images/avatar.png')" alt="" />
              </van-col>
              <van-col span="14" :offset="2">
                <h1 class="name">李某某</h1>
                <h1 class="tag">
                  <van-tag plain type="primary">管理患者10人</van-tag>
                  <van-tag plain type="warning">年限10年</van-tag>
                </h1>
              </van-col>
            </van-row>
            <van-divider
              :style="{
                borderColor: '#F3F3F3'
              }"
            >
            </van-divider>
            <div style="text-align: right">
              <span class="date"
                >已完成
                <h2>3</h2>
              </span>
              <span class="date"
                >未完成
                <h2 style="color:rgba(250,91,87,1);">3</h2>
              </span>
            </div>
          </div>
          <div class="gw">
            <van-row type="flex" align="center">
              <van-col span="3" class="avatar">
                <img :src="require('@/assets/images/avatar.png')" alt="" />
              </van-col>
              <van-col span="14" :offset="2">
                <h1 class="name">李某某</h1>
                <h1 class="tag">
                  <van-tag plain type="primary">管理患者10人</van-tag>
                  <van-tag plain type="warning">年限10年</van-tag>
                </h1>
              </van-col>
            </van-row>
            <van-divider
              :style="{
                borderColor: '#F3F3F3'
              }"
            >
            </van-divider>
            <div style="text-align: right">
              <span class="date"
                >已完成
                <h2>3</h2>
              </span>
              <span class="date"
                >未完成
                <h2 style="color:rgba(250,91,87,1);">3</h2>
              </span>
            </div>
          </div>
        </div>
      </van-tab>
      <van-tab title="已完成">已完成</van-tab>
      <van-tab title="未完成">未完成</van-tab>
    </van-tabs>
  </div>
</template>

<script>
export default {
  data() {
    return {
      active: 0,
      img: "~@/assets/images/avatar.png"
    };
  },
  methods: {
    onClick(name, title) {
      this.$toast(title);
    }
  },
  mounted() {}
};
</script>

<style lang="less">
#consultant {
  text-align: left;
  .van-nav-bar {
    background: rgba(255, 255, 255, 1);
  }
  .van-nav-bar__right {
    color: #3660c8;
  }
  .content {
    .gw {
      margin: 10px;
      padding: 10px 10px 22px;
      background-color: #fff;
      border-radius: 8px;
      .name {
        font-size: 15px;
      }
      .tag {
        margin-right: 9px;
        margin-top: 12px;
      }
      .date {
        margin-left: 30px;
        h2 {
          font-size: 18px;
          color: rgba(64, 64, 64, 1);
        }
      }
    }
  }
}
</style>
