
[浅谈Web图像优化](https://zhuanlan.zhihu.com/p/30362177)

# 事件
图片加载完成回调
img loaded
#imgId.onload = ()=>{

}
document.getElementById('topBanner').onload
#imgId.onreadystatechange = ()=>{
    if(img1.readyState=="complete"||img1.readyState=="loaded"){
        p1.innerHTML ='readystatechange:loaded'
    }
}
轮询 img.complete （如果图片加载失败，在IE中complete的值一直为false,而其他浏览器最后会变为true。）
function imgLoad(img, callback) {
            var timer = setInterval(function() {
                if (img.complete) {
                    callback(img)
                    clearInterval(timer)
                }
            }, 50)
        }
        imgLoad(img1, function() {
            p1.innerHTML('加载完毕')
        })

https://github.com/desandro/imagesloaded

[jquery - Check if an image is loaded (no errors) in JavaScript - Stack Overflow](https://stackoverflow.com/questions/1977871/check-if-an-image-is-loaded-no-errors-in-javascript)

[javascript get img - Google 搜索](https://www.google.com.hk/search?q=javascript+get+img)


[[已解决] 图片 CSS：怎样才能 “响应式 + 固定宽高比例”？ · Ruby China](https://ruby-china.org/topics/17011)

### 延迟加载
[lazysizes](https://github.com/aFarkas/lazysizes): 功能强大的图片延迟加载工具，可以首先加载一个低质量的图片，然后再加载高质量的图片
[图片延迟加载方案 - 简书](http://www.jianshu.com/p/dc5fd46ff22c)
[ApoorvSaxena/lozad.js: 🔥 Highly performant, light ~0.7kb and configurable lazy loader in pure JS with no dependencies for responsive images, iframes and more](https://github.com/ApoorvSaxena/lozad.js)

渐进式图片加载 progressive-image
[59.适用于 vue.js 和原生 js 的渐进式图片加载 · Issue #64 · ccforward/cc](https://github.com/ccforward/cc/issues/64)

[图片加载时使用 SVG 作为图片 placehold](https://zhuanlan.zhihu.com/p/31231427)

### 上传 压缩
[H5上传图片 - 腾讯Web前端 IMWeb 团队社区 | blog | 团队博客](http://imweb.io/topic/568225bb57d7a6c47914fbf2)
[input file 样式 - Google 搜索](https://www.google.com.hk/search?q=input+file+%E6%A0%B7%E5%BC%8F)

* 基本原理是通过canvas渲染图片，再通过 `toDataURL` 方法压缩保存为base64字符串（能够编译为jpg格式的图片）。
* 但由于兼容性的问题，坑很多，所以大部分代码是为了解决兼容性而已。

1.  收到传入的文件后，创建一个 canvas 对象 和 blob 对象（其实也就是对应的文件引用，所以能被 img src直接引用）

2.  创建 img 对象，标记允许跨域处理，src 设置为 blob，接下来就是开始压缩了。

3.  开始压缩，获取图片旋转的方向，计算用户设置的尺寸，设置canvas

* 发现是iOS低版本，异步载入iOS兼容文件，调整为正确方向，保存压缩，并返回 base64
* 其他情况，调整为正确方向
    其他情况1：发现android低版本，异步载入android兼容文件，保存压缩，并返回 base64
    其他情况2：保存压缩，并返回 base64

4.  尽可能释放内存

hack
1.图片方向处理
2.安卓微信压缩问题hack
3.IOS6/7压缩扭曲
4.多张上传（如果浏览器支持）

WebUploader，由Baidu FEX 团队开发，以H5为主，FLASH为辅，兼容 IE6+，iOS 6+, android 4+，采用大文件分片并发上传，极大的提高了文件上传效率，看了官方文档就知道，能满足你所需要的所有功能，一言以蔽之，大而全；至于缺点，大概就是插件体积太大了，自带样式文件，而且还要依赖jquery类库
[应用于移动端注意事项 · Issue #185 · fex-team/webuploader](https://github.com/fex-team/webuploader/issues/185)
[vue webuploader 组件开发](https://www.bbsmax.com/A/GBJrebNBz0/)
vue-webuploader

localResizeIMG
[think2011/localResizeIMG: 前端本地客户端压缩图片，兼容IOS，Android，PC、自动按需加载文件](https://github.com/think2011/localResizeIMG)
[koa-upload/app.js at master · think2011/koa-upload](https://github.com/think2011/koa-upload/blob/master/app.js)

LUploader，纯原生js写的，不依赖任何类库，压缩后的js文件只有5k
[xfhxbb/LUploader: LUploader移动端图片压缩上传插件](https://github.com/xfhxbb/LUploader)

[mhbseal/html5ImgCompress: html5图片压缩，支持pc，mobile（ios/android）和multiple](https://github.com/mhbseal/html5ImgCompress)
[imgResize/README.md at master · CommanderXL/imgResize](https://github.com/CommanderXL/imgResize/blob/master/README.md)

[微信分享图片压缩问题解决方案](https://mp.weixin.qq.com/s?__biz=MzI2NzI4MTEwNA==&mid=2247484423&idx=1&sn=bd282cbc6d28ff8a19dfb8ac7e2a350c&chksm=ea8073b8ddf7faaef3b46a3c0ec59f1ba6649de1d6dce974d2eba42eb41906c5593f0ce34de0&mpshare=1&scene=1&srcid=0811VAUACFfymWdNOBPp8xoh&key=b14ef81558367f70927d52e9d0bdc886e534853757d41f0c1f6b50ab155bcdfb7d34908fca181725eed0a4cc59d60d63c282e6518f62723d98e180ada71189549805f74f312b825db293b2616a125f04&ascene=0&uin=NzIwMTQ2MDQw&devicetype=iMac+MacBookPro12%2C1+OSX+OSX+10.11.6+build(15G31)&version=12020810&nettype=WIFI&fontScale=100&pass_ticket=RZ8We%2FyTrXvssuat0BeMeVquC2oKFSI96Kzg7AAoEPLLE4cCAoDFBlqhSakAqCWh)

### 预览
[henrygd/bigpicture: Lightweight JavaScript image / video viewer. Supports Youtube and Vimeo.](https://github.com/henrygd/bigpicture)
[fancyBox](https://github.com/fancyapps/fancyBox): 一个用于放大缩小图片、Web 内容或者多媒体元素的库，优雅大方
[PhotoSwipe FAQ](http://photoswipe.com/documentation/faq.html)

[jquery - Get the real width and height of an image with JavaScript? (in Safari/Chrome) - Stack Overflow](https://stackoverflow.com/questions/318630/get-the-real-width-and-height-of-an-image-with-javascript-in-safari-chrome/9361340)
[Can I use... Support tables for HTML5, CSS3, etc](https://caniuse.com/#search=naturalHeight)

[「前端」webp图片适配流量优化 · Issue #10 · ShowJoy-com/showjoy-blog](https://github.com/ShowJoy-com/showjoy-blog/issues/10)
[前端图片引入方式神演算](https://zhuanlan.zhihu.com/p/24315362)
[图片资源Base64化在H5页面里有用武之地吗？ | Aotu.io「凹凸实验室」](https://aotu.io/notes/2016/03/04/can-we-use-base64-in-h5-webapps/)
