# vuex

```
安装插件：
npm install vuex --save
```

> store文件夹

```
vuex文件建立单独文件夹store，下有index.js，state.js，mutations.js
state.js:      存储需要统一管理的内容
mutations.js： 改变存储内容的方法

```

> index.js

```
import Vue from 'vue'
import Vuex from 'vuex'
import state from './state.js'
import mutations from './mutations.js'

Vue.use(Vuex)

// 定义一个store实例
const store = new Vuex.Store({
  state,
  mutations
})

export default store
```

> state.js

```
const state = {
  stateMain: {page: null, scrollY: null, leaveTime: null}
}

export default state
```

> mutations.js

```
const SAVE_STATE = 'SAVE_STATE'                       // 保存浏览数据和高度
const SAVE_SINGLE = 'SAVE_SINGLE'                     // 保存单一字符串
const RESET_STATE = 'RESET_STATE'                     // 重置浏览数据和高度
const RESET_STATE_SINGLE = 'RESET_STATE_SINGLE'       // 重置单一字符串浏览数据

const mutations = {
  [SAVE_STATE] (state, obj) {
    state[obj.name].page = obj.page
    state[obj.name].scrollY = obj.scrollY
    state[obj.name].leaveTime = obj.leaveTime
  },
  [SAVE_SINGLE] (state, obj) {
    state[obj.name] = obj.value
  },
  [RESET_STATE] (state, arrName) {
    for (let i = 0; i < arrName.length; i++) {
      state[arrName[i]].page = null
      state[arrName[i]].scrollY = null
      state[arrName[i]].leaveTime = null
    }
  },
  [RESET_STATE_SINGLE] (state, arrName) {
    for (let i = 0; i < arrName.length; i++) {
      state[arrName[i]] = null
    }
  }
}

export default mutations
```

> vue文件中使用方法

```
<template>
    <div class="main" ref="main">
        ...
    </div>
</template>

<script>
    import { mapState, mapMutations } from 'vuex'
    export default {
        data () {
            return {
                main: {data: [], page: 1, allLoaded: false, code: null}
            }
        },
        beforeRouteLeave (to, from, next) {
            const obj = {
                name: 'stateMain',
                page: this.main.page,
                scrollY: this.$refs.main.scrollTop,
                leaveTime: Date.parse(new Date())
            }
            this.SAVE_STATE(obj)
            next()
        },
        mounted () {
            // 引入这个对象后，可以直接使用这个对象或值
            console.log(this.stateMain)  
        },
        computed: {
            // 引入vuex存储信息对象
            ...mapState(['stateMain'])
        },
        methods: {
            // 引入vuex全局变量方法(对应同名方法)
            ...mapMutations(['SAVE_STATE'])
        }
    }
</script>

<style>
    ...
</style>
```


