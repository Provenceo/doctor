<template>
  <div id="patient">
    <van-nav-bar title="患者">
      <template #left>
        <van-icon name="scan" size="20" />
      </template>
      <template #right>
        <img src="@/assets/images/doctor202007171725 _10.png" alt="" />
      </template>
    </van-nav-bar>
    <div class="main">
      <van-search
        v-model="init.key"
        placeholder="请输入搜索关键词"
        input-align="center"
      />
      <van-empty
        image="search"
        description="暂无数据"
        v-if="list.length === 0"
      />
      <van-pull-refresh v-model="refreshing" @refresh="onRefresh">
        <van-list
          v-model="loading"
          :finished="finished"
          finished-text="没有更多了"
          v-if="list.length"
        >
          <van-swipe-cell v-for="item in list" :key="item.id">
            <van-row
              type="flex"
              justify="space-around"
              align="center"
              @click="$router.push(`/detail/${item.id}`)"
            >
              <van-col span="3" class="avatar">
                <img
                  :src="
                    item.img ? item.img : require('@/assets/images/avatar.png')
                  "
                  alt=""
                />
              </van-col>
              <van-col span="15">
                <div class="gr">
                  <span class="name">{{ item.name }}</span>
                  <van-tag plain type="primary" v-if="item.jibing">{{
                    item.jibing
                  }}</van-tag>
                  <van-tag plain type="warning" v-if="item.gwname"
                    >顾问 : {{ item.gwname }}</van-tag
                  >
                </div>
                <div>电话：{{ item.tel1 }}</div>
              </van-col>
              <van-col span="2" style="position: relative;">
                <div v-if="item.msgnums">
                  <img
                    src="@/assets/images/doctor202007171725 _11.png"
                    alt=""
                    class="tx"
                  />
                  <span class="van-info info" badge="99+">{{
                    item.msgnums
                  }}</span>
                </div>
              </van-col>
            </van-row>
            <template #right>
              <van-button square type="info" text="新增病例" />
              <van-button
                square
                type="primary"
                text="治疗方案"
                class="TreatmentPlan"
              />
            </template>
          </van-swipe-cell>
        </van-list>
      </van-pull-refresh>
    </div>
    <div class="addPatient">
      <img
        src="@/assets/images/doctor202007171725 _22.png"
        alt=""
        @click="$router.push('/addPatient')"
      />
    </div>
  </div>
</template>

<script>
import { patient } from "@/apis/patient";
export default {
  data() {
    return {
      list: [],
      loading: false,
      finished: false,
      refreshing: false,
      init: {
        key: "",
        page: 1
      }
    };
  },
  methods: {
    detail() {},
    onClickLeft() {
      this.$toast("返回");
    },
    onClickRight() {
      this.$toast("按钮");
    },
    patient() {
      patient(this.init)
        .then(res => {
          if (this.refreshing) {
            this.list = [];
            this.refreshing = false;
          }
          res.data.list.forEach(item => {
            this.list.push(item);
          });
          this.init.page++;
          if (this.list.length === res.data.list.length) {
            this.loading = false;
            this.finished = true;
          }
        })
        .catch(err => {
          this.$toast(err.msg);
        });
    },
    onRefresh() {
      // 清空列表数据
      this.init.page = 1;
      this.finished = false;
      // 重新加载数据
      // 将 loading 设置为 true，表示处于加载状态
      this.loading = true;
      this.patient();
    }
  },
  mounted() {
    this.patient();
  },
  computed: {
    key() {
      return this.init.key;
    }
  },
  watch: {
    "init.key": {
      deep: true,
      handler: function(newV, oldV) {
        this.init.page = 1;
        this.list = [];
        this.patient();
      }
    }
  }
};
</script>

<style lang="less">
#patient {
  text-align: left;
  padding-bottom: 40px;
  .avatar {
    img {
      width: 50px;
      height: 52px;
    }
  }
  .gr {
    margin-bottom: 10px;
    .name {
      font-size: 15px;
      font-weight: bold;
    }
  }
  .tx {
    width: 20px;
  }
  .addPatient {
    img {
      width: 73px;
      height: 73px;
    }
  }
  .van-info {
    left: 4px;
    right: auto;
  }
  .van-nav-bar__right {
    img {
      width: 20px;
    }
  }
  .van-swipe-cell__wrapper {
    padding: 15px 0;
    background-color: #fff;
    border-bottom: 1px solid #f3f3f3;
    .van-button {
      height: 100%;
      &.TreatmentPlan {
        background-color: #72b3f5;
        border: 1px solid #72b3f5;
      }
    }
  }
  .addPatient {
    position: fixed;
    right: 0;
    bottom: 60px;
  }
}
</style>
