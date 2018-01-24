## stick-footer布局方式
##### 注：这里主要针对移动端，当内容不能撑满一屏时，关闭按钮显示在屏幕的最底部，当内容超出一屏时，关闭按钮在显示在内容的最底部
> dom

```
<template>
    <div class="wrapper">
        <div class="stick-wrapper">
            <div class="stick-main">
                <p>stick footer</p>
            </div>
        </div>
        <div class="stick-close">x</div>
    </div>
</template>
```
> js

```
export default {}
```
> style 

```
<style>
    .wrapper {
        position: fixed;
        top: 0;
        left: 0;
        bottom: 0;
        width: 100%;
        overflow: auto;
    }
    .stick-wrapper {
        min-height: 100%;
        background: orange;
    }
    .stick-main {
        padding-bottom: 50px;
        background: blue;
    }
    .stick-main > p {
        margin: 0;
        height:1000px;
        background: purple;
    }
    .stick-close {
        margin: -60px auto 0 auto;
        text-align: center;
        line-height: 30px;
        width: 30px;
        height: 30px;
        font-size: 30px;
    }
</style>
```


