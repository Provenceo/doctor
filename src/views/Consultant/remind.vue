<template>
  <div id="remind">
    <van-nav-bar
      title="营养顾问"
      left-arrow
      @click-left="onClickLeft"
      class="nav"
    >
    </van-nav-bar>
    <div class="title">
      <van-checkbox v-model="checked" @click="checkAll"
        >已选择({{ result.length }}/{{ list.length }})</van-checkbox
      >
    </div>
    <div class="content">
      <van-checkbox-group v-model="result" ref="checkboxGroup">
        <div v-for="item in list" :key="item.id">
          <van-checkbox :name="item.id">
            <van-row type="flex" align="center">
              <van-col span="4" class="avatar"
                ><img :src="require('@/assets/images/avatar.png')" alt=""
              /></van-col>
              <van-col span="18" :offset="1">
                <h1>{{ item.name }}</h1>
                <div class="main">
                  <span>已完成</span
                  ><strong style="color:rgba(64,64,64,1);">{{
                    item.ywc
                  }}</strong>
                  <span>未完成</span
                  ><strong style="color:rgba(250,91,87,1);">{{
                    item.wwc
                  }}</strong>
                </div>
              </van-col>
            </van-row>
          </van-checkbox>
        </div>
      </van-checkbox-group>
      <van-button type="info">提醒</van-button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      checked: false,
      list: [
        {
          id: 1,
          name: "李某某",
          wwc: "3",
          ywc: "3"
        },
        {
          id: 2,
          name: "张某某",
          wwc: "0",
          ywc: "3"
        },
        {
          id: 3,
          name: "王某某",
          wwc: "0",
          ywc: "0"
        }
      ],
      result: [],
      active: 0,
      img: "~@/assets/images/avatar.png"
    };
  },
  methods: {
    onClickLeft() {
      this.$router.go(-1); //返回上一层
    },
    onClick(name, title) {
      this.$toast(title);
    },
    checkAll() {
      if (this.checked) {
        this.$refs.checkboxGroup.toggleAll(true);
      } else {
        this.$refs.checkboxGroup.toggleAll();
      }
    }
  },
  mounted() {
    console.log(this.$refs.checkboxGroup.children);
  },
  watch: {
    result(val) {
      if (val.length === this.$refs.checkboxGroup.children.length) {
        this.checked = true;
      } else {
        this.checked = false;
      }
    }
  }
};
</script>

<style lang="less">
#remind {
  text-align: left;
  .van-nav-bar__left {
    .van-icon {
      color: #404040;
    }
  }
  .van-nav-bar {
    background-color: #fff;
  }
  .van-checkbox__label {
    margin-left: 24px;
    width: 100%;
  }
  .title {
    padding: 17px 0 18px 22px;
    background: rgba(241, 241, 241, 1);
  }
  .content {
    padding: 20px 20px 22px;
    background-color: #fff;
    .van-col {
      h1 {
        font-size: 15px;
        color: rgba(64, 64, 64, 1);
      }
      .main {
        margin-top: 6px;
        span {
          font-size: 12px;
          color: rgba(153, 153, 153, 1);
        }
        strong {
          margin-left: 10px;
          margin-right: 26px;
          font-size: 18px;
        }
      }
    }
    .van-checkbox {
      padding-bottom: 20px;
      margin-top: 20px;
      border-bottom: 1px solid #f5f5f5;
      &:first-child {
        margin-top: 0;
      }
    }
    .van-button {
      margin-top: 30px;
      width: 100%;
      height: 50px;
      font-size: 16px;
    }
  }
}
</style>
