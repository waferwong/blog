# JavaScript
## 学习

[前端网老姚浅谈：怎么学JavaScript？ - 知乎专栏](https://zhuanlan.zhihu.com/p/23265155)

[phodal/fe: 《我的职业是前端工程师》 - Ebook：I'm a FrontEnd Developer](https://github.com/phodal/fe#%E6%A8%A1%E6%8B%9F%E7%9C%9F%E6%9C%BA%E8%AE%BE%E5%A4%87%E6%A8%A1%E6%8B%9F%E5%99%A8)

[单线程的Javascript | 前端工程师手册](https://leohxj.gitbooks.io/front-end-database/content/theory/single-thread.html)



[getify/You-Dont-Know-JS: A book series on JavaScript. @YDKJS on twitter.](https://github.com/getify/You-Dont-Know-JS)

[mqyqingfeng/Blog: 冴羽写博客的地方，预计写四个系列：JavaScript深入系列、JavaScript专题系列、ES6系列、React系列。](https://github.com/mqyqingfeng/Blog)
[30 seconds of code](https://30secondsofcode.org/)

## 最佳实践
[dreamapplehappy/effective-javascript: To be, or not to be, that is a question! 万剑归宗的无名和独霸天下的雄霸](https://github.com/dreamapplehappy/effective-javascript)
[dreamapplehappy/hacking-with-javascript: To be, or not to be, that is a question! 万剑归宗的无名和独霸天下的雄霸](https://github.com/dreamapplehappy/hacking-with-javascript)

[如何写出好的 JavaScript —— 浅谈 API 设计 - 十年踪迹的博客](https://www.h5jun.com/post/how-to-write-better-js-code.html)

[dwqs/blog: My New Blog's Address. Welcome to star](https://github.com/dwqs/blog)

[You-Dont-Need-jQuery/README.zh-CN.md at master · oneuijs/You-Dont-Need-jQuery](https://github.com/oneuijs/You-Dont-Need-jQuery/blob/master/README.zh-CN.md)
[You Might Not Need jQuery](http://youmightnotneedjquery.com/)


[clean-code-js/README.md at master · alivebao/clean-code-js](https://github.com/alivebao/clean-code-js/blob/master/README.md)
[高效的 JavaScript - 众成翻译](http://www.zcfy.cc/article/dev-opera-efficient-javascript-2320.html)


[How JavaScript works: memory management + how to handle 4 common memory leaks](https://blog.sessionstack.com/how-javascript-works-memory-management-how-to-handle-4-common-memory-leaks-3f28b94cfbec)
[denysdovhan/wtfjs: A list of funny and tricky JavaScript examples](https://github.com/denysdovhan/wtfjs#readme)
[Ten Things A Serious JavaScript Developer Should Learn | benmccormick.org](https://benmccormick.org/2017/07/19/ten-things-javascript/)
[mbeaudru/modern-js-cheatsheet: Cheatsheet for the JavaScript knowledge you will frequently encounter in modern projects.](https://github.com/mbeaudru/modern-js-cheatsheet)


## 函数式编程
[Introduction · JS函数式编程指南](https://llh911001.gitbooks.io/mostly-adequate-guide-chinese/content/)
[JS函数式编程指南 · GitBook](https://www.gitbook.com/book/llh911001/mostly-adequate-guide-chinese/details)
[The Rise and Fall and Rise of Functional Programming (Composing Software)](https://medium.com/javascript-scene/the-rise-and-fall-and-rise-of-functional-programming-composable-software-c2d91b424c8c)
[Glossary of Modern JavaScript Concepts: Part 1](https://auth0.com/blog/glossary-of-modern-javascript-concepts/)
[用函数式编程对JavaScript进行断舍离 | Fundebug博客](https://blog.fundebug.com/2017/09/13/how-i-rediscovered-my-love-for-js/)
[Rethinking JavaScript: The if statement – Hacker Noon](https://hackernoon.com/rethinking-javascript-the-if-statement-b158a61cd6cb)

[7 tips to handle undefined in JavaScript | Dmitri Pavlutin](https://dmitripavlutin.com/7-tips-to-handle-undefined-in-javascript/)


## string
[JavaScript 字符串实用常操纪要 | 晚晴幽草轩](http://jeffjade.com/2016/11/24/116-JavaScript-string-operation/)

[strman - Documentation](https://dleitee.github.io/strman/)

## Number
按0.5取舍数据，其实是四舍五入的变形，只要将原数据放大2倍，进行四舍五入，再除以2还原数据，即实现将数据按0.5进行取舍。

## Array
JavaScript的数组原生就有reverse的API用以翻转数组，因此如果要得到降序的排列，只需要：
`var sorted = _(contacts).sortBy("age").reverse();`
[JavaScript中清空数组的三种方式 - snandy - 博客园](http://www.cnblogs.com/snandy/archive/2011/04/04/2005156.html)

push
unshift

concat 返回新数组

const arr1 = ['a', 'b', 'c', 'd', 'e'];
const arr2 = [...arr1, 'f']; // ['a', 'b', 'c', 'd', 'e', 'f']  
const arr3 = ['z', ...arr1]; // ['z', 'a', 'b', 'c', 'd', 'e']

pop
shift

splice

slice

groupBy
[What is the most efficient method to groupby on a javascript array of objects? - Stack Overflow](http://stackoverflow.com/questions/14446511/what-is-the-most-efficient-method-to-groupby-on-a-javascript-array-of-objects)

[Array.from() - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/from)
[ES6 生成 range 数组和 random 数组 - 网道 - SegmentFault](https://segmentfault.com/a/1190000003935593)

## Object
[Object comparison in JavaScript - Stack Overflow](http://stackoverflow.com/questions/1068834/object-comparison-in-javascript)

## Date
[Get difference between 2 dates in javascript? - Stack Overflow](http://stackoverflow.com/questions/3224834/get-difference-between-2-dates-in-javascript)
[Date - JavaScript | MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date)
[Simplified](http://dygraphs.com/date-formats.html)

2016-01-01
aDate = sDate1.split("-");
oDate1 = new Date(aDate[1] + '-' + aDate[2] + '-' + aDate[0]); //转换为12-18-2002格式 FF不支持
oDate1 = new Date(Date.parse(sDate1));  // IE8不支持 ECMA5
oDate1 = new Date(aDate[0] + '/' + aDate[1] + '/' + aDate[2]);

[date-fns/date-fns: ⏳ Modern JavaScript date utility library ⌛️](https://github.com/date-fns/date-fns)
[smallwins/spacetime: A lightweight timezone library](https://github.com/smallwins/spacetime)
[timeago.js/README_zh.md at master · hustcc/timeago.js](https://github.com/hustcc/timeago.js/blob/master/README_zh.md)
>timeago.js 是一个非常简洁、轻量级、不到 2kb 的很简洁的 Javascript 库，用来将 datetime 时间转化成类似于*** 时间前的描述字符串，例如：“3小时前”。

[aweary/tinytime: A straightforward date and time formatter in <1kb](https://github.com/aweary/tinytime)

## 函数
函数都会返回一个值. 如果方法体中没有返回语句，那么方法会返回undefined
[JavaScript 之 this 详解 | 晚晴幽草轩](http://www.jeffjade.com/2015/08/03/2015-08-03-javascript-this/)
[通过示例学习JavaScript闭包 | Fundebug博客](https://blog.fundebug.com/2017/08/07/javascript-closure-examples/)
[忍者级别的JavaScript函数操作 - 从前端到全栈 - SegmentFault](https://segmentfault.com/a/1190000011792660)
[理解 JavaScript 的函数 - 可译网](https://coyee.com/article/11179-understand-functions-in-javascript)
