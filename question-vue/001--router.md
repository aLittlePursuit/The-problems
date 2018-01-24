# router.js

```
安装插件：
npm install vue-router --save
```

```
import routes from './routes/'                 // 引入routes文件夹下的index.js文件
import VueRouter from 'vue-router'
import { Toast } from 'mint-ui'
import { getLocalStorage } from '@/utils/common'

const router = new VueRouter({
  mode: 'history',
  linkActiveClass: 'active',
  routes
})

// 添加一个全局的前置钩子函数，这个函数会在路由切换开始时调用。调用发生在整个切换流水
// 线之前。如果此钩子函数拒绝了切换，整个切换流水线根本就不会启动。
router.beforeEach((to, from, next) => {
  // 在进入这个路由的时候先判断这个路由是否需要登录,如需登录则判断是否登录
  // 未登录直接跳转 getLocalStorage('openId')是否登录过的标识
  if (to.meta.isNeedLogin) {
    if (getLocalStorage('openId')) {
      next()
    } else {
      setTimeout(() => {
        Toast('此页面需要登录')
        setTimeout(() => {
          next('/main/login')
        }, 2000)
      }, 500)
    }
  } else {
    next()
  }
})

export default router

```
