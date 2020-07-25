<template>
  <div id="treatmentplan">
    <van-nav-bar title="治疗方案" left-arrow @click-left="onClickLeft">
      <template #right>
        <span @click="$router.push(`/HistoricalPlan/${form.pid}`)">历史方案</span>
      </template>
    </van-nav-bar>
    <div class="main">
      <div>
        <van-form @submit="onSubmit">
          <div class="nav">
            <van-field
              v-model="form.title"
              label="治疗标题"
              placeholder="请输入治疗标题"
              :rules="[{ required: true, message: '请输入治疗标题！' }]"
            />
          </div>
          <div class="nav">
            <van-field
              readonly
              clickable
              :value="form.zldate"
              name="calendar"
              label="治疗时间"
              placeholder="请选择治疗时间"
              right-icon="arrow"
              :rules="[{ required: true, message: '请选择治疗时间！' }]"
              @click="showCalendar = true"
            />
            <van-popup v-model="showCalendar" position="bottom">
              <van-datetime-picker
                v-model="value"
                type="date"
                title="选择治疗时间"
                :min-date="minDate"
                @confirm="onConfirm"
                @cancel="showCalendar = false"
              />
            </van-popup>
          </div>
          <div class="nav">
            <div class="title">治疗方案</div>
            <van-field
              v-model="form.fangan"
              autosize
              rows="4"
              type="textarea"
              placeholder="请输入"
              :rules="[{ required: true, message: '请输入治疗方案' }]"
            />
          </div>
          <div class="nav">
            <div class="title">特别注意</div>
            <van-field
              v-model="form.zhuyi"
              autosize
              rows="4"
              type="textarea"
              placeholder="请输入"
            />
          </div>
          <van-button type="info" native-type="submit">提交</van-button>
        </van-form>
      </div>
    </div>
  </div>
</template>

<script>
import { addfangan } from "@/apis/treatmentplan";
export default {
  data() {
    return {
      showCalendar: false,
      minDate: new Date(1970, 1, 1),
      value: new Date(),
      form: {
        pid: "",
        title: "",
        zldate: "",
        fangan: "",
        zhuyi: ""
      }
    };
  },
  methods: {
    onSubmit() {
      addfangan(this.form)
        .then(res => {
          this.$toast("新建治疗方案成功");
        })
        .catch(err => {
          this.$toast(err.msg);
        });
    },
    onClickLeft() {
      this.$router.go(-1); //返回上一层
    },
    onConfirm(date) {
      this.form.zldate = `${date.getFullYear()}/${date.getMonth() +
        1}/${date.getDate()}`;
      this.showCalendar = false;
    }
  },
  created() {
    this.form.pid = this.$route.params.id;
  }
};
</script>

<style lang="less">
#treatmentplan {
  text-align: left;
  color: #404040;
 
  .van-nav-bar__left {
    .van-icon {
      color: #404040;
    }
  }
  .van-divider {
    border-color: transparent;
    margin: 10px 0;
  }
  .van-nav-bar__right {
    color: #3660c8;
    font-size: 14px;
  }
  .main {
    margin: 15px;
    .nav {
      margin-bottom: 15px;
      background-color: #fff;
      border-radius: 8px;
      .title {
        padding: 20px 0 0px 15px;
        font-size: 15px;
      }
    }
    .van-cell {
      padding: 20px 15px;
      border-radius: 8px;
      &::after {
        right: 0;
        left: 0;
      }
      .van-field__label {
        font-size: 15px;
        width: 60px;
      }
    }
  }
  .van-button {
    width: 100%;
    margin-top: 20px;
    border-radius: 3px;
    font-size: 16px;
    height: 50px;
    line-height: 50px;
  }
}
</style>
