## 038--vue-social-sharing分享和vue-clipboard2复制粘贴插件使用
> 安装和引入

```
安装vue-social-sharing插件
npm install --save vue-social-sharing
cnpm install --save vue-social-sharing

安装vue-clipboard2插件
npm install --save vue-clipboard2
cnpm install --save vue-clipboard2

全局引入插件在main.js
import SocialSharing from 'vue-social-sharing'
import VueClipboard from 'vue-clipboard2'

使用插件
Vue.use(SocialSharing)
Vue.use(VueClipboard)
```

> 封装成分享组件share.vue

```
<template>
    <div class="share-wrap" v-if="showShare">
      <div class="share-main clearfix">
        <div class="share-title">分享给好友</div>
        <div class="share-content">
          <social-sharing :networks="overriddenNetworks" :url="currentLink" :title="title" inline-template>
            <div class="share-list">
              <div class="share-cell">
                <network network="weibo">
                  <i class="weibo-icon iconfont iconfont-weibo"></i><br>
                  <span class="weibo-name">新浪微博</span>
                </network>
              </div>
              <div class="share-cell">
                <network network="qq">
                  <i class="weibo-icon iconfont iconfont-qq"></i><br>
                  <span class="weibo-name">qq好友</span>
                </network>
              </div>
            </div>
          </social-sharing>
        </div>
        <!--由于在分享组件中无法添加click事件，所以单独布局、样式调整可点击的区域实现其他功能-->
        <div class="share-content share-content-add">
          <div class="share-list">
            <!--<div class="share-cell">-->
              <!--<i class="weibo-icon iconfont iconfont-wechat"></i><br>-->
              <!--<span class="weibo-name">微信</span>-->
            <!--</div>-->
            <div class="share-cell" v-clipboard:copy="currentLink" v-clipboard:success="onCopy" v-clipboard:error="onError">
              <i class="weibo-icon iconfont iconfont-link"></i><br>
              <span class="weibo-name">复制链接</span>
            </div>
          </div>
        </div>
        <div class="share-cancel" @click="hideShare">取消</div>
      </div>
      <mt-popup class="class-popup" :modal="false" v-model="copyInfo.isVisible" position="top">{{ copyInfo.hint }}</mt-popup>
    </div>
</template>

<script>
  export default {
    props: {
      showShare: {
        type: Boolean,
        default: false
      },
      title: {
        type: String,
        default: '我的分享'
      }
    },
    data () {
      return {
        currentLink: '',
        encodeCrrentLink: '',
        sharerLink: '',
        overriddenNetworks: {},
        copyInfo: {
          isVisible: false,
          hint: ''
        }
      }
    },
    created () {
      // 获取当前页面地址并赋值
      this.currentLink = window.location.href + '#share'
      // encodeURIComponent将//解码成%2F%2F形式（模式如此,需要跟微博/qq页面地址做区分）
      this.encodeCrrentLink = encodeURIComponent(this.currentLink)
      // 新浪微博分享地址
      this.sharerWeiboLink = `http://service.weibo.com/share/share.php?url=${this.encodeCrrentLink}&title=${this.title}#_loginLayer_1518492987727`
      // 腾讯qq分享地址
      this.sharerQQLink = `http://connect.qq.com/widget/shareqq/index.html?url=${this.encodeCrrentLink}&title=${this.title}`
      // 自定义分享列表
      this.overriddenNetworks = {
        'weibo': {
          'sharer': this.sharerWeiboLink,
          'type': 'popup'
        },
        'qq': {
          'sharer': this.sharerQQLink,
          'type': 'popup'
        }
      }
    },
    watch: {
      'copyInfo.isVisible': function (val) {
        if (val) {
          setTimeout(() => {
            this.copyInfo.isVisible = false
          }, 2000)
        }
      }
    },
    methods: {
      hideShare () {
        this.$emit('hideShareLayer', false)
      },
      onCopy: function (e) {
        this.copyInfo.isVisible = true
        this.copyInfo.hint = '复制成功'
      },
      onError: function (e) {
        this.copyInfo.isVisible = true
        this.copyInfo.hint = '复制失败'
      }
    }
  }
</script>

<style lang="scss" rel="stylesheet/scss">
  @import "src/assets/css/global.scss";

  .share-wrap {
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0,0,0,.2);
    z-index: 1006;
    .share-main {
      position: absolute;
      left: 0;
      bottom: 0;
      width: 100%;
      background: $white;
      .share-title {
        text-align: center;
        line-height: 44px;
        height: 44px;
        color: $dark-text;
        border-bottom: 1px solid $light-line;
      }
      .share-content {
        display: inline-block;
        width: 66.666666%;
        &.share-content-add {
          float: right;
          width: 33.333333%;
        }
        .share-list {
          display: flex;
          padding: 20px 0;
          .share-cell {
            flex: 1;
            text-align: center;
            .weibo-icon {
              display: inline-block;
              margin-bottom: 8px;
              text-align: center;
              line-height: 40px;
              width: 40px;
              height: 40px;
              border-radius: 50%;
              color: $white;
              font-size: 18px;
              &.iconfont-weibo {
                background: #df4c4e;
              }
              &.iconfont-qq {
                background: #2b8dec;
              }
              &.iconfont-wechat {
                background: #3db134;
              }
              &.iconfont-link {
                background: #cad4df;
              }
            }
            .weibo-name {
              display: inline-block;
              color: $dark-text;
              font-size: 14px;
            }
          }
        }
      }
      .share-cancel {
        text-align: center;
        line-height: 44px;
        height: 44px;
        color: $white;
        background: $green;
      }
    }
    .class-popup {
      text-align: center;
      line-height: 44px;
      width: 100%;
      height: 44px;
      color: $white;
      background: rgba(0,0,0,.4);
    }
  }
</style>
```

> 项目中使用分享组件


```
<template>
    <div>
        <div @click="showShare = true">分享</div>
        <!--分享组件-->
        <yz-share :show-share="showShare" title="分享-直播" @hideShareLayer="hideShareLayer"></yz-share>
    </div>
</template>

<script>
    export default {
        data () {
            return {
                showShare: false
            }
        },
        methods: {
            // 隐藏分享层
            hideShareLayer (data) {
                this.showShare = data
            }
        }
    }
</script>

<style lang="scss" rel="stylesheet/scss">

</style>
```

