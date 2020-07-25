<template>
  <div id="home">
    <div class="header">
      <van-swipe class="my-swipe" :autoplay="3000" indicator-color="white">
        <van-swipe-item v-for="item in banner" :key="item.id">
          <a :href="item.url">
            <img :src="item.img" alt="" />
          </a>
        </van-swipe-item>
      </van-swipe>
    </div>
    <div class="content">
      <div class="data">
        <div class="title">数据统计</div>
        <div class="main">
          <ul class="clearfix">
            <li>
              <div>
                <p>现存患者</p>
                <h2>{{ dataStatistics.huanzhe }}</h2>
              </div>
            </li>
            <li>
              <div>
                <p>现有营养顾问</p>
                <h2>{{ dataStatistics.guwen }}</h2>
              </div>
            </li>
            <li>
              <div>
                <p>本月复查人数</p>
                <h2>{{ dataStatistics.fucha }}</h2>
              </div>
            </li>
            <li>
              <div>
                <p>本月提交日志</p>
                <h2>{{ dataStatistics.logs }}</h2>
              </div>
            </li>
          </ul>
        </div>
      </div>
      <div class="msg">
        <div class="title">消息提醒</div>
        <div class="main">
          <ul>
            <li v-for="item in massage" :key="item.id">
              <van-row type="flex" justify="space-between" align="center">
                <van-col span="2">
                  <img src="@/assets/images/doctor202007171725 _106.png" alt=""
                /></van-col>
                <van-col span="16" class="content">
                  <span class="title">{{ item.title }}：</span>
                  <span class="info">{{ item.content }}</span></van-col
                >
                <van-col span="6"
                  ><span class="date">{{ item.created }}</span></van-col
                >
              </van-row>
            </li>
            <li class="no" v-if="massage.length === 0">
              暂无数据
            </li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { home } from "@/apis/home";
export default {
  name: "home",
  data() {
    return {
      banner: [],
      dataStatistics: {},
      massage: []
    };
  },
  methods: {
    LoadHome() {
      home().then(res => {
        this.banner = res.data.banner;
        this.dataStatistics = res.data.tongji;
        this.massage = res.data.tixing;
      });
    }
  },
  mounted() {
    this.LoadHome();
  }
};
</script>

<style lang="less">
#home {
  text-align: left;
  padding-bottom: 40px;
  .header {
    // height: 192px;
    .my-swipe .van-swipe-item {
      color: #fff;
      font-size: 20px;
      height: 192px;
      line-height: 192px;
      text-align: center;
      background-color: #39a9ed;
      a {
        display: inline-block;
        width: 100%;
        height: 192px;
        img {
          width: 100%;
          height: 192px;
        }
      }
    }
  }

  .title {
    font-size: 20px;
    color: rgba(64, 64, 64, 1);
    line-height: 20px;
    padding-left: 5px;
    margin-bottom: 20px;
    font-weight: bold;
  }
  .content {
    margin: 15px;
    .data {
      .main {
        background-color: #fff;
        box-shadow: 0px 0px 8px 0px rgba(229, 229, 229, 1);
        border-radius: 8px;
        padding: 30px 0 0 12px;
        ul {
          li {
            width: 50%;
            float: left;
            margin-bottom: 30px;
            p {
              height: 13px;
              font-size: 13px;
              color: rgba(64, 64, 64, 1);
            }
            h2 {
              margin-top: 10px;
              font-size: 26px;
              color: rgba(64, 120, 244, 1);
            }
          }
        }
      }
    }
    .msg {
      margin-top: 30px;
      .main {
        background-color: #fff;
        box-shadow: 0px 0px 8px 0px rgba(229, 229, 229, 1);
        border-radius: 8px;
        padding: 0 0 0 12px;
        ul {
          .no {
            text-align: center;
            font-size: 15px;
          }
          li {
            height: 60px;
            line-height: 60px;
            border-bottom: 1px solid rgba(245, 245, 245, 1);
            img {
              display: inline-block;
              vertical-align: sub;
              width: 20px;
              height: 20px;
            }
            &:last-child {
              border: 0;
            }
            .van-row {
              height: 60px;
              line-height: 60px;
            }
            .content {
              margin: 0;
              width: 280px;
              display: inline-block;
              overflow: hidden;
              text-overflow: ellipsis;
              white-space: nowrap;
              .title {
                font-size: 15px;
              }
              .info {
                font-size: 15px;
              }
            }
            .date {
              float: right;
              margin-right: 10px;
              font-size: 13px;
              color: rgba(153, 153, 153, 1);
            }
          }
        }
      }
    }
  }
}
</style>
