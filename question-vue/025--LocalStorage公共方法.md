# LocalStorage


```
使用方法:
<template>
    <div class="main" @click="save">
      ...
    </div>
</template>
<script>
    // 引入要使用的js中的某个或多个方法
    import { saveLocalStorage, getLocalStorage } from '@/utils/LocalStorage'
    export default {
        data () {
          openId: ''  
        },
        created () {
            // 从localStoragfe中取值
            if (getLocalStorage('openId') !== null) {
                this.openId = getLocalStorage('openId')
            }
        },
        methods: {
            // 给localStoragfe存储值
            save () {
                saveLocalStorage('openId', '465464654654321313')
            }
        }
    }
</script>
<style>
    ...
</style>
```

> LocalStorage.js

```
// 存数据到localstorage
export const saveLocalStorage = (key, value) => {
  localStorage.setItem(key, JSON.stringify(value))
}
// 取localStorage
export const getLocalStorage = (key) => {
  return JSON.parse(localStorage.getItem(key)) || null
}
// 删除某个localStorage
export const removeLocalStorage = (key) => {
  localStorage.removeItem(key)
}
```
