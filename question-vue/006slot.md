## slot分发
> 组件

```
<header>
   <slot name='logo'></slot>
   <slot name='search'></slot>
   <slot name="edit"></slot>
   <slot name="msite-title"></slot>
   <slot name="changecity"></slot>
   <slot name="changeLogin"></slot>
</header>
```
> v-header是组件组件的注册名称，这里要使用组件并且使用的位置不同填充的内容不同

```
<v-header>
<<<<<<< HEAD:question-vue/slot分发.txt
   // 需要展示logo就引入logo的slot
   <span slot='logo' class="log" @click="reload">分发的内容</span>
</v-header>

<style>
  // 定义分发内容的样式
  .log {
	position: absolute;
	left: 10px;
	top: 10px;
	width: 50px;
	height: 30px;
  }
</style>
=======
   <span slot='logo' class="" @click="reload">分发的内容</span>
</v-header>
```
>>>>>>> 61dfdcc9c75e73268360630d8d278b417517628d:question-vue/slot.md
