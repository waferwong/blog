
滚动原理
滚动特效
无线滚动
[skrollr](https://github.com/Prinzhorn/skrollr): 另一款实现一步滚动的开源库，使用人数众多，可实现各种狂拽酷炫掉渣天的前端效果，[看真相](http://prinzhorn.github.io/skrollr/)
[ScrollReveal](https://scrollrevealjs.org/)
[jquery.scrollTo](https://github.com/flesler/jquery.scrollTo): 在页面上以一个元素为起始以动画的方式移动(ScrollTo)到另一个元素， 支持回退等
[jScrollPane](https://github.com/vitch/jScrollPane): 自定义的滚动条，让所有浏览器都显示一样的滚动条
[onepage-scroll](https://github.com/peachananr/onepage-scroll): 提供类似于 iPhone6 展示页类似的效果，适用于单页应用，兼容到 IE8
[scrollMonitor](https://github.com/sakabako/scrollMonitor): 前端插件用来监控元素的滚动事件(进入、退出等)，性能很好
[ScrollMagic](https://github.com/janpaepke/ScrollMagic): 神奇的滚动交互效果插件，可以在滚动的过程中设置各种各样的动态效果
[infinite-scroll](https://github.com/paulirish/infinite-scroll): 滚动加载，滚动到最下到自动加载， Paul Irish 大神之作

[Using flexbox for horizontal scrolling navigation • iamsteve](https://iamsteve.me/blog/entry/using-flexbox-for-horizontal-scrolling-navigation)
[html - Flexbox and vertical scroll in a full-height app using NEWER flexbox api - Stack Overflow](https://stackoverflow.com/questions/14962468/flexbox-and-vertical-scroll-in-a-full-height-app-using-newer-flexbox-api)

[javascript中与Scroll有关的知识点 · Issue #207 · hehongwei44/my-blog](https://github.com/hehongwei44/my-blog/issues/207)
[javascript - How to scroll to an element inside a div? - Stack Overflow](https://stackoverflow.com/questions/635706/how-to-scroll-to-an-element-inside-a-div)
[scroll - 事件类型一览表 | MDN](https://developer.mozilla.org/zh-CN/docs/Web/Events/scroll)
[JS中offsetTop、clientTop、scrollTop、offsetTop各属性介绍 - 简书](https://www.jianshu.com/p/6719f7e1caea)

1：确保#wrapper下只有一个#scroller元素，也就是说#scroller元素不能有兄弟元素。
2：确保#scroller的高度设置正确。也就是说你想让内容在多大的一个框里面滑动要设置正确。这也是比较容易出错的地方。根据你的描述，我觉得你的这个高度可能和最里面内容的高度一样了。打开浏览器调试窗口去确认一下高度无误。
3：在初始化iScroll之后，如果又在其里面的内容层加载了新的内容，一定要将你的iScroll实例刷新。尤其是在利用Angular写移动端的页面的时候，Ajax请求完数据之后，在回调函数里面写一句刷新你的iScroll实例的代码。
[iscroll vue - Google 搜索](https://www.google.com.hk/search?newwindow=1&c2coff=1&safe=strict&q=iscroll+vue&oq=iscr&gs_l=psy-ab.3.2.0l4.211941.213039.0.216691.4.4.0.0.0.0.658.1047.3-1j0j1.2.0....0...1.1.64.psy-ab..2.2.1046.7TwpWOWMgic)
[Dafrok/vue-iscroll-view: IScroll-view component for Vue 2.x](https://github.com/Dafrok/vue-iscroll-view)
[Vue iscroll指令开发 - 简书](http://www.jianshu.com/p/8e838750c054)
[vue scroll - Google 搜索](https://www.google.com.hk/search?q=vue+scroll)
[ElemeFE/vue-infinite-scroll: An infinite scroll directive for vue.js.](https://github.com/ElemeFE/vue-infinite-scroll)

[better-scroll - Google 搜索](https://www.google.com.hk/search?q=better-scroll)
[better-scroll/scroll.vue at master · ustbhuangyi/better-scroll](https://github.com/ustbhuangyi/better-scroll/blob/master/example/components/scroll/scroll.vue)
[介绍 · better-scroll](https://ustbhuangyi.github.io/better-scroll/doc/zh-hans/#better-scroll 是什么)
[当 better-scroll 遇见 Vue - 知乎专栏](https://zhuanlan.zhihu.com/p/27407024)
[和 iscroll 比起来有什么 critical changes 吗？解决了什么 iscroll 难以解决的问题？ · Issue #36 · ustbhuangyi/better-scroll](https://github.com/ustbhuangyi/better-scroll/issues/36)

页面滚动
window.scrollTo(x-coord,y-coord )
该函数实际上和 window.scroll是一样的。 相对滚动可以参考 window.scrollBy，window.scrollByLines，和 window.scrollByPages。


1、onscroll


解释：当元素的滚动条滚动时触发的事件。

onscroll事件貌似任何实体元素都可以绑定，这里的实体元素包括DOM元素、window元素、document元素。

用法即：element.onscroll=function(){};

需要注意的是，滚动条一定要出现，而且滚动条是属于这元素的，例如：

``` html
    <div id="wrap" style="height:100px; overflow:auto;">
      <div id="inner" style="height:200px;">content</div>
    </div>
```

因为外层wrap的高度小于内层inner的高度，所以当设置overflow:auto时会出现滚动条，当拖动滚动条时就会触发wrap的onscroll事件，而不是inner的onscroll事件，即这滚动条属于wrap而不是属于inner，明白这点十分重要，对下面理解的scrollTop、scrollHeight一样道理。

2、scrollTop
解释：元素滚动条内的顶部隐藏部分的高度。

scrollTop属性只有DOM元素才有，window/document没有。
用法1：获取值 var top = element.scrollTop;//返回数字，单位像素
用法2：设置值 element.scrollTop = 200;

对上面的例子来说，控制滚动条的位置是wrap.scrollTop=xx;而不是inner.scrollTop，道理同上。

兼容性问题：获得整个文档scrollTop，IE是document.documentElement.scrollTop，FF/CH则是document.body.scrollTop.



3、scrollHeight
解释：元素滚动条内的内容高度。
scrollHeight同scrollTop属性一样，只有DOM元素才有，window/document没有。

不同的是scrollHeight是只读，不可设置。
兼容性问题：获取整个文档scrollHeight，IE/FF/CH都可以通过document.documentElement.scrollHeight或document.body.scrollHeight获得。

此外还有scrollLeft，scrollWidth，道理是一样的。

4、关于window.scroll()，window.scrollBy()，window.scrollTo()

这3个是全局函数，最新的IE/FF/CH都支持。

window.scroll(x,y)是让window滚动条滚动到那个x,y坐标。//x是水平坐标，y是垂直坐标。
window.scrollBy(-x,-y)是让window滚动条相对滚动到某个坐标，- 10即相对向左/向上滚动10像素。
window.scrollTo(x,y)和window.scroll(x,y)一样。

这3个函数在网上看用的不多，可能在IE/FF/CH各个版本支持不同吧，建议设置element.scrollTop属性的方法替代。

[WebKit Scrollbars](https://css-tricks.com/examples/WebKitScrollbars/)
[Custom Scrollbars in WebKit | CSS-Tricks](https://css-tricks.com/custom-scrollbars-in-webkit/)
[Styling Scrollbars | WebKit](https://webkit.org/blog/363/styling-scrollbars/)

.element::-webkit-scrollbar {display:none}

[Hiding Vertical Scrollbars with Pure CSS in Chrome, IE (6+), Firefox, Opera, and Safari – John Kurlak's Blog](https://blogs.msdn.microsoft.com/kurlak/2013/11/03/hiding-vertical-scrollbars-with-pure-css-in-chrome-ie-6-firefox-opera-and-safari/)

[【IScroll深入学习】解决IScroll疑难杂症 - 叶小钗 - 博客园](http://www.cnblogs.com/yexiaochai/p/3764503.html)
[高级选项 | iScroll 5 API 中文版](https://iiunknown.gitbooks.io/iscroll-5-api-cn/content/advance.html)
