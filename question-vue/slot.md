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
   <span slot='logo' class="" @click="reload">分发的内容</span>
</v-header>
```
