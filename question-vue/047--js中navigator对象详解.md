## navigator对象详解IE11，chrome和firefox浏览器下

```
// 属性
navigator.appCodeName                      // 返回与浏览器相关的内部代码名  都为Mozilla
navigator.appName                          // 返回浏览器正式名称  均为Netscape  
navigator.appVersion                       // 返回浏览器版本号  
navigator.cookieEnabled                    // 返回浏览器是否启用cookie，true和false 
navigator.geolocation                      // 返回地理定位信息(h5)  
navigator.javaEnabled()                    // 检测当前浏览器是否支持 Java，从而知道浏览器是否能显示 Java小程序(IE,chrome返回true，firefox返回false)
navigator.language                         // 返回浏览器的首选语言  
navigator.mimeTypes                        // 返回浏览器支持的Mime类型
navigator.msManipulationViewsEnabled       // 仅支持IE，true  
navigator.msMaxTouchPoints                 // 字面意思是最大的触摸点，IE为0，其他不支持  
navigator.msPointerEnabled                 // IE为true，其他不支持
navigator.onLine                           // 是否连接互联网，均返回true(未断网)  
navigator.platform                         // 所在平台，返回win32
navigator.plugins                          // 返回浏览器插件集合  
navigator.preference                       // 允许一个已标识的脚本获取并设置特定的 Navigator 参数  
navigator.product                          // 浏览器产品名，返回gecko 
navigator.systemLanguage                   // 获取系统语言，IE支持，返回zh-cn  
navigator.userAgent                        // 判断浏览器类型
navigator.userLanguage                     // 返回操作系统的自然语言设置,IE支持，返回zh-cn

// 方法  
navigator.msLaunchUri                      // 回调函数
navigator.taintEnabled                     // 回调函数
navigator.hasOwnProperty                   // 意思是是否支持属性，用法如下
document.hasOwnProperty("ontouchstart")    // 电脑返回false，手机为true
```
