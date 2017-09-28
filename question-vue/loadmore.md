# loadmore

```
<template>
  <div class="class-all-detail">
    <mt-loadmore :bottom-method="loadBottom" :bottom-all-loaded="allLoaded" ref="loadmore">
      <yz-live-cell :liveCell="valueList"></yz-live-cell>
    </mt-loadmore>
  </div>
</template>
```

```
<script>
  export default {
    data () {
      return {
        openId: '',
        userId: '',
        value: '',
        valueList: [],
        getParam: '',
        // 下拉加载
        page: 1,
        totalPage: '',
        allLoaded: false
      }
    },
    created () {
      Indicator.open({
        text: '加载中...',
        spinnerType: 'fading-circle'
      })
      // 获取openId
      if (getLocalStorage('openId') !== null) {
        this.openId = getLocalStorage('openId')
      }
      // 获取userId
      if (getLocalStorage('openId') !== null) {
        this.userId = getLocalStorage('userInfo').uid
      }
      // 得到上个页面传递过来的param值
      this.getParam = this.$route.params.param
      // console.log(this.getParam)
    },
    methods: {
      // 下拉加载更多数据
      loadBottom () {
        /**
        * 先判断当前页码是否等于总页码，由于请求中页码已经+1，所以在这里总页码同样+1去判断
        * 如果不相等上拉加载下一页数据，否则禁止下拉
        */
        if (this.page !== this.totalPage + 1) {
          this.requestLiveList()
        } else {
          this.allLoaded = true
        }
        setTimeout(() => {
          this.$refs.loadmore.onBottomLoaded()
        }, 1500)
      },
      // 直播分类列表接口数据请求
      async requestLiveList () {
        let list = await liveList(this.getParam, this.openId, this.page)
        this.value = list.data
        // 得到总页数
        this.totalPage = Math.ceil(list.data.totalCount / 20)
        // 这里是将数组的元素拼接合并,然后赋值
        this.valueList = [...this.valueList, ...list.data.list]
        // 每请求一次数据，页码+1
        this.page++
        // console.log('totalCount:' + '---' + list.data.totalCount)
        // console.log('valueList:' + '---' + this.valueList.length)
        // console.log('totalPage' + '---' + this.totalPage)
        // console.log('page' + '---' + this.page)
        Indicator.close()  // 数据加载完毕关闭提示信息
      }
    }
  }
</script>
```
