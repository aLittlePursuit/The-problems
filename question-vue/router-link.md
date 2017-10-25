# router-link
> 没有指定tag属性的时候默认解析后router-link为a标签

```
<router-link to="/"></router-link>
```
> 指定tag属性的时候解析后router-link为tag属性的值的标签,此处为li标签

```
<router-link  tag="li" to="/"></router-link>
```
> 当出现这种方式的跳转时，说明展示页面为同一个页面只是展示的内容根据id的不同而不同

```
<router-link  v-for="item in hotcity" :to="'/city/' + item.id" :key="item.id">
    {{item.name}}
</router-link>
或者
<router-link  v-for="item in hotcity" :to="`/city/${item.id}`" :key="item.id">
    {{item.name}}
</router-link>
```
> name跳转

```
<router-link :to="{name: 'name'}"></router-link>
<router-link :to="{name: 'name', params: {type: 'type'}}"></router-link>
<router-link :to="{name: 'name', query: {type: 'type'}}"></router-link>
```

注释：无论router-link解析后的是什么标签只要带to属性都可跳转路径，（单独的页面跳转直接to="跳转地址"，重复使用根据id不同填充响应的数据的页面需要用:to="跳转地址"）