<template>
  <div id="addPatient">
    <van-nav-bar
      title="新增患者"
      left-arrow
      @click-left="onClickLeft"
      class="nav"
    />
    <div class="header">
      <van-form @submit="onSubmit">
        <van-field
          v-model="form.name"
          name="姓名"
          label="姓名"
          placeholder="请输入患者姓名"
          :rules="[{ required: true, message: '请填写患者姓名！' }]"
        />
        <van-field name="radio" label="性别">
          <template #input>
            <van-radio-group v-model="form.sex" direction="horizontal">
              <van-radio name="1">男</van-radio>
              <van-radio name="2">女</van-radio>
            </van-radio-group>
          </template>
        </van-field>
        <van-field
          readonly
          clickable
          :value="form.birthday"
          name="calendar"
          label="出生日期"
          placeholder="请选择出生日期"
          right-icon="arrow"
          @click="showCalendar = true"
          :rules="[{ required: true, message: '请选择出生日期！' }]"
        />
        <van-popup v-model="showCalendar" position="bottom">
          <van-datetime-picker
            v-model="value"
            type="date"
            title="选择出生日期"
            :min-date="minDate"
            @confirm="onConfirm"
            @cancel="showCalendar = false"
          />
        </van-popup>
        <van-field
          v-model="form.tel1"
          name="本人电话"
          label="本人电话"
          :maxlength="11"
          placeholder="请输入患者本人电话"
          type="tel"
          :rules="[
            { required: true, message: '请填写患者手机号码！' },
            { pattern: /^1[3456789]\d{9}$/, message: '手机号码格式错误！' }
          ]"
        />
        <van-field
          v-model="form.tel2"
          name="家属电话"
          label="家属电话"
          :maxlength="11"
          placeholder="请输入患者家属电话"
          type="tel"
          :rules="[
            { required: true, message: '请填写家属手机号码！' },
            { pattern: /^1[3456789]\d{9}$/, message: '手机号码格式错误！' }
          ]"
        />
        <!-- <van-field
          readonly
          clickable
          label="身份证号"
          :value="form.idcard"
          @touchend.native.stop="idcard = true"
          placeholder="请输入患者身份证号"
          :rules="[
            { required: true, message: '请填写患者身份证号！' },
            {
              pattern: /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/,
              message: '身份证号格式错误！'
            }
          ]"
        />
        <van-number-keyboard
          v-model="form.idcard"
          :show="idcard"
          :maxlength="18"
          extra-key="X"
          @blur="idcard = false"
        /> -->
        <van-field
          v-model="form.idcard"
          name="身份证号"
          label="身份证号"
          :maxlength="18"
          placeholder="请输入患者身份证号"
          :rules="[
            { required: true, message: '请填写患者身份证号！' },
            {
              pattern: /(^\d{15}$)|(^\d{18}$)|(^\d{17}(\d|X|x)$)/,
              message: '身份证号格式错误！'
            }
          ]"
        />
        <van-field
          v-model="form.addr1"
          name="家庭地址"
          label="家庭地址"
          placeholder="请输入患者家庭地址"
        />
        <van-field
          v-model="form.addr2"
          name="常住地址"
          label="常住地址"
          placeholder="请输入患者常住地址"
        />
        <van-field
          readonly
          clickable
          name="picker"
          :value="form.jibing"
          label="癌症类型"
          placeholder="请选择癌症类型"
          right-icon="arrow"
          @click="showAzlx = true"
          :rules="[{ required: true, message: '请选择癌症类型！' }]"
        />
        <van-popup v-model="showAzlx" position="bottom">
          <van-picker
            show-toolbar
            :columns="Azlx"
            @confirm="onAzlxConfirm"
            @cancel="showAzlx = false"
          />
        </van-popup>
        <van-field name="yygw" label="是否选择营养顾问" class="yygw">
          <template #input>
            <van-radio-group v-model="form.gwid" direction="horizontal">
              <van-radio name="1">是</van-radio>
              <van-radio name="0">否</van-radio>
            </van-radio-group>
          </template>
        </van-field>
        <van-field
          readonly
          clickable
          name="picker"
          :value="form.gwname"
          label="营养顾问"
          placeholder="请选择营养顾问"
          @click="showYygw = true"
          v-if="form.gwid === '1'"
          right-icon="arrow"
        />
        <van-popup v-model="showYygw" position="bottom">
          <van-picker
            show-toolbar
            :columns="Yygw"
            @confirm="onYygwConfirm"
            @cancel="showYygw = false"
          />
        </van-popup>
        <div class="save">
          <div class="code"><i></i> 保存自动生成二维码</div>
          <van-button block type="info" native-type="submit">
            保存
          </van-button>
        </div>
      </van-form>
    </div>
  </div>
</template>

<script>
import { addPatient } from "@/apis/patient";
export default {
  data() {
    return {
      idcard: false,
      showCalendar: false,
      showYygw: false,
      showAzlx: false,
      Azlx: [],
      Yygw: [],
      minDate: new Date(1970, 1, 1),
      value: new Date(),
      form: {
        action: "add",
        name: "",
        sex: "1",
        birthday: "",
        tel1: "",
        tel2: "",
        idcard: "",
        addr1: "",
        addr2: "",
        jibing: "",
        gwid: "0",
        gwname: ""
      }
    };
  },
  methods: {
    onInput(value) {
      this.$toast(value);
    },
    onDelete() {
      this.$toast("删除");
    },
    onClickLeft() {
      this.$router.go(-1); //返回上一层
    },
    onConfirm(date) {
      this.form.birthday = `${date.getFullYear()}/${date.getMonth() +
        1}/${date.getDate()}`;
      this.showCalendar = false;
    },
    onAzlxConfirm(data) {
      this.form.jibing = data.title;
      console.log(data);
      this.showAzlx = false;
    },
    onYygwConfirm(data) {
      this.form.gwname = data.name;
      console.log(data);
      this.showYygw = false;
    },
    onSubmit() {
      console.log(this.form);
      addPatient(this.form)
        .then(res => {
          this.$toast("新建成功");
          this.$router.push('/patient')
        })
        .catch(err => {
          this.$toast(err.msg);
        });
    },

    LoadPatient() {
      addPatient()
        .then(res => {
          this.Azlx = res.data.jibing;
          this.Azlx.forEach(item => {
            console.log(item);
            item.text = item.title;
          });
          this.Yygw = res.data.guwen;
          this.Yygw.forEach(item => {
            console.log(item);
            item.text = item.name;
          });
        })
        .catch(err => {
          this.$toast(err.msg);
        });
    }
  },
  mounted() {
    this.LoadPatient();
  },
  watch: {
    "form.gwid": {
      deep: true,
      handler: function(newV, oldV) {
        if (newV === "0") {
          this.form.gwname = "";
        }
      }
    }
  }
};
</script>

<style lang="less">
#addPatient {
  padding-bottom: 60px;
  .van-nav-bar{
    background-color: #ededed;
  }
  .nav {
    .van-icon {
      color: #404040;
    }
  }
  .yygw {
    &.van-cell {
      .van-cell__title {
        width: 150px;
      }
    }
  }

  .save {
    background-color: #fff;
    padding: 30px 20px;
    margin: 16px 0;
    text-align:left;
     .code {
      margin-bottom: 15px;
      font-size: 16px;
      font-weight: 500;
      i {
        display: inline-block;
        width: 13px;
        height: 13px;
        border-radius: 50%;
        background-color: #fa5b57;
      }
    }
  }
}
</style>
