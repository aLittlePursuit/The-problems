## vue点击切换tab

```
<template>
    <div class="tab">
        <div class="tab-cell" :class="{active: changeType === 'weibo'}" @click="changeTab('weibo')">动态</div>
        <div class="tab-cell" :class="{active: changeType === 'articles'}" @click="changeTab('articles')">圈子</div>
        <div class="tab-cell" :class="{active: changeType === 'live'}" @click="changeTab('live')">直播</div>
        <div class="tab-cell" :class="{active: changeType === 'question'}" @click="changeTab('question')">问答</div>
      </div>
</template>
```

```
<script>
    export default {
        methods: {
            // tab切换方法，切换不同的接口请求数据，渲染页面
            changeTab (type) {
                this.changeType = type
            }
        }
    }
</script>
```

```
<style lang="scss" rel="stylesheet/scss" scoped>
  .tab {
      display: flex;
      line-height: 50px;
      height: 50px;
      font-size: 18px;
      border-bottom: 1px solid $line-light;
      background: $white;
      .tab-cell {
        flex: 1;
        position: relative;
        text-align: center;
        &.active {
          color: $green;
          &:before {
            position: absolute;
            left: 10%;
            bottom: 0;
            content: '';
            width: 80%;
            height: 2px;
            background: $green;
          }
        }
      }
    }
</style>
```

