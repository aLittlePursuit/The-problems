> 使用pre标签v-html可以正确的解析返回数据中的回车换行符

```
<template>
    <div class="main">
        <pre v-html=""></pre>
    </div>
</template>

<style>
    .main {
        pre {
            white-space: pre-wrap;
            word-wrap: break-word;
        }
    }
</style>
```
