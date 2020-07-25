<template>
  <div id="my">
    <van-nav-bar>
      <template #left>
        <img src="@/assets/images/doctor202007171725 _12.png" alt="" />
      </template>
      <template #right>
        <img src="@/assets/images/doctor202007171725 _6.png" alt="" />
      </template>
    </van-nav-bar>
    <div class="main">
      <div class="header">
        <div class="massage">
          <van-row
            type="flex"
            align="center"
            @click="$router.push('/AccountInformation')"
          >
            <van-col span="4" class="avatar"
              ><img :src="require('@/assets/images/avatar.png')" alt=""
            /></van-col>
            <van-col span="14">
              <h1 class="name">李某某</h1>
              <div class="tag">
                <van-tag plain type="primary">
                  <img
                    src="@/assets/images/doctor202007171725 _15.png"
                    alt=""
                  />
                  主管医生
                </van-tag>
                <van-tag plain type="warning">从业10年</van-tag>
              </div></van-col
            >
          </van-row>
        </div>
        <div class="people">
          <div class="title">
            管理人数
          </div>
          <van-row type="flex" align="center">
            <van-col span="12">
              <h2>100</h2>
              人
              <div>患者</div>
            </van-col>
            <van-col span="12">
              <h2>30</h2>
              人
              <div>营业顾问</div>
            </van-col>
          </van-row>
        </div>
      </div>
      <div class="content">
        <div class="title">常用工具</div>
        <van-cell
          title="直播台"
          is-link
          :icon="require('@/assets/images/doctor202007171725 _9.png')"
        />
        <van-cell
          is-link
          title="留言板"
          :icon="require('@/assets/images/doctor202007171725 _8.png')"
        />
        <van-cell
          is-link
          title="调查问卷"
          :icon="require('@/assets/images/doctor202007171725 _14.png')"
        />
        <van-cell
          is-link
          title="知识推送"
          :icon="require('@/assets/images/doctor202007171725 _18.png')"
        />
        <van-cell
          is-link
          title="意见反馈"
          :icon="require('@/assets/images/doctor202007171725 _5.png')"
        />
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="less">
#my {
  text-align: left;
  .van-nav-bar {
    background: url("~@/assets/images/doctor202007171725 _83.png");
    background-size: 100% 293px;
    background-position-y: 0;
    .van-nav-bar__left {
      img {
        width: 18px;
      }
    }
    .van-nav-bar__right {
      img {
        width: 18px;
      }
    }
  }
  .main {
    .header {
      height: 293px;
      background: url("~@/assets/images/doctor202007171725 _83.png") no-repeat;
      background-position-y: -50px;
      background-size: 100% 293px;
      padding: 40px 20px 20px 20px;
      .massage {
        color: #fff;
        margin-bottom: 55px;
        .van-tag--primary {
          background: transparent;
          border-radius: 4px;
          color: #fff;
          background: rgba(0, 0, 0, 0.4);
        }
        .van-tag--warning {
          background: transparent;
          border-radius: 4px;
          height: 20px;
          font-size: 10px;
          padding: 0 10px;
          color: #fff;
          margin-left: 4px;
        }
        .tag {
          margin-top: 10px;
          img {
            width: 10px;
            margin-right: 3px;
            // vertical-align: top;
          }
          .van-tag {
            vertical-align: text-bottom;
          }
        }
        .avatar {
          margin-right: 15px;
        }
      }
      .people {
        background: rgba(255, 255, 255, 1);
        border-radius: 9px;
        text-align: center;
        padding: 20px 20px 20px 20px;
        .title {
          text-align: left;
          font-size: 18px;
          margin-bottom: 20px;
        }
        .van-row {
          font-size: 14px;
          color: rgba(153, 153, 153, 1);
          .van-col {
            &:first-child {
              border-right: 1px solid #f5f5f5;
            }
          }
          h2 {
            color: #4589ed;
            font-size: 24px;
          }
        }
      }
    }
    .content {
      margin: 15px 20px 0;
      background-color: #fff;
      padding: 20px 20px 0 20px;
      border-radius: 9px;
      color: #404040;
      .title {
        font-size: 18px;
      }
      .van-cell {
        font-size: 15px;
        padding: 22px 0;
        .van-icon__image {
          width: 18px;
          height: 18px;
          margin-right: 15px;
        }
        &::after {
          left: 0;
          right: 0;
        }
      }
    }
  }
}
</style>
