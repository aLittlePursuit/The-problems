## 返回顶部

```
<div @click="backTop">返回顶部</div>
backTop(){
    animate(document.body, {scrollTop: '0'}, 400,'ease-out');
}
```
