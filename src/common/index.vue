<template>
  <div class="page">
      <router-view></router-view>
    <div class="nav-footer" v-if="$route.meta.navShow">
      <footer>
        <router-link
          v-for="(item, index) in navList"
          :to="item.path"
          :key="index"
          v-bind:class="{ active: activeRoute == item.path }"
        >
          <div :class="'tab-' + index"></div>
          <p v-text="item.name"></p>
        </router-link>
      </footer>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      navList: [
        {
          path: "/home",
          name: "首页"
        },
        {
          path: "/patient",
          name: "患者"
        },
        {
          path: "/consultant",
          name: "营养顾问"
        },
        {
          path: "/my",
          name: "我的"
        }
      ]
    };
  },
  computed: {
    activeRoute() {
      return this.$route.path;
    }
  },
  methods: {}
};
</script>

<style lang="less">
@import "~@/styles/index.less";
@import "~@/styles/variable.less";
.nav-footer {
  position: fixed;
  left: 0px;
  bottom: 0px;
  width: 100%;
  .h(98);
  background: @tab-general-bg-color;
  display: block;
  footer {
    font-size: 0;
    border-top: 1px solid #e7e7e7;
    border-bottom: 1px solid #f8f8f8;
    .pt(10);
    line-height: 1.2;
    width: 100%;
    .h(98);
    display: flex;
    a {
      text-decoration: none;
      color: @base-font-color;
      -webkit-box-flex: 1;
      -moz-box-flex: 1;
      -webkit-flex: 1;
      -ms-flex: 1;
      flex: 1;
      text-align: center;
      box-sizing: border-box;
      display: block;
      .fs(22);
      .tab-0,
      .tab-1,
      .tab-2,
      .tab-3 {
        display: inline-block;
        .h(42);
        .w(42);
        background-size: cover;
      }
      .tab-0 {
        background-image: url("~@/assets/images/doctor202007171725 _36.png");
      }
      .tab-1 {
        background-image: url("~@/assets/images/doctor202007171725 _4.png");
      }
      .tab-2 {
        background-image: url("~@/assets/images/doctor202007171725 _17.png");
      }
      .tab-3 {
        background-image: url("~@/assets/images/doctor202007171725 _41.png");
      }
      &:hover {
        text-decoration: none;
      }
      &.router-link-active.active {
        .tab-0 {
          background-image: url("~@/assets/images/doctor202007171725 _35.png");
        }
        .tab-1 {
          background-image: url("~@/assets/images/huanzhe.png");
        }
        .tab-2 {
          background-image: url("~@/assets/images/yisheng.png");
        }
        .tab-3 {
          background-image: url("~@/assets/images/doctor202007171725 _40.png");
        }
      }
    }
    p {
      margin: 0;
    }
  }
}
</style>
