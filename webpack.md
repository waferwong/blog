
<!-- toc orderedList:0 depthFrom:1 depthTo:6 -->

* [示例](#示例)
* [插件](#插件)
* [概念](#概念)
    * [Chunk 是什么？](#chunk-是什么)
    * [Chunk 包含了哪些内容？](#chunk-包含了哪些内容)
    * [entry chunk 入口块](#entry-chunk-入口块)
    * [normal chunk 普通块](#normal-chunk-普通块)
    * [initial chunk 初始块](#initial-chunk-初始块)
    * [例子解释](#例子解释)
  * [原理](#原理)
* [resolve](#resolve)
      * [使用 alias](#使用-alias)
      * [使用 noParse](#使用-noparse)
* [资源](#资源)
  * [路径处理](#路径处理)
  * [html](#html)
    * [html-loader](#html-loader)
    * [html-webpack-plugin](#html-webpack-plugin)
      * [模板](#模板)
      * [内联](#内联)
  * [CSS](#css)
    * [ExtractTextPlugin](#extracttextplugin)
    * [PostCSS](#postcss)
    * [CSS module](#css-module)
    * [CSS压缩](#css压缩)
  * [图片 字体](#图片-字体)
* [缓存](#缓存)
* [区分环境](#区分环境)
  * [开发](#开发)
* [JS打包策略](#js打包策略)
    * [dll](#dll)
      * [hash](#hash)
    * [CommonsChunkPlugin](#commonschunkplugin)
      * [manifest](#manifest)
    * [第三方库](#第三方库)
  * [分片/按需加载 Code Splitting](#分片按需加载-code-splitting)
    * [require.ensure](#requireensure)
    * [import then](#import-then)
    * [require.include](#requireinclude)
    * [Chunk 优化](#chunk-优化)
* [多页](#多页)
* [流程](#流程)
* [优化](#优化)
    * [速度](#速度)
      * [cache](#cache)
      * [happypack](#happypack)
    * [大小](#大小)
    * [tree shaking](#tree-shaking)

<!-- tocstop -->

# 示例
[基于webpack搭建前端工程解决方案探索](http://www.infoq.com/cn/articles/frontend-engineering-webpack?hmsr=toutiao.io&utm_campaign=rightbar_v2&utm_content=link_text&utm_medium=toutiao.io&utm_source=toutiao.io)
[sapling-team/generator-sapling-pc: PC端项目脚手架，兼容IE8+](https://github.com/sapling-team/generator-sapling-pc)
[「前端」看懂前端脚手架你需要这篇webpack · Issue #7 · ShowJoy-com/showjoy-blog](https://github.com/ShowJoy-com/showjoy-blog/issues/7)
[package.json](https://gist.github.com/gwuhaolin/cebd252a23793e742e6acae90ab63e83)
[静态资源 | 介绍](http://hq5544.github.io/vue-webpack/static.html)
[基于webpack和vue.js搭建的H5端框架(其实主要用于Hybrid开发H5端框架，但是依然能够作为纯web端使用) | HcySunYang](http://hcysun.me/2016/03/25/%E5%9F%BA%E4%BA%8Ewebpack%E5%92%8Cvue.js%E6%90%AD%E5%BB%BA%E7%9A%84H5%E7%AB%AF%E6%A1%86%E6%9E%B6(%E5%85%B6%E5%AE%9E%E4%B8%BB%E8%A6%81%E7%94%A8%E4%BA%8EHybrid%E5%BC%80%E5%8F%91H5%E7%AB%AF%E6%A1%86%E6%9E%B6%EF%BC%8C%E4%BD%86%E6%98%AF%E4%BE%9D%E7%84%B6%E8%83%BD%E5%A4%9F%E4%BD%9C%E4%B8%BA%E7%BA%AFweb%E7%AB%AF%E4%BD%BF%E7%94%A8)/)
[HJM's blog](http://imhjm.com/article/59a23be97dd03248a2e8d583)
[看清楚真正的 Webpack 插件 - zoumiaojiang](https://zoumiaojiang.com/article/what-is-real-webpack-plugin/?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)

[webpack-contrib/awesome-webpack: A curated list of awesome Webpack resources, libraries and tools](https://github.com/webpack-contrib/awesome-webpack#webpack-plugins)

[小议webpack下的AOP式无侵入注入](https://mp.weixin.qq.com/s/de1N9mK_in-mkktqBFHygA)

# 插件
const chalk = require('chalk')
const ProgressBarPlugin = require('progress-bar-webpack-plugin')
new ProgressBarPlugin({
    format: '  build [:bar] ' + chalk.green.bold(':percent') + ' (:elapsed seconds)'
}),
进度显示不准，不实用
[javascript - Why does Webpack's DefinePlugin require us to wrap everything in JSON.stringify? - Stack Overflow](https://stackoverflow.com/questions/39564802/why-does-webpacks-defineplugin-require-us-to-wrap-everything-in-json-stringify)


# 概念
chunk是webpack中最基本的概念之一，且chunk常常会和entry弄混淆。在「打包文件分割部分」我们定义了两个入口entry point -- app和vendor，而通过一些配置，webpack会生成最后的一些打包文件，在这个例子中最后生成的文件有app.js 、 vendor.js 、 manifest.js。这些文件便被称为块chunk。

entry & chunk 可以简单的理解为一个入口、一个出口

chunks
输出的打包js

assets
最终输出output的文件（html, css, js, png...）,包括插件生成的（Copy）

entrypoints

module
引用的每一个js, css, jpg ...

### Chunk 是什么？

webpack 中 Chunk 实际上就是输出的 .js 文件，可能包含多个模块，主要的作用是为了优化异步加载。

### Chunk 包含了哪些内容？

对于同步的情况，一个 Chunk 会递归的把模块中所有的依赖都加入到 Chunk 中。

对于异步的情况，在每一个 split point 上所有依赖的模块会打包进一个新的 chunk，和同步一样，依赖也是递归的，如果子模块依赖其他模块也会加入到 chunk 中，依赖的回调函数中 require 的其他模块也会打包进 chunk 中，以下公式表示 chunk 内容：

chunk content = recursive(ensure 依赖) + recursive(callback 依赖)


`chunk`是webpack中最基本的概念之一，且`chunk`常常会和`entry`弄混淆。在「打包文件分割部分」我们定义了两个入口entry point -- app和vendor，而通过一些配置，webpack会生成最后的一些打包文件，在这个例子中最后生成的文件有`app.js 、 vendor.js 、 manifest.js`。这些文件便被称为块`chunk`。

**entry & chunk 可以简单的理解为一个入口、一个出口**

在官方1.0文档中webpack的chunk类型分为三种：

1.  entry chunk 入口块
2.  normal chunk 普通块
3.  initial chunk 初始块

### entry chunk 入口块

`entry chunk 入口块`不能由字面意思理解为由入口文件编译得到的文件，由官网介绍

> An entry chunk contains the runtime plus a bunch of modules

可以理解为包含runtime运行时的块可以称为entry chunk，一旦原本存在运行时（runtime）的`entry chunk`失去了运行时，这个块就会转而变成`initial chunk`。

### normal chunk 普通块

> A normal chunk contains no runtime. It only contains a bunch of modules.

普通块不包含运行时runtime，只包含一系列模块。但是在应用运行时，普通块可以动态的进行加载。通常会以jsonp的包装方式进行加载。而`code splitting`主要使用的就是普通块。

### initial chunk 初始块

> An initial chunk is a normal chunk.

官方对initial chunk的定义非常简单，初始块就是普通块，跟普通块相同的是同样不包含运行时runtime，不同的是初始块是计算在初始加载过程时间内的。在介绍入口块entry chunk的时候也介绍过，一旦入口块失去了运行时，就会变成初始块。这个转变经常由`CommonsChunkPlugin`插件实现。

### 例子解释

还是拿「打包文件分割」的代码做例子，

``` js
// app.js

require('vue');
require('vuex');
```

``` js
// webpack.config.js

entry: {
    app: 'app/app.js',
    vendor: ['vue', 'vuex'],
  },
```

没有使用`CommonsChunkPlugin`插件之前，两个entry分别被打包成两个chunk，而这两个chunk每个都包含了运行时，此时被称为`entry chunk`入口块。

而一旦使用了`CommonsChunkPlugin`插件，运行时runtime最终被转移到了`manifest.js`文件，此时最终打包生成的三个chunk`app.js 、 vendor.js 、 manifest.js`，app.js、vendor.js失去了runtime就由入口块变成初始块。

Initial chunk 大多数情况下是由 CommonsChunkPlugin 这个插件生成的, 应该首先加载, 但遇到 entry chunk 中的入口 module(0) 才会执行.

## 原理
每个文件都是一个资源，可以用require导入js
每个入口文件会把自己所依赖(即require)的资源全部打包在一起，一个资源多次引用的话，只会打包一份
对于多个入口的情况，其实就是分别独立的执行单个入口情况，每个入口文件不相干(可用CommonsChunkPlugin优化)

webpack的id 有两种 一种为 chunkid 一种为moduleId

每个chunkid 对应的是一个js文件
每个moduleid对应的是一个个js文件的内容的模块（一个js文件里面可以require多个资源，每个资源分配一个moduleid）
为何要出来一个chunkid呢？ 这个chunkid的作用就是，标记这个js文件是否已经加载过了

这个 webpackJsonp([0],[]) 第一个参数 [0] 是什么意思呢？  它就是 chunkid ,我们知道一个chunkid
id对应一个 js 文件，它对应的js文件就是它的入口文件 entry.js， 那为何这里还要是一个数组

因为一个入口文件的话，可以依赖多个js文件，其他的 id 就是它所依赖的， 其实就是配置webpack的时候

那个入口js对应的 数组

index: ['./src/js/entry.js'],   [0] 和 现在的id数组一一对应

[webpack源码解读：命令行输入webpack的时候都发生了什么？ - 知乎专栏](https://zhuanlan.zhihu.com/p/24717349)
[webpack 源码解析 - 前端 - 掘金](https://juejin.im/entry/576b7aeda633bd0064065c74)
[细说 webpack 之流程篇 | Taobao FED | 淘宝前端团队](http://taobaofed.org/blog/2016/09/09/webpack-flow/)
[webpack打包-模块分布解析 - CNode技术社区](https://cnodejs.org/topic/5867bb575eac96bb04d3e301)
[webpack产出代码模块化浅析 · Dont](http://shellphon.wang/githublog/2017/02/webpack-product.html)
[从 Bundle 文件看 Webpack 模块机制](https://zhuanlan.zhihu.com/p/25954788)

webpack runtime（`webpackBootstrap`）[代码](https://gist.github.com/blade254353074/4a591d559065383adbdc3946e515158c)不多，主要包含几个功能：

* 全局 `webpackJsonp` 方法：模块读取函数，用来区分模块是否加载，并调用 `__webpack_require__` 函数；
* 私有 `__webpack_require__` 方法：模块初始化执行函数，并给执行过的模块做标记；
* 异步 chunk 加载函数（用 script 标签异步加载），加载的 chunk 内容均被 `webpackJsonp` 包裹的，script 加载成功会直接执行。这个函数还包含了所有生成的 chunks 的路径。在 webpack 2 中这个函数用到了 Promise，因此可能需要提供 Promise Polyfill；
* 对 ES6 Modules 的默认导出（export default）做处理。

立即执行函数

入口文件entry以及需要异步加载的模块js都被编译成webpackJsonp()的函数执行结构
`wpJsonp`的主要作用，就是将模块的执行内容存放到modules中，以方便`wpRequire`的时候，需要的模块能被找到执行体并初始化生成对应的module模块，在这个过程中，`moduleId`就是模块执行体以及模块对象的索引值。

另外`wpJsonp`还有一个逻辑是执行chunk的回调，即异步加载模块在加载完成并执行时，会触发执行`wpRequire.ensure`时加入的回调内容。在这过程中，ensure主要负责的是：

1.  将回调收集（模块正在加载中）
2.  执行回调（之前已经加载过了）
3.  开辟缓存位置（`installedChunks`）并启用`script`加载js。

而`chunkId`主要为入口文件或者异步加载文件的索引值。

关于`installedModules`变量，用于存储加载好的模块对象，当对应索引的内容为0时，没有含义，因为逻辑在判断if时发现没有模块，所以要去加载模块，跟初始化时加载模块是一样的。而当加载完模块后，则会保存对应的module对象。

关于`installedChunks`变量，用于标记chunk的加载状态，主要用于异步加载，当对应索引的内容为0时，表示该chunk已经加载过了，如果正在加载，则为数组（回调函数数组）。当chunk在 `wpJsonp`执行时加载已经完成，其逻辑也会去判断回调，统一执行回调，并将对应标识置零。

编译结果内，会将用到的chunk都整理到`ensure`的script加载逻辑内，根据chunkId来索引加载。

library
[webpack中library和libraryTarget与externals的使用 · Issue #10 · zhengweikeng/blog](https://github.com/zhengweikeng/blog/issues/10)
[liangklfangl/webpack-external-library](https://github.com/liangklfangl/webpack-external-library)
[创建 Library](https://doc.webpack-china.org/guides/author-libraries/)

# webpack 4
## 零配置
entry 的默认值是 ./src 
output.path 的默认值是 ./dist
mode 的默认值是 production
UglifyJs 插件默认开启 caches 和 parallizes

## mode
### development
默认启用optimization.namedModules（原NamedModulesPlugin，现已弃用）
开发时开启注视和验证，并且自动加上了eval devtool
development 模式 使用 eval 构建 module，用来提升构建速度
webpack.DefinePlugin 插件的 process.env.NODE_ENV 的值不需要再定义，默认是 development

### production
默认使用optimization.noEmitOnErrors（原NoEmitOnErrorsPlugin，现已弃用）。
生产环境默认开启了很多代码优化（minify，splite等）
生产环境不支持watching，开发环境优化了重新打包的速度
生产环境开启模块串联（原ModuleConcatenationPlugin），没用过不多说
ModuleConcatenationPlugin->optimization.concatenateModules 
webpack.DefinePlugin 插件的 process.env.NODE_ENV 的值不需要再定义，默认是 production

### none
如果你给mode设置为none，所有默认配置都去掉了

## Optimization
[webpack/WebpackOptions.json at master · webpack/webpack](https://github.com/webpack/webpack/blob/master/schemas/WebpackOptions.json)
[webpack-contrib/mini-css-extract-plugin: Lightweight CSS extraction plugin](https://github.com/webpack-contrib/mini-css-extract-plugin)

### CommonsChunkPlugin
[RIP CommonsChunkPlugin.md](https://gist.github.com/sokra/1522d586b8e5c0f5072d7565c2bee693)

### UglifyJsPlugin
optimization.minimize为true就行，production mode下面自动为true

optimization.minimizer可以配置你自己的压缩程序

### sideEffects
入的第三方插件在 package.json 里面配置  sideEffects:false 后，据说是可以大幅度地减小打包出的文件的体积，具体待验证。

目前初步了解 sideEffects 的信息：sideEffects:false 表示该模块无副作用。当你需要导入，但不需要导出任何东西时，但需要在导入时做其他事情(必然初始化，pollyfill等)，这就是导入模块的副作用. 目前对这个理解的不多，具体在第三方库的构建上面没有一个直观的感受，需要继续深入了解。

# resolve

如果不希望这里涉及到的路径和执行webpack命令时的具体路径相关，而是希望相对于配置文件的路径的话，就需要使用path模块

context：基础目录，绝对路径，用于从配置中解析入口起点(entry point)和 loader
默认使用当前目录，但是推荐在配置中传递一个值。这使得你的配置独立于 CWD(current working directory - 当前执行路径)。

不加context的时候，路径的配置是基于process.cwd()，即脚本运行时shell所在的目录，而不是配置文件所在的目录

webpack 使用 enhanced-resolve 来解析文件路径
[模块解析(Module Resolution)](https://doc.webpack-china.org/concepts/module-resolution)
[解析(Resolve)](https://doc.webpack-china.org/configuration/resolve/)
[模块(Module)](https://doc.webpack-china.org/configuration/module/#module-noparse)

若未设置`resolve.modules`属性值，则webpack默认先从`node_modules`查找模块，然后在根目录下查找。

alias
创建 import 或 require 的别名，来确保模块引入变得更简单
https://doc.webpack-china.org/configuration/resolve/#resolve-alias

#### 使用 alias

`resolve.alias` 配置路径映射。
发布到npm的库大多数都包含两个目录，一个是放着cmd模块化的lib目录，一个是把所有文件合成一个文件的dist目录，多数的入口文件是指向lib里面下的。
默认情况下webpack会去读lib目录下的入口文件再去递归加载其它依赖的文件这个过程很耗时，alias配置可以让webpack直接使用dist目录的整体文件减少文件递归解析。配置如下：

``` js
module.exports = {
  resolve: {
    alias: {
      'moment': 'moment/min/moment.min.js',
      'react': 'react/dist/react.js',
      'react-dom': 'react-dom/dist/react-dom.js'
    }
  }
};
```

alias
配置路径映射。 发布到npm的库大多数都包含两个目录，一个是放着cmd模块化的lib目录，一个是把所有文件合成一个文件的dist目录，多数的入口文件是指向lib里面下的。 默认情况下webpack会去读lib目录下的入口文件再去递归加载其它依赖的文件这个过程很耗时，alias配置可以让webpack直接使用dist目录的整体文件减少文件递归解析。
alias: {
  'moment': 'moment/min/moment.min.js',
  'react': 'react/dist/react.js',
  'react-dom': 'react-dom/dist/react-dom.js'
}

#### 使用 noParse

`module.noParse` 配置哪些文件可以脱离webpack的解析。
有些库是自成一体不依赖其他库的没有使用模块化的，比如jquey、momentjs、chart.js，要使用它们必须整体全部引入。
webpack是模块化打包工具完全没有必要去解析这些文件的依赖，因为它们都不依赖其它文件体积也很庞大，要忽略它们配置如下：

``` js
module.exports = {
  module: {
    noParse: /node_modules\/(jquey|moment|chart\.js)/
  }
};
```

像是 react 这种已经打好了生产包的使用 externals 很方便，但是也有很多 npm 包是没有提供的，这种情况下 DLLBundle 仍可以使用。
如果只是引入 npm 包一部分的功能，比如 require('react/lib/React') 或者 require('lodash/fp/extend') ，这种情况下 DLLBundle 仍可以使用。
当然如果只是引用了 react 这类的话，externals 因为配置简单所以也推荐使用。

noParse
配置哪些文件可以脱离webpack的解析。 有些库是自成一体不依赖其他库的没有使用模块化的，比如jquey、momentjs、chart.js，要使用它们必须整体全部引入。 webpack是模块化打包工具完全没有必要去解析这些文件的依赖，因为它们都不依赖其它文件体积也很庞大
noParse: /node_modules\/(jquey|moment|chart\.js)/
如果你 确定一个模块中没有其它新的依赖 就可以配置这项，webpack 将不再扫描这个文件中的依赖。

# 资源

在传统或稍早一点的应用中，我们通常会将所有的图片，字体等资源放在一个基础目录下，如`assets/`或`images`，但是对于那些在多项目间重复的插件代码或资源来说，每一次迁移，我们都得在一大堆图片，字体资源里寻找出我们需要迁移的资源，这对代码可重用和其独立性有一定限制，而且与现在提倡的组件化开发模式也不相符。

webpack对于资源的处理方式给组件化开发提供了很大便利，使得我们以组件为单位，可以在某一组件目录下存放所有相关的js，css，图片，字体等资源文件；组件的迁移公用成本很低。不过组件化开发并不是说不需要资源目录了，一些公用的资源依然放在项目的基础目录下。

不要立即删除无用的资源(等待数周), 以免长时间保持浏览器窗口打开的用户 404

[webpack与SPA实践之管理CSS等资源 – 熊建刚的博客](http://blog.codingplayboy.com/2017/06/06/webpack_resource_manage/)
[翻译 | 关键CSS和Webpack: 减少阻塞渲染的CSS的自动化解决方案](https://mp.weixin.qq.com/s/VAVT_JTJE1v2nXx8NVwP9Q)

## 路径处理

1.  **output.publicPath**: 对于这个选项，我们无需关注什么绝对相对路径，因为两种路径都可以。我们只需要知道一点：这个选项是指定 HTML 文件中资源文件 (字体、图片、JS文件等) 的`文件名`的公共 URL 部分的。在实际情况中，我们首先会通过`output.filename`或有些 loader 如`file-loader`的`name`属性设置`文件名`的原始部分，webpack 将`文件名`的原始部分和公共部分结合之后，HTML 文件就能获取到资源文件了。
2.  **devServer.contentBase**: 设置静态资源的根目录，`html-webpack-plugin`生成的 html 不是静态资源。当用 html 文件里的地址无法找到静态资源文件时就会去这个目录下去找。
3.  **devServer.publicPath**: 指定浏览器上访问所有 **打包(bundled)文件** (在`dist`里生成的所有文件) 的根目录，这个根目录是相对服务器地址及端口的，比`devServer.contentBase`和`output.publicPath`优先。

html
- img src
- link href

css
- url

js
- import

过程：
将引用到的每一个资源标记，小于limit直接用dataurl，大于则将路径转换为file-loader的name参数（默认放在output目录下），
例如，url("../../resources/images/activities/springActivity-1.png") => url("resources/images/activities/springActivity-1.png")
url("cardBack.png") => url("healthProduct/css/cardBack.png")
url("./cardBack.png") => url("healthProduct/css/cardBack.png")
{
  loader: 'file-loader',
  options: {
    name: '[path][name].[ext]'
  }  
}
[name]	{String}	file.basename	The basename of the resource
[path]	{String}	file.dirname	The path of the resource relative to the context
http://127.0.0.1:8088/healthProduct/css/healthProduct/css/cardBack.png
http://127.0.0.1:8088/【healthProduct/css】【/healthProduct/css/cardBack.png】

此时需要配置publicPath，否则会报404，配置后会拼接上publicPath， 如 url("/weixin/resources/images/activities/springActivity-1.png")

配置了publicPath后，html-webpack-plugin 将从【相对文件】引用变成【相对根目录】引用
如
<link href="/vendors.css" rel="stylesheet">
<script type="text/javascript" src="/vendors.js"></script>

可以配置publicPath的地方
- output
- ExtractTextPlugin
- file-loader

publicPath为全局配置，会导致图片地址也变为这个cdn地址，如果我们的图片有另一个cdn地址怎么办？
插件是可以针对不同的资源覆盖这个地址的，所以比如对于图片，我们可以使用上文描述过的url-loader覆盖publicPath，如：use: "url-loader?name=[name].[ext]&publicPath=img.xxx.com..."

资源路径的处理

- 相对路径，例如，./assets/logo.png 将会被解析成依赖模块。它们将会被基于 webpack 输出配置所自动生成的 URL 所代替。
- 无前缀 URL，例如，assets/logo.png 将会被视为相对路径，并且变成 ./assets/logo.png。
- 带有 ~ 前缀的 URL 将会被视为依赖模块的请求，类似于 require('some-module/image.png')。如果你想要让 webpack 将它作为模块处理，可以使用这个前缀。例如，如果你想要用 assets 作为 alias，你需要使用 `<img src="~assets/logo.png">` 来确保 alias 可以使用。【注意只能在vue里面使用】
- 相对跟目录的 URL，例如，/assets/logo.png 完全不会被 webpack 处理。

https://github.com/bholloway/resolve-url-loader

## html
html 压缩
html-loader
html-webpack-plugin

html里的`<style>`没有loader可以处理

### html-loader
对于style的处理？
[file-loader引起的html-webpack-plugin坑 - wonyun - 博客园](http://www.cnblogs.com/wonyun/p/5950722.html)

### html-webpack-plugin
[jantimon/html-webpack-plugin: Simplifies creation of HTML files to serve your webpack bundles](https://github.com/jantimon/html-webpack-plugin)
[html-webpack-plugin/template-option.md at master · jantimon/html-webpack-plugin](https://github.com/jantimon/html-webpack-plugin/blob/master/docs/template-option.md)

[jharris4/html-webpack-include-assets-plugin: Add the ability to include assets based on a list of paths](https://github.com/jharris4/html-webpack-include-assets-plugin)

#### 模板
ejs和html兼容
ejs 语法特别慢
html-loader不支持ejs语法
为template指定的模板文件没有指定**任何loader的话**，默认使用`ejs-loader`。如`template: './index.html'`，若没有为`.html`指定任何loader就使用`ejs-loader`

[html-webpack-template/index.html at 86f285d5c790a6c15263f5cc50fd666d51f974fd · jaketrent/html-webpack-template](https://github.com/jaketrent/html-webpack-template/blob/86f285d5c790a6c15263f5cc50fd666d51f974fd/index.html)

#### 内联
在打包文件的时候，有时候需要把 js、css 等代码内联进 html 中，减少文件的请求，优化加载速度。
用过 fis 的同学应该对 `__inline` 语法比较熟悉，它就是用来把代码内联进 html 的

[web-webpack-plugin/readme_zh.md at master · gwuhaolin/web-webpack-plugin](https://github.com/gwuhaolin/web-webpack-plugin/blob/master/readme_zh.md#自动探测html入口-demo)

## CSS
[webpack中关于样式的处理 · Issue #9 · zhengweikeng/blog](https://github.com/zhengweikeng/blog/issues/9)
[Clarify importLoaders documentation? · Issue #228 · webpack-contrib/css-loader](https://github.com/webpack-contrib/css-loader/issues/228)

### ExtractTextPlugin
allchunks
那什么时候需要传入第一个参数呢，那就得明白什么时候样式不会被抽取出来。
了解过code splittiog的同学便会知道，我们有些代码在加载页面的时候不会被使用时，使用code splitting，可以实现将这部分不会使用的代码分离出去，独立成一个单独的文件，实现按需加载。

那么如果在这些分离出去的代码中如果有使用require引入样式文件，那么使用ExtractTextPlugin这部分样式代码是不会被抽取出来的。
这部分不会抽取出来的代码，可以使用loader做一些处理，这就是ExtractTextPlugin.extract第一个参数的作用。
code splitting么？将该参数配置为true，那么所有分离文件的样式也会全部压缩到一个文件上。
引用 id为3的模块 即css2, 但是我们看 3 模块
的定义，为空函数， 它给出的解释是  removed by extract-text-webpack-plugin 实际
就是newExtractTextPlugin把相关的css全部移出去了

allChunks: true;时指定从所有模块中抽取CSS输出至单独CSS文件，包括异步引入的额外模块；此插件默认是只抽取初始模块内引入的CSS；
extract方法
1. use: 将CSS转换成模块的加载器；
2. fallback: 对于不被抽取输出至单独CSS文件的CSS模块使用的加载器，上例中`style-loader`即说明以内联方式使用，该加载器通常在`allChunks: false`时处理额外的模块；

### PostCSS
在css文件中使用@import引入其他样式文件，但是使用autoprefixer发现，import进来的样式没有处理
不推荐使用@import的，心细的童鞋可以看到最后生成的样式文件有样式是重复的。
所以一般我们应该是在js中使用require来引入样式文件

### CSS module
css-loader modules参数

### CSS压缩
通过配置 css-loader?minimize参数可以开启压缩输出最小的css。css的压缩实际是是通过cssnano实现的。
UglifyJsPlugin它既可以压缩js代码也可以压缩css代码。其实并不能说是在压缩css代码，本质来说还是压缩js代码，再将这块代码输出到css文件中。

## 图片 字体
图片压缩
[Klathmon/imagemin-webpack-plugin: Plugin to compress images with imagemin](https://github.com/Klathmon/imagemin-webpack-plugin)
sprite
[mixtur/webpack-spritesmith: Webpack plugin that converts set of images into a spritesheet and SASS/LESS/Stylus mixins](https://github.com/mixtur/webpack-spritesmith)

imagemin-mozjpeg

url-loader limit  最佳实践

[vue+webpack在“双十一”导购产品的技术实践 · Issue #24 · amfe/article](https://github.com/amfe/article/issues/24)

# 缓存

1.  同样的文件内容对应同样的名字，同时设置最大缓存失效期。这样在需要同一份代码时，浏览器总是使用本地缓存（连304请求都不需要）
2.  尽可能将很少变动的代码提取成单独的一份文件，使得这部分代码几乎总是被缓存，从而提高整体缓存利用率

[利用 webpack 处理开发与线上环境静态资源切换问题 - 前沿开发团队 - SegmentFault](https://segmentfault.com/a/1190000007178900)
[Caching](https://webpack.js.org/guides/caching/)
[Webpack中hash与chunkhash的区别，以及js与css的hash指纹解耦方案 - 才子锅锅 - 博客园](http://www.cnblogs.com/ihardcoder/p/5623411.html)
[你用 webpack 1.x 输出的 hash 靠谱不？ - zhenyong 的分享 - SegmentFault](https://segmentfault.com/a/1190000007309850)
[Webpack2 中的 NamedModulesPlugin 与 HashedModuleIdsPlugin - 前端 - 掘金](https://juejin.im/entry/58f0348ca0bb9f006a881e5f)
[用 webpack 实现持久化缓存](https://sebastianblade.com/using-webpack-to-achieve-long-term-cache/#webpackmd5hash)
[Webpack 真正的持久缓存实现|Blog - Yunfei](http://blog.yunfei.me/blog/webpack_long_term_caching.html)
[LoaderOptionsPlugin · webpack 中文文档(2.2)](http://www.css88.com/doc/webpack2/plugins/loader-options-plugin/)
[请教一个 webpack 打包 .vue 的问题 - V2EX](https://www.v2ex.com/t/350395)
[Webpack 的静态资源持久缓存 - 众成翻译](http://zcfy.cc/article/long-term-caching-of-static-assets-with-webpack-1204.html)

[webpack-chunk-hash/index.js at master · alexindigo/webpack-chunk-hash](https://github.com/alexindigo/webpack-chunk-hash/blob/master/index.js)
[adventure-yunfei/md5-hash-webpack-plugin: Plugin to replace a standard webpack chunkhash with md5.](https://github.com/adventure-yunfei/md5-hash-webpack-plugin)
[webpack-md5-hash/webpack_md5_hash.js at master · erm0l0v/webpack-md5-hash](https://github.com/erm0l0v/webpack-md5-hash/blob/master/plugin/webpack_md5_hash.js)

[Caching Assets Long Term with Webpack – Connect the Dots – Medium](https://medium.com/connect-the-dots/caching-assets-long-term-with-webpack-5ad24a4c39bd)
[Long-term caching of static assets with Webpack – Andrey Okonetchnikov – Medium](https://medium.com/@okonetchnikov/long-term-caching-of-static-assets-with-webpack-1ecb139adb95)
[webpack2-long-term-cache/webpack.config.js at master · blade254353074/webpack2-long-term-cache](https://github.com/blade254353074/webpack2-long-term-cache/blob/master/example6/webpack.config.js)

[Webpack Freestyle 之 Long Term Cache](https://zhuanlan.zhihu.com/p/27710902)
[scinos/webpack-plugin-hash-output: Plugin to replace webpack chunkhash with an md5 hash of the final file conent.](https://github.com/scinos/webpack-plugin-hash-output)

JS 资源的 [chunkhash] 由 webpack 计算，Images/Fonts 的 [hash] 由 webpack/file-loader 计算，提取的 CSS 的 [contenthash] 由 webpack/extract-text-webpack-plugin 计算

webpack 编译中会导致缓存失效的因素

在一个 webpack 编译出的分块 (chunk) 文件中，内容分为如下四部分：

a. 包含的模块的源代码
b. webpack 生成的模块 id (module id) (包括包含的模块 id, 以及该模块引用的依赖模块的 id)
c. webpack 用于启动运行的 bootstrap runtime
d. Chunk ID




# 区分环境
[survivejs/webpack-merge: Merge designed for Webpack (MIT)](https://github.com/survivejs/webpack-merge)
[HenrikJoreteg/hjs-webpack: Helpers/presets for setting up webpack with hotloading react and ES6(2015) using Babel.](https://github.com/HenrikJoreteg/hjs-webpack)
[分解配置文件 · Webpack - 从初学者到大师](https://mrshi.gitbooks.io/survivejs_webpack_chinese/chapter3-2.html)

## 开发
自动刷新 模块热替换
[模块热替换](https://doc.webpack-china.org/guides/hot-module-replacement)
[模块热替换(Hot Module Replacement)](https://doc.webpack-china.org/concepts/hot-module-replacement)
[webpack-dev-server原理分析与HMR实现 - CSDN博客](http://blog.csdn.net/liangklfang/article/details/56848925)
[webpack 插件拾趣 (1) —— webpack-dev-server - vajoy - 博客园](http://www.cnblogs.com/vajoy/p/7000522.html)
[搭建带热更新功能的本地开发node server - wonyun - 博客园](http://www.cnblogs.com/wonyun/p/7077296.html)
[liangklfangl/wcf: update webpack common configuration](https://github.com/liangklfangl/wcf)
[liangklfangl/webpack-hmr](https://github.com/liangklfangl/webpack-hmr)
[Express结合Webpack的全栈自动刷新 - acgtofe](http://acgtofe.com/posts/2016/02/full-live-reload-for-express-with-webpack)
[如何打造一个令人愉悦的前端开发环境（四）](https://zhuanlan.zhihu.com/p/22266335)

ip://webpack-dev-server

# JS打包策略

项目打包策略遵循以下几点原则：

- 选择合适的打包粒度，生成的单文件大小不要超过500KB(导致第一次加载很慢)
- 充分利用浏览器的并发请求，同时保证并发数不超过6
- 尽可能让浏览器命中304，频繁改动的业务代码不要与公共代码打包
- 避免加载太多用不到的代码，层级较深的页面进行异步加载

基于以上原则，我选择的打包策略如下：
- 第三方库如vue、jquery、bootstrap打包为一个文件
- 公共组件如弹窗、菜单等打包为一个文件
- 工具类、项目通用基类打包为一个文件
- 各个功能模块打包出自己的入口文件
- 各功能模块作用一个SPA，子页面进行异步加载

### dll
[Webpack的dll功能 - 前沿开发团队 - SegmentFault](https://segmentfault.com/a/1190000005969643)
[彻底解决Webpack打包性能问题 - 知乎专栏](https://zhuanlan.zhihu.com/p/21748318)
[教你如何玩转webpack.DllPlugin · Issue #6 · superpig/blog](https://github.com/superpig/blog/issues/6)

#### hash
使用`assets-webpack-plugin`得到dll js的hash，在`html-webpack-plugin`引用
 <%= htmlWebpackPlugin.options.bundleName %>

[Webpack DllPlugin打包小技巧 · BccSafe's Blog](http://www.bccsafe.com/web%20developer/2016/12/11/Webpack-DllPlugin-tips/)
[kossnocorp/assets-webpack-plugin: Webpack plugin that emits a json file with assets paths](https://github.com/kossnocorp/assets-webpack-plugin)


ProvidePlugin export default
expose-loader?

### CommonsChunkPlugin
[【译】webpack 小札: 充分利用 CommonsChunkPlugin() - 知乎专栏](https://zhuanlan.zhihu.com/p/26131812)
[CommonsChunkPlugin](https://doc.webpack-china.org/plugins/commons-chunk-plugin/)
[webpack的commonchunkplugin深度解析以及chunk和module内部结构 - CSDN博客](http://blog.csdn.net/liangklfang/article/details/55224360)

必须手工引用，能不能自动在html引用？
提取公共chunk
[webpack/examples/common-chunk-and-vendor-chunk at master · webpack/webpack](https://github.com/webpack/webpack/tree/master/examples/common-chunk-and-vendor-chunk)
提取相同业务公共chunk
[webpack/examples/multiple-commons-chunks at master · webpack/webpack](https://github.com/webpack/webpack/tree/master/examples/multiple-commons-chunks)
公共CSS
[webpack/examples/multiple-entry-points-commons-chunk-css-bundle at master · webpack/webpack](https://github.com/webpack/webpack/tree/master/examples/multiple-entry-points-commons-chunk-css-bundle)

[webpack/examples/multiple-entry-points at master · webpack/webpack](https://github.com/webpack/webpack/tree/master/examples/multiple-entry-points)

CommonsChunkPlugin中配置的name和entry中配置的入口之间有什么关系？
如果CommonsChunkPlugin 中配置的name在entry中存在，那么这个抽取的模块首先是包含enry中指定的js文件，然后再考虑包含抽取其他entry中的公用部分。

CommonsChunkPlugin中配置的name顺序有什么关系，每一个公用模块的抽取逻辑是什么？

这个没有找到官方的解释，通过实践，我认为应该是倒序考虑的，首先是启动脚本放在数组的最后一个文件中，例如boot中。每一个模块的逻辑如下：

首先看自己有没有对应的entry，如果有则抽取entry对应的模块，并递归抽取模块中公用的模块。例如common中的component1.js和component2.js共同依赖jquery，则common中也抽取jquery。

其次看数组中是否还有上一个元素，如果没有则将所有entry中剩余没有抽取的公用模块也都抽取出来，如果有则交给上一个元素，自己也就执行完了。例如vender先将Vue.js和vender.js抽取出来，然后发现还有common模块，所以自己就执行完了，common先将component1.js和component2.js抽取出来以后，发现上面没有文件了，所以就把entry中剩余没有抽取的公共模块也抽取出来了，比如page1.js和page2.js公用的componet4.js。

这样打包以后我们需要保证页面中文件引用的顺序，因为他们之间有了依赖关系，例如上面的配置页面的引用顺序应该是
1 boot.js
2 vender.js
3 common.js
然后是每一个页面的js page1.js 或者page2.js

children和async
children 使用代码拆分功能，一个 chunk 的多个子 chunk 会有公共的依赖。为了防止重复，可以将这些公共模块移入父 chunk。这会减少总体的大小，但会对首次加载时间产生不良影响。
如果预期到用户需要下载许多兄弟 chunks（例如，入口 trunk 的子 chunk），那这对改善加载时间将非常有用。
async 并非将公共模块移动到父 chunk（增加初始加载时间），而是使用新的异步加载的额外公共chunk。当下载额外的 chunk 时，它将自动并行下载。

#### manifest
[soundcloud/chunk-manifest-webpack-plugin: Allows exporting a manifest that maps entry chunk names to their output files, instead of keeping the mapping inside the webpack bootstrap.](https://github.com/soundcloud/chunk-manifest-webpack-plugin)
使用了md5指纹之后发现每次打包还是会发生变化？

这是由于webpack的处理机制导致的，webpack每次打包会把每个模块的配置信息如文件名、文件顺序、文件md5等信息作为配置打入js中，以便于其进行模块管理，而这部内容，每次打包都有可能发生变化，导致整个js文件名每次都会发生变化。

webpack提供了一个 manifest 的机制来剥出这个配置文件。我们需要使用 CommonsChunkPlugin 来将其剥离，同时使用 chunk-manifest-webpack-plugin 读取其内容导出另外一个文件，防止其内容变化导致整个js文件指纹发生变化：
``` javascript
// webpack.config.js
var ChunkManifestPlugin = require("chunk-manifest-webpack-plugin");

module.exports = {
  plugins: [
    new webpack.optimize.CommonsChunkPlugin({
      name: ["manifest"], // extracted manifest
      minChunks: Infinity,
    }),
    new ChunkManifestPlugin({
      filename: "chunk-manifest.json",
      manifestVariable: "webpackManifest"
    })
  ]
};
```
当然，对于前后端分离的项目，你也可以将这部分内容直接打入html以减少一个请求，使用 inline-manifest-webpack-plugin（ inline-manifest-webpack-plugin ） 即可
或者使用html-webpack-plugin

2. 仅把映射表导出为一个 JSON 文件，然后再内联到 html

简单来说，就是保持 runtime 位置不变，提取其中文件名映射表。可以通过 `chunk-manifest-webpack-plugin` 完成。

``` javascript
// webpack.config.js
var ChunkManifestPlugin = requir('chunk-manifest-webpack-plugin');
{
    plugins: [
        new ChunkManifestPlugin({filename: 'chunk-manifest.json', manifestVariable: 'webpackManifest'})
    ]
}
```

``` html
<!-- index.html -->
<script>
window.webpackManifest = {...};// 内联 chunk-manifest.json
</script>
```

可以看下新的 runtime 代码，里面引用文件名映射的地方发生了修改：

``` javascript
/******/    __webpack_require__.e = function requireEnsure(chunkId, callback) {
                    // ...
/******/            script.src = __webpack_require__.p + window["webpackManifest"][chunkId];
/******/            head.appendChild(script);
/******/        }
```

[szrenwei/inline-manifest-webpack-plugin: inline your Webpack manifest.js with a script tag to save http request](https://github.com/szrenwei/inline-manifest-webpack-plugin)
[DustinJackson/html-webpack-inline-source-plugin: Embed javascript and css source inline when using the webpack dev server or middleware](https://github.com/DustinJackson/html-webpack-inline-source-plugin)

### 第三方库
[【翻译向】webpack2 指南（下） | 抹桥的博客](https://www.kisnows.com/2017/01/18/webpack2-guide-3/)

## 分片/按需加载 Code Splitting
[Webpack 大法之 Code Splitting - 知乎专栏](https://zhuanlan.zhihu.com/p/26710831)
[lyyourc/webpack-code-splitting-demo: A demo 4 webpack code splitting & long term cache](https://github.com/lyyourc/webpack-code-splitting-demo)
[webpack源码学习系列之二：code-splitting（代码切割） · Issue #100 · youngwind/blog](https://github.com/youngwind/blog/issues/100)
[经典webpack入门（讲的很透彻 last update 2016.6.8 -m "附上source" ） - CNode技术社区](https://cnodejs.org/topic/57528759adc77ac170409e79)

### require.ensure
require.ensure(dependencies, callback) 是 Webpack 的按需加载方法，在一个 ensure 块中产生引用的文件都将被单独打包成分片文件，在运行时动态（运行到ensure语句时）加载。
直接写到 dependencies 参数中的模块不同点在于只会被加载，没有被 require 的时候不会被运行。
写到 dependencies 参数中的模块会被打入chunk中，当它被chunk中的其他模块再次异步调用时，不会再次生成chunk
require.ensure可传入第三个参数，必须是str，若两个拆分点有相同的第三参数会使用相同的chunk

```javascript
require.ensure(["./file"], function(require) {
  require("./file2");
});

// is equal to

require.ensure([], function(require) {
  require.include("./file");
  require("./file2");
});
```


### import then
import("./module").then((module) => {
  ...
}).catch(...)
npm i babel-plugin-syntax-dynamic-import -D
{
  "presets": [['es2015', {module: false}]],
  'plugins': ['syntax-dynamic-import']
}
[Code Splitting - Async](https://doc.webpack-china.org/guides/code-splitting-async/)


### require.include

可以使用 require.include 方法，直接引入模块，如下例子：  

```javascript
require.ensure(["./file"], function(require) {
  require("./file2");
});

// is equal to

require.ensure([], function(require) {
  require.include("./file");
  require("./file2");
});
```

这个方法可以实现一些分块的优化，当一个 chunk-parent 可能会异步引用多个 chunk-child 而这些 chunk-child 可能都包含了 moduleA, 那么可以在 chunk-parent 中 require.include('moduleA') 就可以避免重复加载 moduleA。

require.include('./b');

如果去掉前面的 require.include('./b')，chunk-one 和 chunk-two 里都会重复打入模块b。这里就是起到了一个依赖前置的作用（提前到了当前的依赖树，子依赖树继承）。而且模块b实际在被 require 的时候才会被运行。
webpack还提供require.include函数，将一个模块打包到当前chunk，但不运行这个模块；可以将多个child chunks都包含的模块提取到parent chunk中


### Chunk 优化

在一些特殊的场景可以利用如下这些插件来完成 Chunk 的优化，

* LimitChunkCountPlugin
* MinChunkSizePlugin
* AggressiveMergingPlugin


# 多页
[webpack多页应用架构系列（十二）：利用webpack生成HTML普通网页&页面模板 - 实用至上 - SegmentFault](https://segmentfault.com/a/1190000007126268)

``` js
function getEntry(globPath, pathDir) {
	var files = glob.sync(globPath);
	var entries = {},
		entry, dirname, basename, pathname, extname;

	for (var i = 0; i < files.length; i++) {
		entry = files[i];
		dirname = path.dirname(entry);
		extname = path.extname(entry);
		basename = path.basename(entry, extname);
		pathname = path.join(dirname, basename);
		pathname = pathDir ? pathname.replace(new RegExp('^' + pathDir), '') : pathname;
		entries[pathname] = ['./' + entry];
	}
	return entries;
}
var pages = Object.keys(getEntry('src/views/**/*.html', 'src/views/'));


function getEntry(sourcePath){
    var entrys = {};
    var basename;
    glob.sync(sourcePath).forEach(function(entry){
        basename = path.basename(entry,path.extname(entry));
        entrys[basename] = entry;
    });
    return entrys;
}
var pages = getEntry('./app/web/*.jade');
```

# 流程
[webpack-cleanup-plugin](https://www.npmjs.com/package/webpack-cleanup-plugin)
[johnagan/clean-webpack-plugin: A webpack plugin to remove your build folder(s) before building](https://github.com/johnagan/clean-webpack-plugin)


# 优化
[home](https://webpack.github.io/analyse/)
[Stats](https://webpack.js.org/configuration/stats/)
[Webpack Chart](http://alexkuz.github.io/webpack-chart/)

[Webpack 实用技巧高效实战](http://mp.weixin.qq.com/s?__biz=MzI1NjEwMTM4OA==&mid=2651231994&idx=1&sn=17a344ef74809ddd7e8e5b13b00c5652&scene=23&srcid=0729xg3ATCirw0eDZKmwjdC0#rd)


### 速度
[Webpack 打包优化之速度篇 | 晚晴幽草轩](https://jeffjade.com/2017/08/12/125-webpack-package-optimization-for-speed/)
[Webpack 性能优化 （一） — OneAPM](http://code.oneapm.com/javascript/2015/07/07/webpack_performance_1/)
[使用别名做重定向 | Webpack Performance](http://webpack-performance.com/2015/07/06/alias/)
[Optimising build performance, initial: 40s, incremental: 6s · Issue #1574 · webpack/webpack](https://github.com/webpack/webpack/issues/1574)
[webpack Performance: The Comprehensive Guide · Issue #15 · lcxfs1991/blog](https://github.com/lcxfs1991/blog/issues/15)
[加速 Webpack](https://www.ibm.com/developerworks/cn/web/wa-lo-expedite-webpack/index.html)

#### cache
[cache-loader](https://doc.webpack-china.org/loaders/cache-loader/)
[webpack-contrib/cache-loader: Caches the result of following loaders on disk.](https://github.com/webpack-contrib/cache-loader)

#### happypack
[happypack 原理解析 | Taobao FED | 淘宝前端团队](http://taobaofed.org/blog/2016/12/08/happypack-source-code-analysis/)
[happypack/webpack.config.js at master · amireh/happypack](https://github.com/amireh/happypack/blob/master/examples/cache-loader/webpack.config.js)
[Loader Compatibility List · amireh/happypack Wiki](https://github.com/amireh/happypack/wiki/Loader-Compatibility-List)
[使用happypack将vuejs项目webpack初始化构建速度提升50% | flyyang's Blog](https://flyyang.github.io/2017/03/09/%E4%BD%BF%E7%94%A8happypack%E5%B0%86vuejs%E9%A1%B9%E7%9B%AEwebpack%E5%88%9D%E5%A7%8B%E5%8C%96%E6%9E%84%E5%BB%BA%E9%80%9F%E5%BA%A6%E6%8F%90%E5%8D%8750/)

webpack-parallel-uglify-plugin

### 大小
[robertknight/webpack-bundle-size-analyzer: A tool for finding out what contributes to the size of Webpack bundles](https://github.com/robertknight/webpack-bundle-size-analyzer)
[webpack打包bundle.js体积大小优化 · Issue #65 · youngwind/blog](https://github.com/youngwind/blog/issues/65)
[更小体积的 Lodash | 小曹哥的博客](http://www.xiaocaoge.com/lodash-shrinking.html?utm_source=tuicool&utm_medium=referral)
[Webpack按需打包Lodash的几种方式 | Yusen's Blog | 学习弯道超车的技巧！](https://imys.net/20161217/webpack-use-lodash.html)
[Webpack 打包优化之体积篇 | 晚晴幽草轩](https://jeffjade.com/2017/08/06/124-webpack-packge-optimization-for-volume/)


源码打包
通过模块引入的方式在前端虽然方便，但也带来一些问题，经常使得打出来的文件非常庞大，有两个原因

1、随意的 npm install 引入了大量重复的模块，被反复打在了同一个bundle中，虽然 webpack 本身会对重复模块去重，但是我们一般会对 node_modules 中的包去除编译，而如果包提供者稍不注意，提供的打包版本中已经含有和项目中使用过的模块，就造成了资源浪费。

2、babel/webpack的打包辅助函数重复。如果依赖包也是使用webpack/babel打包，很多工具打进去的polyfill/helper代码，实际上会造成重复，如 Object.assgin 的 polyfill。

所以我们的实践是在内部提供的包，都推荐走源码打包的模式。

而我们在配置中经常会使用 exclude: /node_modules/ 直接排除掉了依赖包，如果我们相对其中的某些包进行源码编译，光写正则很难满足需求，其实webpack此处是可以提供一个function的，如：

``` javascript
exclude: pather => {
   if (needPass) {
      return true;
   } else {
      return false;
   }
}
```
### tree shaking
让webpack理解es6 的导入机制，例如现在有两个文件

``` javascript
// utils.js
export function foo() {
    return 'foo';
}
export function bar() {
    return 'bar';
}
// app.js
import { foo } from './utils'
```

如果不使用 tree-shaking，app.js编译输出为

``` javascript
/***/ function(module, exports) {

  'use strict';

  Object.defineProperty(exports, "__esModule", {
    value: true
  });
  exports.foo = foo;
  exports.bar = bar;
  // utils.js
  function foo() {
    return 'foo';
  }
  function bar() {
    return 'bar';
  }

/***/ }
```

可以看到上面包含了 foo 和 bar 两个函数，把utils里的内容全部打包进去了，如果使用tree-shaking，输出结果是这样的

``` javascript
/***/ (function(module, __webpack_exports__, __webpack_require__) {

"use strict";
/* harmony export (immutable) */ __webpack_exports__["a"] = foo;
/* unused harmony export bar */
// utils.js
function foo() {
  return 'foo';
}
function bar() {
  return 'bar';
}
/***/ }),
```

我们可以看到哪些方法是没有被使用的，你可以通过 `--optimize-minimize` 参数压缩代码剔除未被使用的函数

``` javascript
// 脚本
  "scripts": {
    "build": "webpack --optimize-minimize",
    "seebuild": "webpack"
  }

// 通过格式工具查看到的结果
function(t, e, n) {
  "use strict";
  function r() {
    return "foo"
  }
  e.a = r
}
```

已经没有bar了


tree-shaking 是指借助es6 `import export` 语法静态性的特点来删掉export但是没有import过的东西。要让tree-shaking工作需要注意以下几点：

* 配置babel让它在编译转化es6代码时不把`import export`转换为cmd的`module.export`，配置如下：

    ``` json
    "presets": [
      [
        "es2015",
        {
          "modules": false
        }
      ]
    ]
    ```

* 大多数分布到npm的库里的代码都是es5的，但是也有部分库（redux,react-router等等）开始支持tree-shaking。这些库发布到npm里的代码即包含es5的又包含全采用了es6 `import export` 语法的代码。
    拿redux库来说，npm下载到的目录结构如下：

    ```
    ├── es
    │   └── utils
    ├── lib
    │   └── utils
    ```
    其中lib目录里是编译出的es5代码，es目录里是编译出的采用`import export` 语法的es5代码，在redux的`package.json`文件里有这两个配置：

    ```
    "main": "lib/index.js",
    "jsnext:main": "es/index.js",
    ```
    这是指这个库的入口文件的位置，所以要让webpack去读取es目录下的代码需要使用jsnext:main字段配置的入口，要做到这点webpack需要这样配置：

    ``` js
    module.exports = {
      resolve: {
              mainFields: ['jsnext:main','main'],
          }
    };
    ```

    这会让webpack先使用jsnext:main字段，在没有时使用main字段。这样就可以优化支持tree-shaking的库。
