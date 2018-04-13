## 参考
[Web App防坑手册 - kpaxqin - SegmentFault](https://segmentfault.com/a/1190000005864691?f)
[详细解剖大型H5单页面应用的核心技术点 - 【艾伦】 - 博客园](http://www.cnblogs.com/aaronjs/p/6768852.html)
[重新搭建性能监控体系——第三章：单页应用的特点带来的挑战 · Issue #5 · HuazhuLi/Blog](https://github.com/HuazhuLi/Blog/issues/5)

[vue-axios-github/router.js at master · superman66/vue-axios-github](https://github.com/superman66/vue-axios-github/blob/master/src/router.js)

## 微信公众号
[微信公众号 SPA - Google 搜索](https://www.google.com.hk/search?q=%E5%BE%AE%E4%BF%A1%E5%85%AC%E4%BC%97%E5%8F%B7+SPA)

## 入口
main.js
index.html
App.vue

index.html
```html
<body>
	<div id="app">
		<router-view></router-view>
	</div>
</body>
```
```
<template>
    <router-view></router-view>
</template>
<script>
    export default {

    }
</script>
```


```
index.html
<body>
  <div id="app"></div>
</body>

main.js
new Vue({
  el: '#app',
  router,
  store,
  template: '<App/>',
  components: {
    App
  }
})
或者
new Vue({
  router,
  store,
  render: h => h(App)
}).$mount('#app')

App.vue
<template>
    <div id="app">
        <router-view></router-view>
    </div>
</template>

<script>
export default {
    name: 'app',
}
</script>

router.js
export default new Router({
  routes: [
    {
      path: '/',
      name: 'home',
      component: Home
    }
  ]
}
```

## 路由

[vuejs2 - Difference between beforeRouteUpdate and watching '$route' - Vue.js? - Stack Overflow](https://stackoverflow.com/questions/47184331/difference-between-beforerouteupdate-and-watching-route-vue-js)

合理的运用子路由，避免ajax请求

在路由层面，往往对路由层面理解不够深的开发者来说，子路由感觉可能就是一个摆设，通常都是一个页面一个路由。

此时就会出现了明显的问题，每当切换到下个路由或者返回到前一个路由，都会重新执行生命周期，大多数数据的来源都是在 created 里去请求的。

子路由的原理

先说说子路由的原理，子路由原理则是拿到单个 .vue 文件的实例，通过append节点到父路由设定的 dom 节点里，当切换路由的时候，则是把父节点插入的子路由的节点再进行移除。

路由切换生命周期发生了那些变化

{
path:'menus',
components:Menus,
children:[
  {
    path: 'dishDetail',
    components:DishDetail
  }
]
}

从上面一个基本的路由可以看出，DishDetail 是 Menus 的子路由，对于点餐项目，Menus 是点餐的主页面，DishDetail 是菜单详情页 Menus 通常进入页面的时候几乎所有的数据向后台请求都是经过这个页面进行操作。

而我做的云客官项目，此页面向后台发送了五个数据请求，只能说这是避免不了的请求
 DishDetail 是菜单详情页，同样也是用户频繁进行的页面，操作率还是很高的，为了避免重复发送ajax请求，设定 DishDetail 为 Menus 的子路由。

当进入 DishDetail 路由的时候，只是把 DishDetaili 当作 dom 插入 Meuns 页面的中，DishDetail 会执行自己的生命周期，返回到 Menus 路由的时候， DishDetail 路由只是把自己当 Menus 路由中移除，同时 destory 掉自己。

无论前进还是后退，Meuns 路由并没有销毁，也没有加载。

{
path:'menus',
components:Menus,
}，
{
path: 'dishDetail',
components:DishDetail
}

DishDetail 和 Menus 是同级路由，通过 Menus 路由进入到 Detail 路由的时候，两者都发生了变化，Menus 路由则是进行销毁，加载进来的是 DishDetail 路由，一旦路由进行销毁再重新加载此路的时候，都需要重新执行生命周期。

如何不通过子路由来加载 DishDetail 的话，每次进入详情页再返回之后，都会重新执行 Menus 的生命周期，执行五次 AJAX 请求，能避免 HTTP 请求则避免。

vuex 跨路由操作，必然只能在子路由操作

在 h5 页面中，当使用 vuex 进行跨路由操作时，会导致当用户刷新页面的时候，vuex 同样的也会初始化，同时就会导致报错。

那如果是子路由的话，必然所有数据都是通过父路由进行数据操作完毕之后，放入数据共享，然后再由子路去获取，这样就算刷新页面不会导致数据错误。

#### 路由[](https://aotu.io/notes/2017/07/17/The-Exploration-and-Practice-of-Vue/index.html#%E8%B7%AF%E7%94%B1)

一个路由子项如下：
```
    {

    name: 'index', path: '/index',

    meta: {title: '陪伴空间', pv: 50, profiles: true, visitor: true, verify () { return true }},

    components: {default: Index2, navbar: Navbar}

    }
```

其中，配置里的 meta 包含了该页面（视图）的配置信息：

* title：页面的标题
* pv：用作记录页面的 PV
* profiles：用于判断是否需要有孩子才能进入这个页面
* visitor: 是否支持游客访问
* verify：如果支持游客访问，可选的额外的放行校验

> 问题：在 ios 里，单页面应用切换视图时页面标题不能更新  
> 解决：切换路由时用 iframe 加载一个空页面即可触发 title 更新，如下所示

```
    const iframeLoad = (src) => {

    let iframe = document.createElement('iframe')

      iframe.style.display = 'none'

      iframe.src = src

    document.body.appendChild(iframe)

      iframe.addEventListener('load', function() {

        setTimeout(function() {

          iframe.remove()

        }, 0)

      })

    }
```

路由中还要处理比较多的事情，在 `router.beforeEach` 中处理传进页面的参数，请求登陆状态和档案数据等基本接口，上报 PV，在 `router.afterEach` 中处理比较次要的事情。

## vuex
[Vuex新手入门指南 - 知乎专栏](https://zhuanlan.zhihu.com/p/25701238)
[Vuex——Vue单页应用状态管理架构 | 全面回忆 | zhangdiweb | zhangdi | hahacoo](http://zhangdiweb.com/2016/09/08/Vuex%E2%80%94%E2%80%94Vue%E5%8D%95%E9%A1%B5%E5%BA%94%E7%94%A8%E7%8A%B6%E6%80%81%E7%AE%A1%E7%90%86%E6%9E%B6%E6%9E%84/)
[Vuex框架原理与源码分析 -](https://tech.meituan.com/vuex-code-analysis.html)
[手把手教你怎么拆分 vuex@2.x - 前端 - 掘金](https://juejin.im/entry/5937c768570c35005b79a050)
[vuex-persistedstate - Google 搜索](https://www.google.com.hk/search?q=vuex-persistedstate&newwindow=1&c2coff=1&safe=strict&ei=ZdOjWe77Gcz2mAGamIfICA&start=20&sa=N&biw=1920&bih=955)
[robinvdvleuten/vuex-persistedstate: 💾 Persist Vuex state with localStorage.](https://github.com/robinvdvleuten/vuex-persistedstate)

[vuex/products.js at dev · vuejs/vuex](https://github.com/vuejs/vuex/blob/dev/examples/shopping-cart/store/modules/products.js)


## 登陆
[Vuejs 2 Authentication Tutorial](https://auth0.com/blog/vuejs2-authentication-tutorial/)
在一般的登录过程中，一种前端方案是：

1. 检查状态：进入页面时或者路由变化时检查是否有登录状态(保存在cookie或者本地存储的值)；
2. 如果有登录态则查询登录信息(uid，头像等...)并保存起来；如果没有则跳转到登录页；
3. 在登录页面（或者登录框），校检用户输入信息是否合法；
4. 校检通过后发送登录请求；校检不成功则反馈给用户；
5. 登录成功则从后端数据中取出session信息保存登录状态(可能需要跳转);登录不成功则提示用户不成功；
6. 用户做出注销操作时删除登录状态。


#### 滚动行为[](https://aotu.io/notes/2017/07/17/The-Exploration-and-Practice-of-Vue/index.html#%E6%BB%9A%E5%8A%A8%E8%A1%8C%E4%B8%BA)

对于 SPA 应用来说滚动行为是个挺头疼的问题，毕竟其本质只是一个页面，又是异步渲染的，所以难以保证各个视图的滚动行为能像多页面应用一样。为此进行了以下几步的探索。

* 结合 vuex 来存储滚动

在 view 的 beforeDestory 时，主动记录该视图的滚动值，在下次 mounted 时延时滚动到该位置。

> 这个方案需要为每个需要记录滚动的视图添加 state、mutation 和 action，并在视图添加额外的代码，实际操作繁琐，且跳外部链接后再返回时所记录的值也已经被销毁。

* 使用浏览器存储

为了解决跳外部链接后返回也能定位滚动位置，使用 localStorage 来记录滚动值，而且使用了 mixin，这样有需要操纵滚动行为的视图插入这个 mixin 就可以了，不需要在视图里加额外代码。

但是问题来了，我们并不能区分当次访问是第一次打开还是刚从外链返回，就导致了第一次访问也会被定位，就想到了 cookie，让 cookie 保持 30min。显然，这不是好的解决方案，再考虑到的是 sessionStorage，在当前会话中它能一直保持数据，跳外链返回后数据也还能保持着（此前以为跳外链后 sessionStorage 的数据也会被清除），新标签打开视为新会话，互不共用数据，这几点特性正好符合我们的要求。

另外要考虑的一个问题是，页面是异步渲染的，我们并不知道它的接口什么时候都请求完了，于是除了有默认的延时滚动外，还添加了主动触发滚动的特性，让开发者考虑什么时候页面才算加载完（通常是 watch 某个或多个异步请求的状态），然后主动去调用滚动方法。

最后要指出的是，滚动行为的解决方案也并不是完美的，比如，这个方案并不适用于有模块懒加载的页面。

最终 mixin 代码如下：
``` javascript
/**
 * 如需手动触发滚动：
 * manualTriggerLivescroll: true
 * this._livescroll()
 */
import Tools from '@/utils/tools'
const ss = window.sessionStorage
export default {
  data () {
    return {
      routeName: this.$route.name,
      liveScrollFlag: false,
      liveScrollFn: null,
      liveScrollTimer: null
    }
  },
  computed: {
    liveScrollTop () {
      return ss ?
        ss.getItem(`view-${this.routeName}`) :
        Tools.getCookie(`view-${this.routeName}`)
    }
  },
  methods: {
    _livescroll () {
      if (this.liveScrollFlag || !this.liveScrollTop) {
        return
      }
      this.liveScrollFlag = true
      // $nextTick 发挥不太稳定
      this.liveScrollTimer = window.setTimeout(() => {
        document.body.scrollTop = document.documentElement.scrollTop = this.liveScrollTop
      }, 500)
    }
  },
  mounted () {
    document.body.scrollTop = document.documentElement.scrollTop = 0
    !this.manualTriggerLivescroll && this._livescroll()
    this.liveScrollFn = () => {
      ss ?
        ss.setItem(`view-${this.routeName}`, this.getScrollTop()) :
        Tools.setCookie(`view-${this.routeName}`, this.getScrollTop(), 0.2083)
    }
    window.addEventListener('touchend', this.liveScrollFn, false)
  },
  beforeDestroy () {
    window.removeEventListener('touchend', this.liveScrollFn, false)
    this.liveScrollTimer && window.clearTimeout(this.liveScrollTimer)
  }
}
```
