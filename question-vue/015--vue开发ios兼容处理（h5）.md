##  在ios设备上滚动生涩处理

```
<style>
    // ios采用上述样式时，会在滚动情况下生成滚动条，无滚动时隐藏滚动条
    // 有些地方需要将滚动条隐藏处理，例如，自定义滚动组件中...
    .scroll-cell {
      flex: 1;
      background: $white;
      overflow: hidden;
      .col {
        /*width: 100%;*/
        margin-right: -11px;  // 负margin是为了将ios生成的滚动条撑到显示区域外面，隐藏掉(ios不显示滚动条)
        height: 252px;
        overflow: auto;
        -webkit-overflow-scrolling: touch; // 该属性会调用ios原生的滚动并且给设备硬件加速
        color: $dark-text;
        background: $white;
        @include scrollHide;
        > ul {
          margin: 0;
          padding: 107px 0;
          padding-right: 11px;  // 抵消前面的负margin(ios不显示滚动条)
          list-style: none;
          > li {
            text-align: center;
            line-height: 36px;
            height: 36px;
            overflow: hidden;
          }
        }
      }
    }
</style>
```

#### 注：需要注意的地方是，在使用该属性的时候尽量避免使用fixed定位，在ios设备上会产生不可避免的bug，如滚动回弹效果会使fixed元素定位不准（跟着一起晃动）,而且偶尔会出现滚动卡死现象，因此在移动端开发页面布局中一开始就应该避免使用fixed，可以使用main包裹header、content、footer,样式如下：


```
<template>
  <div class="main">
    <div class="header"></div>
    <div class="content"></div>
    <div class="footer"></div>
  </div>
</template>
<style lang="scss" rel="stylesheet/scss" scoped>
    @import "mixin.scss文件路径";   // 引入mixin.scss
    html, body {
        width: 100%;
        height:: 100%;
    }
    .main {
        position: relative;
        padding: 40px 0 50px 0;
        width: 100%;
        height: 100%;
        .header {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 40px;
            background: red;
        }
        .content {
            width: 100%;
            height: 100%;
            overflow: auto;
            -webkit-overflow-scrolling: touch;
            @include scrollHide;
        }
        .footer {
            position: absolute;
            left: 0;
            bottom: 0;
            width: 100%;
            height: 50px;
            background: blue;
        }
    }
</style>
```

> mixin.scss

```
// 滚动条样式(显示)
@mixin scrollShow {
  &::-webkit-scrollbar {
    width: 3px;
  }
  &::-webkit-scrollbar-thumb {
    background: $line-dark;
  }
  &::-webkit-scrollbar-track-piece {
    background: transparent;
  }
}

// 滚动条样式(隐藏)
@mixin scrollHide {
  &::-webkit-scrollbar {
    display: none;
  }
}
```



