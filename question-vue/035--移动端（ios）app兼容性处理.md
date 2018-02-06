
## h5开发移动端（ios）浏览器和app兼容性处理
> 浏览器和app都存在页面系统自有的页面回弹效果，并且浏览器和app回弹方式存在视觉上的差异，都会给用户带来不好的体验

1、ios浏览器

注：在布局方式中不要使用fixed去定位元素，由于在滚动元素滚动到底部继续向下执行滚动手势的时候，我们使用fixed定位的元素看着没有任何位移，实际上body元素是随着手势做了向上位移，当位移没有结束的时候会出现定位偏差，主管展示上我们继续滑动页面会出现假卡死现象知道body元素回归原位为止


```
// 避免使用的布局方式
<template>
    <div class="main">
        <!--header--fixed定位至顶部-->
        <div class="header"></div>
        <!--content--fixed定位至中间区域-->
        <div class="content">
            <!--滚动区域overflow: auto或scroll-->
        </div>
        <!--footer--fixed定位至底部-->
        <div class="footer"></div>
    </div>
</template>

<style lang="scss" rel="stylesheet/scss" scoped>
    html, body {
        height: 100%;
    }
    .main {
        height: 100%;
        .header {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 50px;
            background: red;
        }
        .content {
            position: fixed;
            top: 50px;
            left: 0;
            bottom: 50px;
            width: 100%;
            background: yellow;
            overflow: auto;
        }
        .footer {
            position: fixed;
            left: 0;
            bottom: 0;
            width: 100%;
            height: 50px;
            background: red;
        }       
    }
</style>
```


```
// 建议使用的布局方式
<template>
    <div class="main">
        <!--header--absolute定位至顶部-->
        <div class="header"></div>
        <!--content--撑满屏幕-->
        <div class="content">
            <!--滚动区域overflow: auto或scroll-->
            <div class="scroll-area"></div>    
        </div>
        <!--footer--absolute定位至底部-->
        <div class="footer"></div>
    </div>
</template>

<style lang="scss" rel="stylesheet/scss" scoped>
    html, body {
        height: 100%;
    }
    .main {
        position: relative;
        height: 100%;
        .header {
            position: absolute;
            top: 0;
            left: 0;
            width: 100%;
            height: 50px;
            background: red;
        }
        .content {
            padding: 50px 0;
            height: 100%;
            .scroll-area {
                height: 100%;
                overflow: auto;
                background: yellow;
            }
        }
        .footer {
            position: absolute;
            left: 0;
            bottom: 0;
            width: 100%;
            height: 50px;
            background: red;
        }       
    }
</style>
```

1、ios打壳app

```
// 在壳文件中配置属性，屏蔽回弹即可（对布局方式不存在影像）
<preference name="webviewbounce" value="false" />
<preference name="DisallowOverscroll" value="true" />
<preference name="UIWebViewBounce" value="false" />

```
