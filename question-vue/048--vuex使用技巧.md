## vuex使用技巧

```
// vuex文件
store
  ├── actions.js                // 封装多个mutation操作方法
  ├── getters.js                // 对state做映射，以便读取数据
  ├── index.js                  // vuex配置文件，需全局引入
  ├── mutations.js              // 定义变量字符串
  ├── mutationTypes.js          // 存储数据的逻辑
  └── state.js                  // 存储的数据
```

```
// index.js
import Vue from 'vue'
import Vuex from 'vuex'
import * as actions from './actions'
import * as getters from './getters'
import state from './state'
import mutations from './mutations'

Vue.use(Vuex)

// 定义一个store实例
const store = new Vuex.Store({
  actions,
  getters,
  state,
  mutations
})

export default store
```

```
// state.js 存储的数据
import { loadSearch } from 'common/js/storage'

const state = {
  test: '',
  searchHistory: loadSearch()   // 从localStorage取值
}

export default state
```

```
// getters.js 对state做映射，以便读取数据
export const test = state => state.test
export const searchHistory = state => state.searchHistory
```

```
// mutation-types.js  定义变量字符串
export const SET_SEARCH_HISTORY = 'SET_SEARCH_HISTORY'
```

```
// mutations.js  存储数据的逻辑
import * as types from './mutation-types'

const mutations = {
  [types.SET_TEST] (state, query) {
    state.test = query
  },
  [types.SET_SEARCH_HISTORY] (state, query) {
    state.searchHistory = query
  }
}

export default mutations
```

```
// actions.js  封装多个mutation的操作方法
import * as types from './mutation-types'
import { saveSearch } from 'common/js/storage'

export const saveSearchHistory = ({commit}, query) => {
  commit(types.SET_SEARCH_HISTORY, saveSearch(query))
}
```


```
// template中调用方法（search.vue）
<template>
    模板
</template>

<script>
    import { mapGetters, mapMutations, mapActions } from 'vuex'
    
    export default {
        computed: {
            // 获取数据test
            ...mapGetters([
                'test'
            ])
        },
        mounted () {
            console.log(this.test)
            this.settest = '666'
            this.saveSearchHistory('搜索值')
        },
        methods: {
            // 可操作数据
            ...mapMutations({
                settest: 'SET_TEST'
            }),
            // 可操作数据
            ...mapActions([
                'saveSearchHistory'
            ])
        }
    }
</script>
```





