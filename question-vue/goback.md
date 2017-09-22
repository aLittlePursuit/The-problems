## 后退一步

```
<div @click="$router.go(-1)">返回</div>
```
> 当前页面http://localhost:8080/currentPage

```
<template>
    <div class="current-page">
      <div>这个页面是当前页面</div>
      // 下一级页面跳转入口
      <router-view></router-view>
    </div>
</template>
```
> 下一级页面http://localhost:8080/currentPage/nextPage

```
<template>
    <div class="next-page">
        <div @click="$router.go(-1)">返回</div>
        <div>下一级页面</div>
    </div>
</template>
```
注：父子级页面之间nextPage返回currentPage，currentPage页面完全无操作，created()和mounted()完全不会重新调用,如果currentPage有选项操作等返回下级页面返回这个页面状态依旧会保留。
> 当前页面http://localhost:8080/currentPage

```
<template>
    <div class="current-page">
      <div>这个页面是当前页面</div>
    </div>
</template>
```
> 同级页面http://localhost:8080/nextPage

```
<template>
    <div class="next-page">
        <div @click="$router.go(-1)">返回</div>
        <div>下一级页面</div>
    </div>
</template>
```
注：兄弟级页面之间nextPage返回currentPage，currentPage页面会调用created()和mounted()。
