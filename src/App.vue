<template>
  <div id="app">
    <div class="title-bar">
      <div class="title">
        <div class="logo">
          <img src="@/assets/logo.png" alt />
        </div>
        <div class="txt">
          <button @click="close">关闭</button>
          <ul>
            <li>个性推荐</li>
            <li>歌单</li>
            <li>主播电台</li>
            <li>排行榜</li>
            <li>歌手</li>
            <li>最新音乐</li>
            <li>
              <input type="text" placeholder="搜索" />
            </li>
          </ul>
        </div>
      </div>
      <div class="window-tool">
        <div></div>
      </div>
    </div>
    <div class="content">
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
let { remote } = require("electron");
export default {
  methods: {
    close() {
      remote.getCurrentWindow().maximize();
    },
    // 防抖
    debounce(fn) {
      let timeout = null;
      const a = 2
      return function() {
        console.log(a);
        clearTimeout(timeout);
        timeout = setTimeout(() => {
          fn.apply(this, arguments);
        }, 1000);
      };
    }
  },
  mounted() {
    let win = remote.getCurrentWindow();
    win.on(
      "resize",
      this.debounce(() => {
        console.log("123");
      })
    );
  }
};
</script>

<style lang="scss">
@import url("./assets/reset.css");

#app {
  .title-bar {
    background-color: #f9f9f9;
    .title {
      -webkit-app-region: drag;
      display: flex;
      justify-content: space-between;
      .logo {
        flex: 1;
        margin-right: 90px;
        img {
          width: 50px;
          height: 50px;
        }
      }
      .txt {
        flex: 9;
        ul {
          display: flex;
          flex-wrap: nowrap;
          justify-content: space-around;
          // display: inline-block;
          li {
            float: left;
            color: #646464;
            font-size: 14px;
            line-height: 50px;
          }
        }
      }
    }
  }
}
</style>
