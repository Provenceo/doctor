<template>
  <div id="TakingProducts">
    <van-nav-bar title="服用产品"> </van-nav-bar>
    <div class="product">
      <div class="header">
        <van-row type="flex" justify="space-between">
          <van-col span="6">产品名称</van-col>
          <van-col span="6">服用剂量</van-col>
        </van-row>
      </div>
      <div class="content">
        <van-row
          type="flex"
          justify="space-between"
          v-for="item in list"
          :key="item.id"
        >
          <van-col span="6">{{ item.name }}</van-col>
          <van-col span="6">
            <van-field v-model="item.num" />
          </van-col>
        </van-row>
      </div>
      <van-button type="info" @click="sure">确定</van-button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      value: "",
      list: [
        {
          id: 1,
          name: "洗衣粉",
          num: ""
        },
        { id: 2, name: "酸奶", num: "" }
      ]
    };
  },
  methods: {
    sure() {
      let obj = JSON.parse(localStorage.getItem("form"));
      let list = this.list.filter(item => {
        if (item.num != "") {
          return item;
        }
      });
      obj.list = list;
      localStorage.setItem("form", JSON.stringify(obj));
      this.$router.go(-1)
      console.log(list);
    }
  },
  mounted() {}
};
</script>

<style lang="less">
#TakingProducts {
  text-align: left;
  background-color: #fff;
  margin-bottom: 50px;
  .van-nav-bar {
    background-color: #ededed;
  }
  .product {
    padding: 26px 20px;
    .header {
      border-bottom: 1px solid #f5f5f5;
      padding-bottom: 19px;
      color: #999999;
    }
    .content {
      .van-row {
        padding: 15px 0;
        border-bottom: 1px solid #f5f5f5;
        .van-cell {
          padding: 0;
          input {
            width: 70px;
            height: 26px;
            border-radius: 8px;
            text-align: center;
            border: 1px solid rgba(221, 221, 221, 1);
          }
        }
      }
    }
    .van-button {
      width: 100%;
      height: 50px;
      line-height: 50px;
      font-size: 16px;
      margin-top: 30px;
    }
  }
}
</style>
