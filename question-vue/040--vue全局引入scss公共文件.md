## vue全局引入scss公共文件

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
