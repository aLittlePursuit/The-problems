## vue全局引入scss公共文件和js文件

> 引入scss方法

```
1、首先在项目中安装依赖sass-resources-loader
   安装方法：npm install sass-resources-loader --save-dev
   
2、进入目录build/utils.js
   更改：  scss: generateLoaders('sass')
   更改为：scss: generateLoaders('sass').concat(
              {
                loader: 'sass-resources-loader',
                options: {
                  resources: path.resolve(__dirname, '../src/common/css/public.scss')  // 填写要引入的scss文件地址
                }
              }
            )
```

> 引入js方法
1. 例如：test.js文件引入main.js文件中


```
test.js如下

export default {
    test1 () {
        console.log('test1')
    },
    test2 () {
        console.log('test2')
    }
}



main.js中如下，其中用$的目的在于好区分

import test from '@/common/js/test'
Vue.prototype.$test = test



vue文件中调用如下

<script>
  export default {
    created () {
      this.test()
    },
    methods: {
      test () {
        this.$test.test1()
        this.$test.test2()
      }
    }
  }
</script>

```
