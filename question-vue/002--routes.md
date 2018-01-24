# routes文件

```
说明：
项目每个模块单独抽出路由.js文件，全部汇总到index.js下，目的是看起来更清晰，方便维护。
routes/index.js
      /module1.js
      /module2.js
```

> index.js

```
const main = r => require.ensure([], () => r(require('@/pages/main')), 'main')

// 引入module1.js等文件...
import module1Router from '@/routes/module1'
import module2Router from '@/routes/module2'

const routes = [
  // 默认定向为module1First.vue页面
  {
    path: '',
    redirect: '/main/module1First'
  },
  {
    path: '/main',
    name: 'main',
    component: main,
    children: [
      ...module1Router,
      ...module2Router
    ]
  }
]

export default routes

```

> module1.js


```
const module1 = r => require.ensure([], () => r(require('@/pages/module1/module1')), 'module1')
const module1First = r => require.ensure([], () => r(require('@/pages/module1/children/module1First')), 'module1First')
const module1Second = r => require.ensure([], () => r(require('@/pages/module1/children/module1Second')), 'module1Second')

const module1Router = [
  {
    path: 'module1',
    name: 'module1',
    component: module1,
    children: [
      {
        path: 'module1First',
        name: 'module1First',
        component: module1First
      },
      {
        path: 'module1Second',
        name: 'module1Second',
        component: module1Second
      }
    ]
  }
]

export default module1Router

```

> module2.js


```
const module2 = r => require.ensure([], () => r(require('@/pages/module2/module2')), 'module2')
const module2First = r => require.ensure([], () => r(require('@/pages/module2/children/module2First')), 'module2First')
const module2Second = r => require.ensure([], () => r(require('@/pages/module2/children/module2Second')), 'module2Second')

const module1Router = [
  {
    path: 'module2',
    name: 'module2',
    component: module2,
    children: [
      {
        path: 'module2First',
        name: 'module2First',
        component: module2First
      },
      {
        path: 'module2Second',
        name: 'module2Second',
        component: module2Second
      }
    ]
  }
]

export default module1Router

```


