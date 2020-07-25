<template>
  <div id="detail">
    <van-nav-bar title="患者详情" left-arrow @click-left="onClickLeft" />
    <div class="header">
      <div class="massage">
        <van-row type="flex" justify="space-around" align="center" class="top">
          <van-col span="3" class="avatar">
            <img
              :src="info.img ? info.img : require('@/assets/images/avatar.png')"
              alt=""
            />
          </van-col>
          <van-col span="15">
            <div class="gr">
              <span class="name">{{ info.name }}</span>
              <van-tag plain type="primary" v-if="info.jibing">{{
                info.jibing
              }}</van-tag>
              <van-tag plain type="warning" v-if="info.gwname">{{
                info.gwname
              }}</van-tag>
            </div>
            <div class="tel">电话：{{ info.tel1 }} {{ info.tel2 }}</div>
          </van-col>
          <van-col span="2" style="position: relative;">
            <div>
              <img
                src="@/assets/images/doctor202007171725 _12.png"
                alt=""
                class="tx"
              />
              <span class="van-info info">{{ tongji.msgnums }}</span>
            </div>
          </van-col>
        </van-row>
        <van-divider
          :style="{
            borderColor: 'rgba(255,255,255,.6)',
            padding: '0 16px'
          }"
        >
        </van-divider>
        <div class="record">
          <span>
            <h1>{{ tongji.logsnums }}</h1>
            <p>健康记录</p>
          </span>
          <span>
            <h1>{{ tongji.fangannums }}</h1>
            <p>治疗方案</p>
          </span>
          <span>
            <h1>{{ tongji.blnums }}</h1>
            <p>病例记录</p>
          </span>
          <span>
            <h1>{{ tongji.cfnums }}</h1>
            <p>营养处方</p>
          </span>
        </div>
      </div>
    </div>
    <div class="main">
      <van-row
        type="flex"
        justify="space-between"
        align="center"
        class="fangan"
        @click="record"
      >
        <van-col span="2">
          <img src="@/assets/images/doctor202007171725 _2.png" alt="" />
        </van-col>
        <van-col span="20">新增病例</van-col>
        <van-col span="2" :offset="2"><van-icon name="arrow"/></van-col>
      </van-row>
      <van-row
        type="flex"
        justify="space-between"
        align="center"
        class="fangan"
        @click="$router.push(`/TreatmentPlan/${detailId}`)"
      >
        <van-col span="2">
          <img src="@/assets/images/doctor202007171725 _7.png" alt="" />
        </van-col>
        <van-col span="20">新增治疗方案</van-col>
        <van-col span="2" :offset="2"><van-icon name="arrow"/></van-col>
      </van-row>
      <van-row
        type="flex"
        justify="space-between"
        align="center"
        class="fangan"
        @click="$router.push(`/newNutritionPrescription/${detailId}`)"
      >
        <van-col span="2">
          <img src="@/assets/images/doctor202007171725 _39.png" alt="" />
        </van-col>
        <van-col span="20">新增营养处方</van-col>
        <van-col span="2" :offset="2"><van-icon name="arrow"/></van-col>
      </van-row>
    </div>
  </div>
</template>

<script>
import { patientDetail } from "@/apis/patient";
export default {

  data() {
    return {
      detailId: null,
      info: {},
      tongji: {},
      detailData: {
        id: "",
        gwname: "",
        name: "",
        img: "",
        jibing: "",
        blnums: ""
      }
    };
  },
  methods: {
    onClickLeft() {
      this.$router.go(-1); //返回上一层
    },
    detail() {
      patientDetail({ id: this.detailId })
        .then(res => {
          this.detailData = {
            id: res.data.info.id,
            gwname: res.data.info.gwname,
            name: res.data.info.name,
            img: res.data.info.img,
            jibing: res.data.info.jibing,
            blnums: res.data.tongji.blnums
          };
          this.info = res.data.info;
          this.tongji = res.data.tongji;
        })
        .catch(err => {
          this.$toast(err.msg);
        });
    },
    record() {
      var detail = JSON.stringify(this.detailData);
      this.$router.push("/record/" + encodeURIComponent(detail));
    }
  },
  mounted() {
    this.detail();
  },
  created() {
    this.detailId = this.$route.params.id;
  }
};
</script>

<style lang="less">
#detail {
  text-align: left;
  .tel {
    font-size: 14px;
  }
  .avatar {
    img {
      width: 50px;
      height: 52px;
    }
  }
  .fangan {
    padding: 20px 20px;
    background-color: #fff;
  }
  .van-icon {
    color: #404040;
  }
  .header {
    background: url("~@/assets/images/doctor202007171725 _82.png") no-repeat;
    background-size: 100% auto;
    height: 234px;
    // width: 375px;
    .massage {
      .gr {
        margin-bottom: 10px;
      }
      .name {
        font-size: 15px;
        font-weight: bold;
      }
      .tx {
        width: 20px;
      }
      .top {
        margin-bottom: 25px;
      }
      color: #fff;
      padding-top: 35px;
      .van-tag--plain {
        background-color: transparent;
      }
      .van-tag--primary.van-tag--plain {
        color: #fff;
      }
      .van-tag--warning.van-tag--plain {
        color: #f7d300;
      }
      .van-info {
        left: 4px;
        right: auto;
      }
      .record {
        span {
          display: inline-block;
          width: 24%;
          text-align: center;
          h1 {
            margin-top: 25px;
            margin-bottom: 10px;
            font-size: 24px;
            //   font-weight: bold
          }
          p {
            font-size: 12px;
            color: rgba(255, 255, 255, 0.8);
          }
        }
      }
    }
  }
  .main {
    img {
      width: 15px;
    }
    div {
      font-weight: bold;
    }
    .van-row {
      color: #404040;
      font-size: 15px;
      border-bottom: 1px solid rgba(245, 245, 245, 1);
      &:last-child {
        border-bottom: 0;
      }
      img {
        vertical-align: middle;
      }
    }
  }
}
</style>
