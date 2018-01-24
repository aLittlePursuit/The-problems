# main.js

```
import Vue from 'vue'
import App from './App'

// 路由
import router from './router'                           // 引入router.js文件

// 状态管理
import store from './store/'                            // 引入store文件夹下的index.js文件

// mint-ui库
import Mint from 'mint-ui'                              // 引入mint-ui库

// 视频插件
import VueVideoPlayer from 'vue-video-player'           // 引入视频插件

// css
import '@/assets/css/reset.css'                         // 格式化初始样式
import '@/assets/css/iconfont.css'                      // 字体图标样式
import 'mint-ui/lib/style.css'                          // mint-ui 样式

// 全局引入自定义组件
import avatar from '@/components/header/avatar'
// 全局注册自定义组件（每个页面都可以直接使用）<v-avatar></v-avatar>
Vue.component('v-avatar', avatar)

Vue.use(VueVideoPlayer)
Vue.use(Mint)

Vue.config.productionTip = false

/* eslint-disable no-new */
new Vue({
  el: '#app',
  template: '<App/>',
  components: { App },
  store,                                                // 根组件注入--vuex
  router                                                // 根组件注入--vueRouter
}) 

```
