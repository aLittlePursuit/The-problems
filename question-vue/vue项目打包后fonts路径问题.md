## vue项目打包后fonts路径问题
> vue-cli打包完成后提示fonts路径不对

路径变成staric/css/static/css/font/...而我们需要的路径是static/css/font/...
```
![image](http://snsoss.yizhen.cn/Uploads/Picture/2017-12-01/5a20f17da88ab.png)
将文件中extract: true修改为false
```
