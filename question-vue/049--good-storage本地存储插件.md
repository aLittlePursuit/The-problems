## good-storage本地存储插件

```
// 安装good-storage插件
npm install good-storage --save

// storage.js 专门处理本地存储的逻辑
import storage from 'good-storage'

const SEARCH_KEY = '__search__'
const SEARCH_MAX_LENGTH = 10

// 数组插入方法
const insertArray = (arr, val, compare, maxLen) => {
  // 查看数组中是否包含要检索的内容findIndex  es6语法查找数组元素并返回index
  const index = arr.findIndex(compare)
  // 如果是数组第一个元素，无操作
  if (index === 0) {
    return
  }
  // 如果存在且不是第一个元素，则删除这个元素
  if (index > 0) {
    arr.splice(index, 1)
  }
  // 将这个元素添加至数组头部
  arr.unshift(val)
  // 如果有最大存储限制，并且数组长度超出，则删除最后一个元素
  if (maxLen && arr.length > maxLen) {
    arr.pop()
  }
}

// 删除数组元素方法
const deleteFromArray = (arr, compare) => {
  // 查看数组中是否包含要检索的内容findIndex  es6语法查找数组元素并返回index
  const index = arr.findIndex(compare)
  // 如果存在这个元素则删除
  if (index > -1) {
    arr.splice(index, 1)
  }
}

// 保存搜索内容
export const saveSearch = (query) => {
  // 意思是获取本地存储，如果没有则为空数组
  let searches = storage.get(SEARCH_KEY, [])
  // 将搜索值插入数组searches
  insertArray(searches, query, (item) => {
    return item === query
  }, SEARCH_MAX_LEN)
  // 存入localstorage
  storage.set(SEARCH_KEY, searches)
  // 返回这个数组
  return searches
}

// 删除搜索内容
export const deleteSearch = (query) => {
  // 意思是获取本地存储，如果没有则为空数组
  let searches = storage.get(SEARCH_KEY, [])
  // 删除存储中的值
  deleteFromArray(searches, (item) => {
    return item === query
  })
  // 存入localstorage
  storage.set(SEARCH_KEY, searches)
  // 返回这个数组
  return searches
}

// 清除localstorage
export const clearSearch = () => {
  // 删除这个localstorage
  storage.remove(SEARCH_KEY)
  // 返回空数组
  return []
}

// 获取localstorage搜素值
export const loadSearch = () => {
  return storage.get(SEARCH_KEY, [])
}
```
