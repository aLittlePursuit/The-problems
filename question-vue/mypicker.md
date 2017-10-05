## mypicker
### 自定义二级联动组件，可扩展多列
> template

```
<template>
  <div class="scroll">
    <div class="scroll-cell">
      <div class="col col-hook" @scroll="scrollListen(0)">
        <ul>
          <li v-for="item in col1">{{ item.text }}</li>
        </ul>
      </div>
    </div>
    <div class="scroll-cell">
      <div class="col col-hook" @scroll="scrollListen(1)">
        <ul>
          <li v-for="item in col1[col1Number].col2">{{ item.text }}</li>
        </ul>
      </div>
    </div>
    <div class="mask-top"></div>
    <div class="select-box"></div>
    <div class="mask-bottom"></div>
  </div>
</template>
```
> script

```
<script>
  export default {
    data () {
      return {
        col1Number: 0,
        col2Number: 0
      }
    },
    created () {
      this.col1 = [
        {text: '科室1', id: '1', col2: [{text: '科室11', id: '11'}, {text: '科室12', id: '12'}, {text: '科室13', id: '13'}]},
        {text: '科室2', id: '2', col2: [{text: '科室21', id: '21'}, {text: '科室22', id: '22'}, {text: '科室23', id: '23'}]},
        {text: '科室3', id: '3', col2: [{text: '科室31', id: '31'}, {text: '科室32', id: '32'}, {text: '科室33', id: '33'}]},
        {text: '科室4', id: '4', col2: [{text: '科室41', id: '41'}, {text: '科室42', id: '42'}, {text: '科室43', id: '43'}]}
      ]
    },
    methods: {
      scrollListen (e) {
        const holdHeight = 36
        let scrollCell = document.getElementsByClassName('col-hook')
        let scrollHeight = scrollCell[e].scrollTop  // 滚动高度
        let getNumber = Math.round(scrollHeight / holdHeight)
        if (e === 0) {
          this.col1Number = getNumber
        }
        if (e === 1) {
          this.col2Number = getNumber
        }
        console.log('第一列id:' + this.col1[this.col1Number].id)
        console.log('第二列id:' + this.col1[this.col1Number].col2[this.col2Number].id)
      }
    }
  }
</script>
```
> style

```
style lang="scss" rel="stylesheet/scss">
  body {
    background: blue;
  }
  .scroll {
    display: flex;
    position: fixed;
    left: 0;
    bottom: 0;
    width: 100%;
  }
  .scroll-cell {
    flex: 1;
    background: white;
  }
  .col {
    width: 100%;
    height: 252px;
    overflow: auto;
    background: white;
  }
  .col::-webkit-scrollbar {
    display: none;
  }
  .col > ul {
    margin: 0;
    padding: 107px 0;
    list-style: none;
  }
  .col > ul > li {
    text-align: center;
    line-height: 36px;
    height: 36px;
  }
  .select-box {
    position: absolute;
    left: 0;
    top: 107px;
    width: 100%;
    height: 36px;
    background: rgba(0,0,0,.1);
  }
  .mask-top,
  .mask-bottom {
    position: absolute;
    left: 0;
    width: 100%;
    height: 107px;
    background: rgba(255,255,255,.5);
  }
  .mask-top {
    top: 0;
  }
  .mask-bottom {
    bottom: 0;
  }
</style>
```