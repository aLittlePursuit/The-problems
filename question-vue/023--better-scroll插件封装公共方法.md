## better-scroll插件封装方法
> scroll.js


```
使用方法:
<template>
    <div class="main" ref="main">
      <ul>
        <li></li>
        <li></li>
        <li></li>
        ...
      </ul>
    </div>
</template>
<script>
    // 引入要使用的js中的某个或多个方法
    import { addScrollBounce } from '@/utils/scroll'
    export default {
        mounted () {
            this.$nextTick(() => {
                addScrollBounce(this.$refs.main)
            })
        }
    }
</script>
<style>
    .main {
        width: 100%;
        height: 300px;
        overflow: hidden;
    }
</style>
```


```
import BScroll from 'better-scroll'

// y轴支持回弹
export const addScrollBounce = (el) => {
  const scroll = new BScroll(el, {
    probeType: 3,
    click: true,
    bounceTime: 600   // 回弹时间
  })
  scroll.refresh()
}

// y轴不支持回弹
export const addScroll = (el) => {
  const scroll = new BScroll(el, {
    probeType: 3,
    click: true,
    bounce: false
  })
  scroll.refresh()
}

// x轴支持回弹
export const addScrollBounceX = (el) => {
  const scroll = new BScroll(el, {
    scrollX: true,
    scrollY: false,
    probeType: 3,
    click: true,
    bounceTime: 600   // 回弹时间
  })
  scroll.refresh()
}

// x轴不支持回弹
export const addScrollX = (el) => {
  const scroll = new BScroll(el, {
    scrollX: true,
    scrollY: false,
    probeType: 3,
    click: true,
    bounce: false
  })
  scroll.refresh()
}
```
