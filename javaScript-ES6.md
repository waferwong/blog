[mjavascript/practical-modern-javascript: 🏊 Dive into ES6 and the future of JavaScript](https://github.com/mjavascript/practical-modern-javascript)
[ES6 常用新特性讲解 | 熊D博客](http://blog.beard.ink/JavaScript/ES6-%E5%B8%B8%E7%94%A8%E6%96%B0%E7%89%B9%E6%80%A7%E8%AE%B2%E8%A7%A3/)
[ECMAScript 6 扫盲](http://mp.weixin.qq.com/s?__biz=MzAxMjA5ODQwMQ==&mid=2455058700&idx=1&sn=9361036ef5dc0c27cafb0612d495a85c)
[深入浅出ES6（一）：ES6是什么](http://www.infoq.com/cn/articles/es6-in-depth-an-introduction)
[深入浅出ES6（十）：集合](http://www.infoq.com/cn/articles/es6-in-depth-collections)
[ES6 你可能不知道的事 - 进阶篇 | Taobao FED | 淘宝前端团队](http://taobaofed.org/blog/2016/11/03/es6-advanced/)
[面对前端六年历史代码，如何接入并应用ES6解放开发效率](http://mp.weixin.qq.com/s/wu1RzfXWo8k-fu_tZxe9NA)
[聊聊ES7与ES8特性 | Fundebug博客](https://blog.fundebug.com/2017/08/28/es7-and-es8/)

[JavaScript Factory Functions with ES6+ – JavaScript Scene – Medium](https://medium.com/javascript-scene/javascript-factory-functions-with-es6-4d224591a8b1)

## babel
[剖析Babel——Babel总览 | AlloyTeam](http://www.alloyteam.com/2017/04/analysis-of-babel-babel-overview/)
[babel/definitions.js at master · babel/babel](https://github.com/babel/babel/blob/master/packages/babel-plugin-transform-runtime/src/definitions.js)
[Babel 入门教程 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2016/01/babel.html)

[如何写好.babelrc？Babel的presets和plugins配置解析 - 韩小平的博客](https://excaliburhan.com/post/babel-preset-and-plugins.html)
[再见，babel-preset-2015](https://zhuanlan.zhihu.com/p/29506685)
[以 async/await 为例，说明 babel 插件怎么搭 · Issue #8 · sabakugaara/sabakugaara.github.io](https://github.com/sabakugaara/sabakugaara.github.io/issues/8)

[Babel polyfill 知多少](https://zhuanlan.zhihu.com/p/29058936)
[Babel的使用 - 前端工程化 - SegmentFault](https://segmentfault.com/a/1190000008159877#articleHeader10)
[从0到1搭建webpack2+vue2自定义模板详细教程 - 小青年博客 - SegmentFault](https://segmentfault.com/a/1190000009454172#articleHeader8)
[你真的会用 Babel 吗? - SYJ个人主页 - SegmentFault](https://segmentfault.com/a/1190000011155061)



# let const
块级作用域 顶层变量（window global）
let 声明的变量只在let命令所在的代码块内有效（for）
var的问题，在function返回function
const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址不得改动。对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指针，const只能保证这个指针是固定的，至于它指向的数据结构是不是可变的，就完全不能控制了。
Object.freeze
var constantize = (obj) => {
  Object.freeze(obj);
  Object.keys(obj).forEach( (key, i) => {
    if ( typeof obj[key] === 'object' ) {
      constantize( obj[key] );
    }
  });
};
[ES6 变量声明与赋值：值传递、浅拷贝与深拷贝详解 - 知乎专栏](https://zhuanlan.zhihu.com/p/28508795)

# 解构
ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构（Destructuring）。
在等号赋值或for循环中，如果需要从数组或对象中取值，尽量使用解构。
在自己定义函数的时候，如果调用者传来的是数组或对象，形参尽量使用解构方式，优先使用对象解构，其次是数组解构。代码可读性会很好。
在调用第三方函数的时候，如果该函数接受多个参数，并且你要传入的实参为数组，则使用扩展运算符。可以避免使用下标形式传入参数。也可以避免很多人习惯的使用apply方法传入数组。
rest运算符使用场景应该稍少一些，主要是处理不定数量参数，可以避免arguments对象的使用。
[妙用ES6解构和扩展运算符让你的代码更优雅 - loop4ever - 博客园](http://www.cnblogs.com/chrischjh/p/4848934.html)
[使用对象展开运算符 | Redux 中文文档 Join the chat at https://gitter.im/camsong/redux-in-chinese](http://cn.redux.js.org/docs/recipes/UsingObjectSpreadOperator.html)
[解构赋值 - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)
[Several demos and usages for ES6 destructuring. Runnable demos and slides about the same topic: http://git.mikaelb.net/presentations/bartjs/destructuring](https://gist.github.com/mikaelbr/9900818)
[Default values for nested object parameters using destructuring · Issue #1940 · babel/babel](https://github.com/babel/babel/issues/1940)

# module
ES6 模块之中，顶层的this指向undefined，即不应该在顶层代码使用this。
export命令用于规定模块的对外接口，import命令用于输入其他模块提供的功能。
## export
一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用export关键字输出该变量。


# class
JavaScript 中的类只是 JavaScript 现有的、基于原型的继承模型的一种语法包装（语法糖），它能让我们用更简洁明了的语法实现继承。

[Familiarity Bias is Holding You Back: It’s Time to Embrace Arrow Functions](https://medium.com/javascript-scene/familiarity-bias-is-holding-you-back-its-time-to-embrace-arrow-functions-3d37e1a9bb75)


# 异步
Callback Hell
Promise
[JavaScript Promise迷你书（中文版）](http://liubin.org/promises-book/)
[我的Promise对象初识与进阶 - 知乎专栏](https://zhuanlan.zhihu.com/p/26767436)
[咪西西の部落格](https://aonosora.com/article/6)
[JavaScript异步与Promise实现 – 熊建刚的博客](http://blog.codingplayboy.com/2017/05/10/async_promise/)

Generator
[深度了解ES6：魔力四射的生成器 Generators](https://mp.weixin.qq.com/s?__biz=MzIwNjQwMzUwMQ==&mid=2247483886&idx=1&sn=929d1575210697dad5cda8d44a90e8d6&scene=1&srcid=07027Cr9IuN8YNyWRMl6NK3Y&from=groupmessage&isappinstalled=0#wechat_redirect)

async await
[Await and Async Explained with Diagrams and Examples – Nikolay Grozev](http://nikgrozev.com/2017/10/01/async-await/)
[articles-translator/Javascript中Async-Await优于Promise的6个原因.md at master · neal1991/articles-translator](https://github.com/neal1991/articles-translator/blob/master/Javascript%E4%B8%ADAsync-Await%E4%BC%98%E4%BA%8EPromise%E7%9A%846%E4%B8%AA%E5%8E%9F%E5%9B%A0.md)
[JavaScript是如何工作的:事件循环和异步编程的兴起-5个关于如何使用async/await编写更简洁代码的技巧 - 众成翻译](http://zcfy.cc/article/how-javascript-works-event-loop-and-the-rise-of-async-programming-5-ways-to-better-coding-with-4506.html)
[浅谈Async/Await](https://mp.weixin.qq.com/s/5ir6N17XHPRtQ_kQm8ZV0A)
[Async/Await是这样简化JavaScript代码的 | Fundebug博客](https://blog.fundebug.com/2017/10/16/async-await-simplify-javascript/)
[Async/Await替代Promise的6个理由 | Fundebug博客](https://blog.fundebug.com/2017/04/04/nodejs-async-await/)
[重构：从Promise到Async/Await | Fundebug博客](https://blog.fundebug.com/2017/12/13/reconstruct-from-promise-to-async-await/)
[深入理解ES7的async/await | coolcao的小站](http://coolcao.com/2016/12/12/deeper-understanding-of-async-await/)

```javascript
//初始化GPS
        Public.getGPS().then((data) => {
            this.lat = data.latitude; // 纬度，浮点数，范围为90 ~ -90
            this.lon = data.longitude; // 经度，浮点数，范围为180 ~ -180。
            console.log('clinicList  GPSInit  latLon=' + data.latitude + ',' + data.longitude);


            if (!data.isCache) {
                return GetInfoByLatLon(data.latitude, data.longitude).then(res => {
                    console.log('clinicList GetInfoByLatLon  res=' + res);
                    this.cityName = res.cityName;
                    this.cityCode = res.cityCode;

                })
            }
        }).then(()=>{
            this.getClinicsAjax(true);
        }).catch(() => {
            this.getClinicsAjax(true);
        });
```

# Proxy
[实例解析 ES6 Proxy 使用场景 · PINGGOD](http://pinggod.com/2016/%E5%AE%9E%E4%BE%8B%E8%A7%A3%E6%9E%90-ES6-Proxy-%E4%BD%BF%E7%94%A8%E5%9C%BA%E6%99%AF/)
[探索两种优雅的表单验证——策略设计模式和ES6的Proxy代理模式 · Issue #19 · jawil/blog](https://github.com/jawil/blog/issues/19)

# Reflect
[ES6 Reflect](https://zhuanlan.zhihu.com/p/24778807)
