

1.  
2.  [Flat UI Colors__](http://flatuicolors.com/) - 漂亮的扁平化配色；
3.  [Material Design Lite__](http://getmdl.io/index.html) - 基于谷歌 Material Design 的前端框架；
5.  [Section separators__](http://tympanus.net/Development/SectionSeparators/) - CSS 区域分割；
6.  [Topcoat__](http%3A//topcoat.io/) - 专注为简洁、快速的 Web 应用提供 CSS 开发的工具；
7.  [Create Ken Burns Effect__](http://www.kirupa.com/html5/ken_burns_effect_css.htm) - 利用 CSS3 实现的 Ken burns 特效；
8.  [DynCSS__](http%3A//www.vittoriozaccaria.net/dyn-css/) - 用于分析 CSS -dyn-属性规则，并使其具备动态属性；
9.  
10.  [CSSpin__](http://webkul.github.io/csspin/) - 丰富的 CSS 加载动画；
11.  [Feather icons__](http://feathericons.com/) - 简单、漂亮的开源图标库；
12.  [Ion icons__](http%3A//ionicons.com/) - 专为 Ionic 框架设计的图标字体；
13.  [Font Awesome__](http%3A//fontawesome.io/) - 可缩放的矢量图标字库；
14.  [Font Generator__](http%3A//brandmark.io/font-generator/) - 在线字体生成器；
15.  [On/Off FlipSwitch__](http://proto.io/freebies/onoff/) - 在线创建纯 CSS3 动画开关效果；
16.  [UIkit__](http://getuikit.com/) - 轻量级的模块化前端框架；
17.  [Bootstrap__](http%3A//getbootstrap.com/) - 著名的前端框架；
18.  [Foundation__](http%3A//foundation.zurb.com/) - 著名的前端框架。

[CSS3 Mask 安利报告 | Aotu.io「凹凸实验室」](https://aotu.io/notes/2016/10/19/css3-mask/)

[前端每周清单半年盘点之 CSS 篇](https://zhuanlan.zhihu.com/p/29065136?group_id=888348684608245760)
[CSS参考手册_web前端开发参考手册系列](http://css.doyoe.com/)
[DevDocs — CSS documentation](http://devdocs.io/css/)
[The invisible parts of CSS - Mike Riethmuller](https://madebymike.com.au/writing/the-invisible-parts-of-css/)
[从Chrome源码看浏览器如何计算CSS](https://zhuanlan.zhihu.com/p/25380611?hmsr=toutiao.io&refer=dreawer&utm_medium=toutiao.io&utm_source=toutiao.io)

[8 CSS gotchas to start your morning off right – Isaac Lyman – Medium](https://medium.com/@isaaclyman/8-css-gotchas-to-start-your-morning-off-right-c5daade0731d)
[The CSS Box Model Explained by Living in a Boring Suburban Neighborhood](https://medium.freecodecamp.com/css-box-model-explained-by-living-in-a-boring-suburban-neighborhood-9a9e692773c1)
[Building performant expand & collapse animations  |  Web  |  Google Developers](https://developers.google.com/web/updates/2017/03/performant-expand-and-collapse)

[hunzaboy/CSS-Checkbox-Library: A huge library of CSS Checkboxes for every taste.](https://github.com/hunzaboy/CSS-Checkbox-Library)

# 核心
包含块
[详解CSS盒模型 - WEB前端 - 伯乐在线](http://web.jobbole.com/84092/)
[CSS块级元素和行内元素 | 晚晴幽草轩](https://jeffjade.com/2015/06/24/2015-06-24-css-block-inline/)

## CSS组织 工程化
[编写模块化 CSS（第 1 部分） - BEM - 众成翻译](http://zcfy.cc/article/3042)
[6种组织CSS的方法](https://zhuanlan.zhihu.com/p/28085207)
[分类方法 - CSS规范 - 规范 - NEC : 更好的CSS样式解决方案](http://nec.netease.com/standard/css-sort.html)


## CSS框架
css reset 采用 normalize.css
[HTML5 css reset « 张鑫旭-鑫空间-鑫生活](http://www.zhangxinxu.com/wordpress/2010/08/html5-css-reset/)
[primer/primer-css: The CSS framework that powers GitHub's front-end design.](https://github.com/primer/primer-css)
[Primer](http://primercss.io/)
[2017 年 20 个最佳的极简 CSS 框架](https://zhuanlan.zhihu.com/p/27767048)

## CSS预处理器 CSS Preprocessors
[SASS用法指南 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2012/06/sass.html)
[stylus中文文档 » 综述 » 张鑫旭-鑫空间-鑫生活](http://www.zhangxinxu.com/jq/stylus/)
[Compass Home | Compass Documentation](http://compass-style.org/)

sass 存在 Duplicate import problem

暂时没去解决，现有以下可以解决办法

Extract File
Webpack loader global
Webpack 去重代码(待证实)
cssnano(推荐)
[去除冗余 – 精简您的CSS样式代码 « 张鑫旭-鑫空间-鑫生活](http://www.zhangxinxu.com/wordpress/2010/02/%e5%8e%bb%e9%99%a4%e5%86%97%e4%bd%99-%e7%b2%be%e7%ae%80%e6%82%a8%e7%9a%84css%e6%a0%b7%e5%bc%8f%e4%bb%a3%e7%a0%81/)
结论是尽量不要使用引用, variable或者function之类的可以使用

参考地址 http://ryerh.com/sass/2016/03/15/vue-webpack-duplicate-sass-import.html

## PostCSS
[PostCSS 配置指北 - 前端 - 掘金](https://juejin.im/entry/57e67ac28ac247005bc9562a)
[Coding-Guide/PostCSS配置指北.md at master · ecmadao/Coding-Guide](https://github.com/ecmadao/Coding-Guide/blob/master/Notes/CSS/PostCSS%E9%85%8D%E7%BD%AE%E6%8C%87%E5%8C%97.md)
[webpack之postcss集成 - 小小前端 - SegmentFault](https://segmentfault.com/a/1190000004592944)
[使用 PostCSS 进行 CSS 处理](https://www.ibm.com/developerworks/cn/web/1604-postcss-css/)
[postCSS-loader配置,让css随心所欲 | 三寸稚笔](http://robin-front.github.io/2016/04/09/postCSS-loader%E9%85%8D%E7%BD%AE/)
[webpack2.0配置postcss-loader - 苏荷酒吧 - 博客园](http://www.cnblogs.com/sonwrain/p/6479153.html)

## 响应式 Responsible WEB Design
[scottjehl/picturefill: A responsive image polyfill for <picture>, srcset, sizes, and more](https://github.com/scottjehl/picturefill)
[amfe/lib-flexible: 可伸缩布局方案](https://github.com/amfe/lib-flexible)
[Propeller - Front-end framework based on Material Design & Bootstrap](http://propeller.in/index.html)
[（译）关于响应式的另一种思考](https://zhuanlan.zhihu.com/p/27258076)

渐进增强、可访问性

## 布局
不考虑兼容的情况下，一维用 flexbox，二维用 css grid，单位 rem/vm vw，更改盒模型为 box-sizing减少padding和border的计算；考虑兼容性则使用 bootstrap3 提供的grid布局方案

[CSS 中，为什么绝对定位（absolute）的父级元素必须是相对定位（relative）？ - 知乎](https://www.zhihu.com/question/19926700)
[CSS 相对|绝对(relative/absolute)定位系列（一） « 张鑫旭-鑫空间-鑫生活](http://www.zhangxinxu.com/wordpress/2010/12/css-%E7%9B%B8%E5%AF%B9%E7%BB%9D%E5%AF%B9%E5%AE%9A%E4%BD%8D%E7%B3%BB%E5%88%97%EF%BC%88%E4%B8%80%EF%BC%89/)

[CSS实现垂直居中的5种方法](https://www.qianduan.net/css-to-achieve-the-vertical-center-of-the-five-kinds-of-methods/)

[基于视口单位的网页排版 · Issue #5 · dwqs/blog](https://github.com/dwqs/blog/issues/5)
[REM vs EM – The Great Debate | Zell Liew](https://zellwk.com/blog/rem-vs-em/)
calc
[CSS3的calc()使用_calc, css3属性详解 教程_w3cplus](http://www.w3cplus.com/css3/how-to-use-css3-calc-function.html)

### flex
[CSS Flexbox 学习指南、工具与框架](https://zhuanlan.zhihu.com/p/25253176)
[拥抱flex布局 | 暗雨HAPPY的Blog](http://sxyblog.com/2017/01/15/%E6%8B%A5%E6%8A%B1%20Flex%20%E5%B8%83%E5%B1%80/)
[更棒，更简洁的栅格系统 — Solved by Flexbox — 更干净, 无 hack 的 CSS](https://hufan-akari.github.io/solved-by-flexbox/demos/grids/)
[移动端全兼容的flexbox速成班 - 前端技术 - 腾讯ISUX](https://isux.tencent.com/flexbox.html)
[Flex 布局教程：语法篇 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
[angular实现日历组件 - 知乎专栏](https://zhuanlan.zhihu.com/p/26418235)
[Flexbox and CSS Grid Part. 1](https://tech.io/playgrounds/7859/flexbox-and-css-grid-part--1)
[Flexbox Cheatsheet](https://yoksel.github.io/flex-cheatsheet/)
[flex布局踩过的那些坑 - 前端CSS - SegmentFault](https://segmentfault.com/a/1190000006559564)
[philipwalton/flexbugs: A community-curated list of flexbox issues and cross-browser workarounds for them.](https://github.com/philipwalton/flexbugs)

在flex-item元素中使用text-overflow:hidden；white-space:nowrap；进行省略文字的操作。

发现flex-item失控了，长度完全根据子元素中的文字决定，把其他同级元素挤跑。
给flex-item元素增加min-width:0

### grid
[CSS 终极之战：Grid VS Flexbox](https://zhuanlan.zhihu.com/p/31952490)
[[译]使用 CSS Grid：以兼容不支持栅格化布局的浏览器 - 掘金](https://juejin.im/post/5a3f494d6fb9a0450a678f8d)

nth-child
[CSS3 :nth-child() 选择器](http://www.w3school.com.cn/cssref/selector_nth-child.asp)

tr:nth-child(even) {background: #CCC}
tr:nth-child(odd) {background: #FFF}

height
min-height
max-height
overflow
[height | CSS-Tricks](https://css-tricks.com/almanac/properties/h/height/)
[CSS中height:100%和height:inherit的异同 « 张鑫旭-鑫空间-鑫生活](http://www.zhangxinxu.com/wordpress/2015/02/different-height-100-height-inherit/)

line-height
[css行高line-height的一些深入理解及应用 « 张鑫旭-鑫空间-鑫生活](http://www.zhangxinxu.com/wordpress/2009/11/css%E8%A1%8C%E9%AB%98line-height%E7%9A%84%E4%B8%80%E4%BA%9B%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3%E5%8F%8A%E5%BA%94%E7%94%A8/)
[CSS基础line-height和vertical-align属性 – 熊建刚的博客](http://blog.codingplayboy.com/2016/12/11/css_line-height_vertical-align/)


基线
[CSS基线之道](https://www.qianduan.net/css-baseline-road/)

[CSS :not()选择器使用技巧 - CSS效果 - Front-End - NalanXue's Blog](http://blog.mingsixue.com/effect/CSS-not-use-skill.html)

table
隔行变色
[css - Hover not working with nth-child - Stack Overflow](http://stackoverflow.com/questions/16193161/hover-not-working-with-nth-child)
thead的tr和隐藏的tr会不会影响


折行
[你真的了解word-wrap和word-break的区别吗？ - 无双 - 博客园](http://www.cnblogs.com/2050/archive/2012/08/10/2632256.html)
