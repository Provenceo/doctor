<template>
  <!-- 软食 -->
  <div id="SoftFood">
    <van-nav-bar title="膳食处方"></van-nav-bar>
    <div class="main">
      <div
        class="food"
        v-for="val in foodData"
        :key="val.id"
        @click="onChange(val)"
      >
        <van-row type="flex" align="center">
          <van-col span="4">
            <div class="num">{{ val.id }}</div>
          </van-col>
          <van-col span="18" :offset="6">
            <div class="content">
              <div v-for="list in val.list" :key="list">
                {{ list }}
              </div>
            </div>
          </van-col>
        </van-row>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      item: "",
      foodData: [
        {
          id: 1,
          list: ["肉沫粥 200g", "煮鸡蛋1个", "青菜木耳香"]
        },
        {
          id: 2,
          list: ["肉沫粥 200g"]
        },
        {
          id: 3,
          list: ["肉沫粥 200g", "煮鸡蛋1个"]
        }
      ]
    };
  },
  methods: {
    onChange(val) {
      let obj = JSON.parse(localStorage.getItem("form"));
      if (this.item === "breakfast") {
        obj.breakfast = val.id + "号套餐";
        obj.breakList = val;
      }
      if (this.item === "lunch") {
        obj.lunch = val.id + "号套餐";
        obj.lunchList = val;
      }
      if (this.item === "dinner") {
        obj.dinner = val.id + "号套餐";
        obj.dinnerList = val;
      }
      console.log(JSON.stringify(obj));
      localStorage.setItem("form", JSON.stringify(obj));
      this.$router.go(-1);
    }
  },
  mounted() {},
  created() {
    this.item = this.$route.params.item;
    console.log(this.item);
  }
};
</script>

<style lang="less">
#SoftFood {
  text-align: left;
  .van-nav-bar {
    background-color: #f5f5f5;
  }
  .main {
    margin: 10px 10px;
  }
  .food {
    border-radius: 8px;
    margin: 10px 0;
    background-color: #fff;
    .van-row {
      position: relative;
    }
    .van-col {
      &:first-child {
        position: absolute;
        background-color: #4589ed;
        height: 100%;
        font-size: 30px;
        color: #fff;
        border-top-left-radius: 8px;
        border-bottom-left-radius: 8px;
        width: 25%;
      }
      .num {
        position: absolute;
        height: 42px;
        width: 18px;
        left: 50%;
        top: 50%;
        margin-left: -9px;
        margin-top: -18px;
      }
      .content {
        padding: 9px 0 9px 9px;
        div {
          margin-bottom: 15px;
          &:last-child {
            margin-bottom: 0;
          }
        }
      }
    }
  }
}
</style>
