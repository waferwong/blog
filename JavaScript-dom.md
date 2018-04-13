

[javascript 中的location.href 并不是立即执行的，是在所在function 执行完之后执行的。 - jinzhaoyoujiu - 博客园](http://www.cnblogs.com/jinzhaoyoujiu/p/javascript_location_href.html)

[JS获取上一访问页面URL地址document.referrer实践 « 张鑫旭-鑫空间-鑫生活](http://www.zhangxinxu.com/wordpress/2017/02/js-page-url-document-referrer/)
[document.referrer history back - Google 搜索](https://www.google.com.hk/search?q=document.referrer+history+back)

# url
[javascript - How to get the value from the GET parameters? - Stack Overflow](https://stackoverflow.com/questions/979975/how-to-get-the-value-from-the-get-parameters)
decodeURI
decodeURIComponent
encodeURI
encodeURIComponent

# event
[How to Create One-Time Events in JavaScript — SitePoint](https://www.sitepoint.com/create-one-time-events-javascript/)

```
Onunload与Onbeforeunload
Onunload，onbeforeunload都是在刷新或关闭时调用，可以在<script>脚本中通过window.onunload来指定或者在<body>里指定。区别在于onbeforeunload在onunload之前执行，它还可以阻止onunload的执行。
Onbeforeunload也是在页面刷新或关闭时调用，Onbeforeunload是正要去服务器读取新的页面时调用，此时还没开始读取；而onunload则已经从服务器上读到了需要加载的新的页面，在即将替换掉当前页面时调用。Onunload是无法阻止页面的更新和关闭的。而 Onbeforeunload 可以做到。曾经做一个考试系统，涉及到防止用户半途退出考试（有意或者无意）
```

### bfc
iOS返回时直接读取缓存，不执行js，但响应popstate
BFC
[javascript - Prevent safari loading from cache when back button is clicked - Stack Overflow](http://stackoverflow.com/questions/8788802/prevent-safari-loading-from-cache-when-back-button-is-clicked)
[javascript - How to prevent reloading of web page from cache while using mobile safari browser? - Stack Overflow](http://stackoverflow.com/questions/24524248/how-to-prevent-reloading-of-web-page-from-cache-while-using-mobile-safari-browse)

```javascript

window.addEventListener("pageshow", (e)=>{
    if(e.persisted){
        window.location.reload();
    }
});

$(window).on('unload', function () {
    // let a=[]
    // for(let i=0; i<10000000;i++){
    //     a.push(i)
    // }
    // Utils.setCache('b', a[a.length-1])
    Utils.setCache('unload', 'unload')
    setTimeout(()=>{
        console.log('1111')
    }, 2000)
});

$(document).on('visibilitychange', function () {
  if (document.visibilityState == 'hidden') {
    Utils.setCache('visibilitychange', 'visibilitychange')
    console.log('2222sync')
   setTimeout(()=>{
           console.log('2222')
       }, 2000)
  }
});
window.onbeforeunload = function(e) {
    Utils.setCache('onbeforeunload', 'onbeforeunload')
};
window.addEventListener('pagehide', function () {
    let a=[]
    for(let i=0; i<10000000;i++){
        a.push(i)
    }
    Utils.setCache('a', a[a.length-1])
    Utils.setCache('pagehide', 'pagehide')
})
```
iOS微信触发unload，pagehide
Android微信触发unload，pagehide，beforeunload
从其他app返回微信时候，会触发visibilitychange

[Page Visibility(页面可见性) API介绍、微拓展 « 张鑫旭-鑫空间-鑫生活](http://www.zhangxinxu.com/wordpress/2012/11/page-visibility-api-introduction-extend/)
[浏览器前进/后退缓存（BF Cache） | Harttle Land](http://harttle.land/2017/03/12/backward-forward-cache.html)

document.activeElement
document.hasFocus()
element.focus()

## 动态修改样式 换肤
className = ''
style.cssText = ''
.style.属性名 = 值;


Style对象是一个 DOM 对象的子对象，它的每个属性都和CSS的属性相对应。
Style对象的引用方法是： DOM对象.style.Style属性名

Style 对象的属性和 CSS 属性的区别是：
1. Style 属性要区分大小写，CSS 属性不区分大小写。
2. 由单个单词命名的 Style 属性和 CSS 属性同名。如：color、border、margin、width、height 等。只有一个特例，CSS 的float 属性对应的 Style 属性是 styleFloat 或 cssFloat。
3. 由多个单词组成的 Style 属性命名方法是：第一个单词小写，其后的单词首字母大写。而 CSS 属性是单词间用“-”分隔。如：font-family 对应于fontFamily，background-image 对应于 backgroundImage，border-top-width 对应于 borderTopWidth。

通过更改外联的css文件引用从而来更改btB的样式，操作很简单。代码如下：

首先得引用外联的css文件，代码如下：

``` html
<link href="css1.css" rel="stylesheet" type="text/css"  id="css"/>

function changeStyle4() {
    var obj = document.getElementById("css");
    obj.setAttribute("href","css2.css");
}
```
[使用vue + less 实现简单换肤功能 - CSDN博客](http://blog.csdn.net/u013884068/article/details/78186798)
[vue移动助手实践（一）——基于vue的换肤功能 - 掘金](https://juejin.im/post/59dae969f265da064c389644)
[你的网站可以一键变色吗？](https://zhuanlan.zhihu.com/p/29610065)
[Element Theme Preview](https://elementui.github.io/theme-preview/#/zh-CN)
