# LocalStorage
> 在vue中定义成公共js文件来调用（例：common.js）

```
// 存数据到localstorage
export const saveLocalStorage = (key, value) => {
  localStorage.setItem(key, JSON.stringify(value))
}
// 取localStorage
export const getLocalStorage = (key) => {
  return JSON.parse(localStorage.getItem(key)) || null
}
```
> 在目标文件中直接引入方式

```
import { saveLocalStorage, getLocalStorage } from './文件路径/common'
```
> 使用方式

```
saveLocalStorage(key, value)
getLocalStorage(key)
```
