> better-scroll插件样式定义（横向滚动）

```
// template
<template>
    <div class="wrap clearfix" ref="wrap">
        <ul class="list">
            <li class="list-cell"></li>
            <li class="list-cell"></li>
            <li class="list-cell"></li>
            <li class="list-cell"></li>
            <li class="list-cell"></li>
            <li class="list-cell"></li>
            <li class="list-cell"></li>
            ...
        </ul>
    </div>
</template>

```

```
// script
<script>
    import BScroll from 'better-scroll'
    export default {
        mounted () {
            addScrollX(this.$refs.wrap)
        },
        methods: {
            addScrollX (el) {
                const scroll = new BScroll(el, {
                scrollX: true,
                scrollY: false,
                probeType: 3,
                click: true,
                bounceTime: 600
              })
              scroll.refresh()
            }
        }
    }
</script>
```

```
// style
<style lang="scss" rel="stylesheet/scss">
    // 清除浮动
    .clearfix:before,
    .clearfix:after {
        display: table;
        content: " ";
    }
    .clearfix:after {
        clear: both;
    }
    .wrap {
        overflow: hidden;
        .list {
            float: left;   // 重点
            write-space: nowrap;  // 重点
            .list-cell {
                display: inline-block;
                padding-right: 10px;
                width: 100px;
                height: 100px;
                background: red;
            }
        }
    }
</style>
```

