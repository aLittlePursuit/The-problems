## slot分发
> 组件test.vue

```
<template>
    <div class="test">
       <slot name='logo'></slot>
       <slot name='search'></slot>
       <slot name="edit"></slot>
       <slot name="msite-title"></slot>
       <slot name="changecity"></slot>
       <slot name="changeLogin"></slot>
    </div>
</template>
<script>
    export default {}
</script>
<style>
    ...
<style>
```

> 使用分发组件

```
<template>
    <div class="main">
        // 使用组件
        <v-test>
            // 需要展示logo就引入logo的slot
            <span slot='logo'>分发的内容logo</span>
            <span slot='edit'>分发的内容edit</span>
        </v-test>
    </div>
</template>
<script>
    import { test } from 'test.vue文件路径'
    export default {
        components: {
            'v-test': test
        }
    }
</script>
<style>
    ...
<style>
```
