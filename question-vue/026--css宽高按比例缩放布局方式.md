## css宽高按比例缩放布局方式
##### 利用元素position、padding来实现宽高按比例缩放的布局
> dom

```
<template>
    <div class="wrapper">
        <div class="square">
            <img src="https://ss1.bdstatic.com/70cFvXSh_Q1YnxGkpoWK1HF6hhy/it/u=770520485,1531552880&fm=27&gp=0.jpg" width="100%" height="100%" alt="">
        </div>
    </div>
</template>
```
> js

```
<script>
    export default {}
</script>
```
> style

```
<style lang="scss" rel="stylesheet/scss">
    .wrapper {
        margin: 0 auto;
        width: 40%;
        background: orange;
        .square {
            position: relative;
            padding-bottom: 100%;
            width: 100%;
            height: 0;
            > img {
                position: absolute;
                left: 0;
                top: 0;
                object-fit: cover;  // 该属性可以确保图片展示不失真，充满容器
                object-position: center;
            }
        }
    }
</style>
```