> 在ios设备上滚动生涩处理

```
// 给滚动元素添加样式,也可添加在body上，或者*
* {
 -webkit-overflow-scrolling: touch;   
}
```

```
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
```


