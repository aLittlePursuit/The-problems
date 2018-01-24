## 下拉加载更多mt-loadmore

```
<template>
    <div class="loadmore">
        <mt-loadmore :bottom-method="loadBottom" :auto-fill="false" :bottom-all-loaded="allLoaded" ref="loadmore">
            <ul>
              <li v-for="item in requestData" style="margin-top: 50px; background: red;">
                <div>{{ item.content }}</div>
                <div>{{ item.create_time }}</div>
              </li>
            </ul>
        </mt-loadmore>
    </div>
</template>

<script>
    import { mineAttention } from '@/service/getData'  // 数据接口
    import { Toast } from 'mint-ui'    // Toast提示信息
    
    export default {
        data () {
            page: 1,          // 默认第一页
            allLoaded: false, // 默认允许下拉
            requestData: []   // 存储请求的数据
        },
        methods: {
            // 数据请求接口
            async requestMineAttention (page) {
                const list = await mineAttention(this.openId, page)
                // 数据
                if (list.data.length) {
                    // es6语法数组数据拼接
                    this.requestData = [...this.requestData.data, ...list.data]
                    this.page++
                } else {
                    Toast('最后一页')
                    this.allLoaded = true    // 当请求的数据长度为空时，禁止上拉加载数据事件
                }
            },
            // 下拉加载数据方法
            loadBottom () {
                setTimeout(() => {
                    // 下拉时请求下一页数据（这时的page已经+1）
                    this.requestMineAttention(this.page)
                    this.$refs.loadmore.onBottomLoaded()
                }, 1500)
            }
        }
    }
</script>

<style>
    ...
</style>
```

