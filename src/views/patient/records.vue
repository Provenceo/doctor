<template>
  <div id="records">
    <van-nav-bar title="新增病历" left-arrow @click-left="onClickLeft">
      <template #right>
        <span @click="$router.push(`/HistoricalCases/${detail.id}`)"
          >历史病例</span
        >
        <!-- HistoricalCases -->
      </template>
    </van-nav-bar>
    <div class="header">
      <van-row type="flex" align="center">
        <van-col span="3" class="avatar">
          <img
            :src="
              detail.img ? detail.img : require('@/assets/images/avatar.png')
            "
            alt=""
          />
        </van-col>
        <van-col span="21" :offset="1">
          <div class="gr">
            <span class="name">{{ detail.name }}</span>
            <van-tag plain type="primary" v-if="detail.jibing">{{
              detail.jibing
            }}</van-tag>
            <van-tag plain type="warning" v-if="detail.gwname">{{
              detail.gwname
            }}</van-tag>
          </div>
          <div>病例次数：{{ detail.blnums }}次</div>
        </van-col>
      </van-row>
    </div>
    <div class="nav">
      <div class="bt">
        <h1>病历标题</h1>
      </div>
      <van-divider
        :style="{ borderColor: 'rgba(225,225,225,.6)', padding: '0 20px' }"
      >
      </van-divider>
      <van-field
        v-model="form.title"
        label="标题"
        placeholder="例如：首次检查病历"
      />
    </div>
    <div class="main">
      <div class="information">
        <h1>基本信息</h1>
        <van-divider :style="{ borderColor: 'rgba(225,225,225,.6)' }">
        </van-divider>
        <van-row type="flex" justify="space-between" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="当前体重"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="2" :offset="5" class="company">kg</van-col>
        </van-row>
        <van-row type="flex" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="未生病前体重"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="2" :offset="5" class="company">kg</van-col>
        </van-row>
        <van-row type="flex" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="一个月前体重"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="2" :offset="5" class="company">kg</van-col>
        </van-row>
        <van-row type="flex" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="三个月前体重"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="2" :offset="5" class="company">kg</van-col>
        </van-row>
        <van-row type="flex" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="身高"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="2" :offset="5" class="company">cm</van-col>
        </van-row>
        <van-row type="flex" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="BMI"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="2" :offset="6" class="company">%</van-col>
        </van-row>
        <van-row type="flex" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="骨骼肌"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="2" :offset="5" class="company">kg</van-col>
        </van-row>
      </div>
      <div class="indicator">
        <h1>营养指标</h1>
        <van-divider :style="{ borderColor: 'rgba(225,225,225,.6)' }">
        </van-divider>
        <van-row type="flex" justify="space-between" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="钠"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="5" :offset="8" class="company">mmol/L</van-col>
        </van-row>
        <van-row type="flex" justify="space-between" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="钙"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="5" :offset="8" class="company">mmol/L</van-col>
        </van-row>
        <van-row type="flex" justify="space-between" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="钾"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="5" :offset="8" class="company">mmol/L</van-col>
        </van-row>
        <van-row type="flex" justify="space-between" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="磷"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="5" :offset="8" class="company">mmol/L</van-col>
        </van-row>
        <van-row type="flex" justify="space-between" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="CRP"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="5" :offset="10" class="company">mg/dL</van-col>
        </van-row>
        <van-row type="flex" justify="space-between" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="TBIL"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="5" :offset="10" class="company">umd/L</van-col>
        </van-row>
        <van-row type="flex" justify="space-between" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="ALB"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="2" :offset="1" class="company">g/L</van-col>
        </van-row>
        <van-row type="flex" justify="space-between" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="ALT"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="2" :offset="1" class="company">u/L</van-col>
        </van-row>
        <van-row type="flex" justify="space-between" align="center">
          <van-col span="21"
            ><van-field
              v-model="form.title"
              label="Cr"
              placeholder="请输入"
              type="number"
          /></van-col>
          <van-col span="5" :offset="10" class="company">umd/L</van-col>
        </van-row>
      </div>
      <div class="disease">
        <h1>疾病信息</h1>
        <van-divider :style="{ borderColor: 'rgba(225,225,225,.6)' }">
        </van-divider>
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
        <van-field
          readonly
          clickable
          name="picker"
          :value="form.jibing"
          label="疾病部位"
          placeholder="请选择疾病部位"
          right-icon="arrow"
          @click="showAzlx = true"
          :rules="[{ required: true, message: '请选择疾病部位！' }]"
        />
        <van-popup v-model="showAzlx" position="bottom">
          <van-picker
            show-toolbar
            :columns="Azlx"
            @confirm="onAzlxConfirm"
            @cancel="showAzlx = false"
          />
        </van-popup>
      </div>
      <div class="complication">
        <h1>并发症</h1>
        <van-divider :style="{ borderColor: 'rgba(225,225,225,.6)' }">
        </van-divider>
        <van-field name="radio" label="胸水" input-align="right">
          <template #input>
            <van-radio-group v-model="radio" direction="horizontal">
              <van-radio name="1">有</van-radio>
              <van-radio name="2">无</van-radio>
            </van-radio-group>
          </template>
        </van-field>
        <van-field name="radio" label="腹水" input-align="right">
          <template #input>
            <van-radio-group v-model="radio" direction="horizontal">
              <van-radio name="1">有</van-radio>
              <van-radio name="2">无</van-radio>
            </van-radio-group>
          </template>
        </van-field>
        <van-field name="radio" label="心包积液" input-align="right">
          <template #input>
            <van-radio-group v-model="radio" direction="horizontal">
              <van-radio name="1">有</van-radio>
              <van-radio name="2">无</van-radio>
            </van-radio-group>
          </template>
        </van-field>
        <van-field name="radio" label="肺部感染" input-align="right">
          <template #input>
            <van-radio-group v-model="radio" direction="horizontal">
              <van-radio name="1">有</van-radio>
              <van-radio name="2">无</van-radio>
            </van-radio-group>
          </template>
        </van-field>
        <van-field name="radio" label="肠梗阻" input-align="right">
          <template #input>
            <van-radio-group v-model="radio" direction="horizontal">
              <van-radio name="1">有</van-radio>
              <van-radio name="2">无</van-radio>
            </van-radio-group>
          </template>
        </van-field>
        <div class="other">其他</div>
        <van-field
          v-model="message"
          rows="3"
          autosize
          type="textarea"
          placeholder="请输入"
          class="textarea"
        />
      </div>
      <div class="inspectionreport">
        <h1 style="display:block">检查报告</h1>
        <van-uploader
          style="display:block"
          :after-read="afterRead"
          v-model="fileList"
          :before-read="beforeRead"
        >
          <img src="@/assets/images/upload.png" alt="" />
        </van-uploader>
        <van-button type="info" style="width:100%">提交</van-button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      detail: {},
      Azlx: [],
      fileList: [],
      showAzlx: false,
      message: "",
      radio: "1",
      form: {
        title: ""
      }
    };
  },
  methods: {
    afterRead(file) {
      // 此时可以自行将文件上传至服务器
      console.log(file);
    },
    beforeRead(file) {
      console.log(file);
      if (
        file.type !== "image/jpeg" &&
        file.type !== "image/gif" &&
        file.type !== "image/png" &&
        file.type !== "image/jpg"
      ) {
        this.$toast("请上传图片");
        return false;
      }
      return true;
    },
    asyncBeforeRead(file) {
      return new Promise((resolve, reject) => {
        if (
          file.type !== "image/jpeg" &&
          file.type !== "image/gif" &&
          file.type !== "image/png" &&
          file.type !== "image/jpg"
        ) {
          this.$toast("请上传图片");
          reject();
        } else {
          let img = new File(file, {
            type: file.type
          });
          resolve(img);
        }
      });
    },
    onClickLeft() {
      this.$router.go(-1); //返回上一层
    },
    onAzlxConfirm() {}
  },
  created() {
    let list = decodeURIComponent(this.$route.params.detail);
    this.detail = JSON.parse(list);
    console.log(this.detail);
  }
};
</script>

<style lang="less">
#records {
  text-align: left;
  color: #404040;
  padding-bottom: 30px;
  .van-nav-bar__left {
    .van-icon {
      color: #404040;
    }
  }
  .gr {
    margin-bottom: 10px;
    .name {
      font-size: 15px;
      font-weight: bold;
    }
  }
  h1 {
    font-size: 18px;
    font-weight: bold;
  }
  .company {
    font-size: 15px;
  }
  .van-nav-bar__right {
    color: #3660c8;
    font-size: 14px;
  }
  .header {
    color: #fff;
    padding: 25px 15px;
    background-image: linear-gradient(to right, #4589ed, #569aff);
    .van-tag--plain {
      background-color: transparent;
    }
    .van-tag--primary.van-tag--plain {
      color: #fff;
    }
    .van-tag--warning.van-tag--plain {
      color: #f7d300;
    }
  }
  .nav {
    background-color: #fff;
    padding-top: 30px;
    margin-bottom: 10px;
    h1 {
      font-size: 18px;
      margin-left: 20px;
      font-weight: bold;
    }
    .van-divider {
      margin: 20px 0;
    }
    .van-cell {
      padding: 0px 18px 20px;
      .van-field__label {
        font-size: 15px;
        margin-left: 5px;
        width: 50px;
      }
    }
  }
  .main {
    .information,
    .indicator,
    .disease,
    .complication,
    .inspectionreport {
      margin-bottom: 10px;
      background-color: #fff;
      padding: 30px 20px 0;
    }
    .complication {
      .other {
        margin: 20px 5px 0;
        font-size: 15px;
      }
      .textarea {
        margin-left: 5px;
      }
    }
    .indicator {
      .van-field__label {
        font-size: 15px;
        width: 50px;
        margin-left: 5px;
      }
    }
    .inspectionreport {
      padding-bottom: 20px;
      .van-uploader {
        margin-top: 20px;
        margin-bottom: 27px;
      }
      .van-uploader__preview {
        width: 100%;
        .van-image {
          height: 100%;
          width: 100%;
        }
      }
      .van-uploader__input-wrapper {
        width: 100%;
        img {
          width: 100%;
        }
      }
      .van-button {
        height: 50px;
        font-size: 16px;
      }
    }
    .van-divider {
      margin: 20px 0 0;
    }
    .van-row {
      border-bottom: 1px solid #f5f5f5;
    }
    h1 {
      font-size: 18px;
      font-weight: bold;
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
      }
    }
  }
}
</style>
