## vue在离开这个路由时清除定时任务
> js

```
export default {
    data () {
      return {
        setReveiveMsg: null
      }
    },
    mounted () {
      // 定时接受数据3秒接收一次数据
      this.setReveiveMsg = setInterval(() => {
        console.log('定时任务')
      }, 5000)
    },
    // 离开这个路由调用方法，清除定时任务
    beforeRouteLeave (to, from, next) {
      clearInterval(this.setReveiveMsg)
      next()
    }
  }
```
