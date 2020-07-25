<template>
  <div id="newNutritionPrescription">
    <van-nav-bar title="新增营养处方" left-arrow @click-left="onClickLeft">
      <template #right>
        历史营养处方
      </template>
    </van-nav-bar>
    <div class="main">
      <div class="prescription">
        <h1>营养处方</h1>
        <van-row type="flex" justify="space-between" align="center">
          <van-col span="20"
            ><van-field
              v-model="form.title"
              label="建议摄入能量"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="3" class="company">千卡</van-col>
        </van-row>
        <van-row type="flex" justify="space-between" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.message"
              label="建议摄入蛋白质"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="3" class="company">g</van-col>
        </van-row>
      </div>
      <div class="dietprescription">
        <h1>膳食处方</h1>
        <div class="breakfast">
          <img src="@/assets/images/Dietzc.png" alt="" />
          <van-field name="radio" label="食品方式" input-align="right">
            <template #input>
              <van-radio-group v-model="form.radio" direction="horizontal">
                <van-radio name="1">软食</van-radio>
                <van-radio name="2">半流食</van-radio>
              </van-radio-group>
            </template>
          </van-field>
          <van-field
            readonly
            clickable
            name="picker"
            v-model="form.breakfast"
            label="食品套餐"
            placeholder="请选择食品套餐"
            right-icon="arrow"
            @click="onChange(form.radio, 'breakfast')"
            :rules="[{ required: true, message: '请选择食品套餐！' }]"
          />
          <div class="foodMain" v-if="form.breakList">
            <div class="food">
              <van-row type="flex" align="center">
                <van-col span="4">
                  <div class="num">{{ form.breakList.id }}</div>
                </van-col>
                <van-col span="18" :offset="6">
                  <div class="content">
                    <div v-for="val in form.breakList.list" :key="val">
                      {{ val }}
                    </div>
                  </div>
                </van-col>
              </van-row>
            </div>
          </div>
        </div>
        <div class="lunch">
          <img src="@/assets/images/Dietwuc.png" alt="" />
          <van-field name="radio" label="食品方式" input-align="right">
            <template #input>
              <van-radio-group v-model="form.radio" direction="horizontal">
                <van-radio name="1">软食</van-radio>
                <van-radio name="2">半流食</van-radio>
              </van-radio-group>
            </template>
          </van-field>
          <van-field
            readonly
            clickable
            name="picker"
            v-model="form.lunch"
            label="食品套餐"
            placeholder="请选择食品套餐"
            right-icon="arrow"
            @click="onChange(form.radio, 'lunch')"
            :rules="[{ required: true, message: '请选择食品套餐！' }]"
          />
          <div class="foodMain" v-if="form.lunchList">
            <div class="food">
              <van-row type="flex" align="center">
                <van-col span="4">
                  <div class="num">{{ form.lunchList.id }}</div>
                </van-col>
                <van-col span="18" :offset="6">
                  <div class="content">
                    <div v-for="list in form.lunchList.list" :key="list">
                      {{ list }}
                    </div>
                  </div>
                </van-col>
              </van-row>
            </div>
          </div>
        </div>
        <div class="dinner">
          <img src="@/assets/images/Dietwc.png" alt="" />
          <van-field name="radio" label="食品方式" input-align="right">
            <template #input>
              <van-radio-group v-model="form.radio1" direction="horizontal">
                <van-radio name="1">软食</van-radio>
                <van-radio name="2">半流食</van-radio>
              </van-radio-group>
            </template>
          </van-field>
          <van-field
            readonly
            clickable
            name="picker"
            v-model="form.dinner"
            label="食品套餐"
            placeholder="请选择食品套餐"
            right-icon="arrow"
            @click="onChange(form.radio1, 'dinner')"
            :rules="[{ required: true, message: '请选择食品套餐' }]"
          />
          <div class="foodMain" v-if="form.dinnerList">
            <div class="food">
              <van-row type="flex" align="center">
                <van-col span="4">
                  <div class="num">{{ form.dinnerList.id }}</div>
                </van-col>
                <van-col span="18" :offset="6">
                  <div class="content">
                    <div v-for="list in form.dinnerList.list" :key="list">
                      {{ list }}
                    </div>
                  </div>
                </van-col>
              </van-row>
            </div>
          </div>
        </div>
      </div>
      <div class="oral">
        <h1>口服营养方案</h1>
        <van-field
          readonly
          clickable
          name="datetimePicker"
          :value="value"
          label="口服时间"
          right-icon="arrow"
          placeholder="请选择口服时间"
          @click="showPicker = true"
          :rules="[{ required: true, message: '请选择口服时间！' }]"
        />
        <van-popup v-model="showPicker" position="bottom">
          <van-datetime-picker
            type="time"
            @confirm="ondateConfirm"
            @cancel="showPicker = false"
          />
        </van-popup>
        <van-field
          readonly
          clickable
          name="picker"
          :value="form.jibing"
          label="服用产品"
          placeholder="请选择服用产品"
          right-icon="arrow"
          @click="onProduct"
          :rules="[{ required: true, message: '请选择服用产品！' }]"
        />
        <div v-if="form.list" class="content">
          <van-row
          type="flex"
          justify="space-between"
          align="center"
          v-for="item in form.list"
          :key="item.id"
        >
          <van-col span="6">{{ item.name }}</van-col>
          <van-col span="6">
            <van-field v-model="item.num" />
          </van-col>
        </van-row>
        </div>
        <div class="add">
          <img src="@/assets/images/add.png" alt="" />
        </div>
      </div>
      <div class="extrameals">
        <h1>加餐建议</h1>
        <van-field
          readonly
          clickable
          name="datetimePicker"
          :value="value"
          label="加餐时间"
          right-icon="arrow"
          placeholder="请选择加餐时间"
          @click="showjcPicker = true"
          :rules="[{ required: true, message: '请选择加餐时间！' }]"
        />
        <van-popup v-model="showjcPicker" position="bottom">
          <van-datetime-picker
            type="time"
            @confirm="onjcConfirm"
            @cancel="showjcPicker = false"
          />
        </van-popup>
        <van-field
          readonly
          clickable
          name="picker"
          :value="form.jibing"
          label="加餐食品"
          placeholder="请选择加餐食品"
          right-icon="arrow"
          @click="showzSptc = true"
          :rules="[{ required: true, message: '请选择加餐食品！' }]"
        />
        <van-popup v-model="showzSptc" position="bottom">
          <van-picker
            show-toolbar
            :columns="Sptc"
            @confirm="onSptcConfirm"
            @cancel="showzSptc = false"
          />
        </van-popup>
        <div class="add">
          <img src="@/assets/images/add.png" alt="" />
        </div>
      </div>
      <div class="exercise">
        <h1>运动处方</h1>
        <van-field
          v-model="form.message"
          autosize
          rows="4"
          type="textarea"
          placeholder="请输入"
        />
      </div>
      <div>
        <van-button type="info">提交</van-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showzSptc: false,
      showlSptc: false,
      showwSptc: false,
      showPicker: false,
      showjcPicker: false,
      minDate: new Date(1970, 1, 1),
      value: "",
      Sptc: [],
      form: {
        id: "",
        title: "",
        radio: "1",
        radio1: "2",
        lunch: "",
        dinner: "",
        breakfast: "",
        jibing: "",
        message: "",
        birthday: ""
      }
    };
  },
  methods: {
    onClickLeft() {
      this.$router.go(-1); //返回上一层
    },
    onSptcConfirm(val) {
      this.showSptc = false;
    },
    ondateConfirm(time) {
      this.showPicker = false;
    },
    onjcConfirm(time) {
      this.showjcPicker = false;
    },
    onConfirm(date) {
      this.form.birthday = `${date.getFullYear()}/${date.getMonth() +
        1}/${date.getDate()}`;
      this.showzSptc = false;
    },
    onChange(val, item) {
      localStorage.setItem("form", JSON.stringify(this.form));
      if (val === "1") {
        this.$router.push(`/SoftFood/${item}`);
      } else {
        this.$router.push(`/SemiLiquidFood/${item}`);
      }
    },
    onProduct() {
      localStorage.setItem("form", JSON.stringify(this.form));
      this.$router.push(`/TakingProducts`);
    }
    // TakingProducts
  },
  created() {
    this.form.id = this.$route.params.id;
    let arr = localStorage.getItem("form");
    if (arr !== null) {
      this.form = JSON.parse(arr);
      console.log(this.form);
    }
  }
};
</script>

<style lang="less">
#newNutritionPrescription {
  text-align: left;
  .van-nav-bar__left {
    .van-icon {
      color: #404040;
    }
  }
  .foodMain {
    margin: 10px 10px;
    box-shadow: 0px 2px 4px 0px rgba(230, 230, 230, 0.5);
    border-top-right-radius: 8px;
    border-bottom-right-radius: 8px;
  }
  .food {
    border-top-right-radius: 8px;
    border-bottom-right-radius: 8px;
    margin: 10px 0;
    background-color: #fff;
    .van-row {
      position: relative;
      border-bottom: none !important;
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
  .van-divider {
    border-color: transparent;
    margin: 10px 0;
  }
  .van-nav-bar__right {
    color: #3660c8;
    font-size: 14px;
  }
  h1 {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 10px;
  }
  .main {
    .company {
      font-size: 15px;
    }
    margin: 15px;
    .van-row {
      border-bottom: 1px solid #f5f5f5;
    }

    .prescription,
    .dietprescription,
    .oral,
    .extrameals,
    .exercise {
      padding: 20px 15px 0;
      border-radius: 8px;
      background-color: #fff;
      margin-bottom: 15px;
      .breakfast,
      .lunch,
      .dinner {
        padding-top: 20px;
        img {
          height: 24px;
        }
      }
      .add {
        text-align: right;
        img {
          width: 39px;
          margin: 22px 0 24px;
        }
      }
      .van-cell {
        padding: 20px 0;
        &::after {
          right: 0;
          left: 0;
        }
        .van-field__label {
          font-size: 15px;
          margin-left: 5px;
          width: 120px;
        }
      }
    }
    
    .dietprescription {
      padding-bottom: 15px;
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
}
</style>
