## vue移动端项目打包后空白页
> vue-cli脚手架工具打包，有两点需要注意的地方、

1. 配置文件打包后的引用文件路径问题

```
![image](http://snsoss.yizhen.cn/Uploads/Picture/2017-12-01/5a20ef71dc41d.png)
将路径assetsPublicPath: ''或者'./'
```
2. 路由配置问题

```
![image](http://snsoss.yizhen.cn/Uploads/Picture/2017-12-01/5a20ef7c89c58.png)
将路由配置项mode: 'history'删除
```
