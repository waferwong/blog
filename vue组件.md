# 组件化
[Vue.js 组件编码规范](https://pablohpsilva.github.io/vuejs-component-style-guide/#/chinese)
[饿了么基于Vue2.0的通用组件开发之路（分享会记录） - WoodK - 博客园](http://www.cnblogs.com/woodk/p/6048890.html)
[vuejs/vue-class-component: ES / TypeScript decorator for class-style Vue components.](https://github.com/vuejs/vue-class-component)
[vue methods decorator - Google 搜索](https://www.google.com.hk/search?newwindow=1&c2coff=1&safe=strict&biw=1920&bih=955&q=vue+methods+decorator&oq=vue+methods+decorator&gs_l=psy-ab.3...14839.20806.0.21214.9.9.0.0.0.0.1057.2235.2-2j2j7-1.5.0....0...1.1j4.64.psy-ab..4.0.0.H6TMMB73t14)

[性能优化之组件懒加载: Vue Lazy Component 介绍](https://zhuanlan.zhihu.com/p/29433875)
[xunleif2e/vue-lazy-component: 🐌 Vue.js 2.x 组件级懒加载方案-Vue.js 2.x component level lazy loading component](https://github.com/xunleif2e/vue-lazy-component)

[Vue 项目中使用 webpack 将多个组件合并打包并实现按需加载 - 知乎专栏](https://zhuanlan.zhihu.com/p/25335884)
[JDC | 京东设计中心 » 漫谈Vue组件库开发](http://jdc.jd.com/archives/212167?hmsr=toutiao.io&utm_medium=toutiao.io&utm_source=toutiao.io)
[Vue组件库的那些事儿，你都知道吗？](https://mp.weixin.qq.com/s/oS94Z6jua5vBoXGCmNLhnw)

# 组件库

[从零开始搭建Vue组件库 VV-UI](https://zhuanlan.zhihu.com/p/30948290)
[Vant - 高效的 Vue 组件库，再造一个有赞移动商城也不在话下-前端外刊评论](https://qianduan.group/posts/5a274ff5485c1a4c84948ccb)

[App](http://aurora.mljr.com/app.html)
[sunshineJi/amaze-vue: 一只基于amazeui样式封装的vue组件库。万水千山总是情，点个star再走行不行~~~](https://github.com/sunshineJi/amaze-vue)
[amaze-vue使用文档--别让vue禁锢了你的amaze ui](https://sunshineji.github.io/amaze-vue-docs/#/)

> 组件库创建

特别在 mobile 端，对精制化项目来说，自己的维护一套组件库是非常有意义的，无论是对整体色彩的定制还是对功能的定制，快节奏的变动和需求迭代改动，第三方的往往是不够。

不适用原因：

1.  跟设计给的样式和色彩不匹配
2.  产品对 C 端用户的体验玩法更为反常
3.  大方向单个组件内小规模改动
4.  组件库的暴露的接口不符合业务需求

对于面向 C 端的产品必然是做出自己的特色，所以自己掌握一套组件库的应用，这个是必然的抉择。

> 如何方便快速稳健的搭建一套基本的组件库。

首先组件库必然的两点：

* 样式组件
* 功能组件

一个基本的组件库样式组件可以让开发布局flex布局grid布局对做项目来说会显的更加轻松，对于基本的功能组件不必要忙着把所有市面上所见的全部造出来，组件库和业务要并行，设计图拿到手之后，看设计图用到的那些通用型组件，把先用到的造出来，不需要的留一边，等项目结束后再造。

> 借鉴组件库，不要往死想

大量第三方组件库都是一个团队，经过大量的测试和用户反馈，兼容性测试进行发布的，无论组件的设计模式和接口暴露的方式，技术都是比较领先的，可以先向大厂商中的组件库中吸收一些组件库的写法和思想，再考虑把第三方的组件好的写法拿过来。
还有很重要的一点是，第三方的组件库对于单个组件都尽量做到很全面，暴露了很多接口，一开始只需要根据自己的项目要求暴露部分接口。

> 不要一味着造组件库

像一些比较不容易理解的组件或者自己还没有能力去吸收和改造 的情况下，我建议还是暂时使用第三方的。
比如说一些 swiper 这种比较复杂的组件，也是项目通用型组件，在快速完成项目和人手不够的情况 下，建议暂时使用第三方的。
不要浪费时间去研究组件如何写法，组件库造的再完美，项目延期了也不是一个完美的结局，可以把这些问题放到版本迭代，项目优化等方面。

## 组件
[Vue 子组件的异步加载及其生命周期控制](https://mp.weixin.qq.com/s/Alv8VTAMiLM5rZGYJYhi6Q)

### modal
[如何使用vue.js构造modal(弹窗)组件? - 知乎](https://www.zhihu.com/question/35820643)
[Vue组件实现tips的总结-蚊子-前端博客](https://www.xiabingbao.com/vue/2017/09/14/vue-component-tips.html)



### loading

vue 动态组件
v-bind
分别监听

## slot

### scope slot-scope
slot-scope是vue2.5+的，在2.5之前的版本应该是scope
作用域插槽的关键之处就在于，父组件能接收来自子组件的slot传递过来的参数
scope其实就是<slot>标签的属性集合，也就是一个对象
[Vue.js作用域插槽的理解和模板“渲染”步骤 - 简书](https://www.jianshu.com/p/a0a83029a217)
[如何理解Vue的作用域插槽 - 个人文章 - SegmentFault](https://segmentfault.com/a/1190000010747756)


## props
如果prop本身是一个对象或者数组的话，由于javascript对象是引用方式，无论是什么绑定方式都会是双向绑定！！

1. 不要在组件内试图修改props传进来的父组件数据，数据只应该由该数据的源头组件来负责app内的CRUD；
2. 数据永久性功能（就是和后台数据库交互保存）最好是由需要处理数据的子组件来和数据库交互，但是通过$emit一个事件通知该数据的源头组件来更新web app的数据;(在子组件tag引用处以@resource-deleted来引用父组件的事件函数) 这种模式带来的问题是数据来源和数据消费者有事件交互的强烈耦合。

还有一种小方案是将数据永久性功能以及web app内部的数据一致两个功能合为一处，即：子组件需要修改源数据时，$emit消息给父亲，由owner来同时完成数据永久性保存和内部app数据一致

3. 对于大型web app可以使用vuex来实现解耦：父子之间通过vuex store state tree来保持联系，任何时候需要获取数据则getter,如果需要修改数据则setter,数据修改后的reactive则由vuejs处理，这种方式最大限度地实现了解耦

4. 但是有时也需要一些平衡：难道每一片小数据都得通过$emit事件给数据源头来做修改吗？由于如果传入的数据是Object类型或者array类型的，则本身由于是reference传参的，也就是说子组件prop传入供子组件读/写的object/array和“源头object/array”实际上是一个对象，因此只要我们不直接简单粗暴以


``` javascript
this.objFromParent = newObjectCreatedByChild  //这样会导致vuejs报错 Avoid mutating a prop directly ...

this.objFromParent.propertyChangedByChild = newObjectCreatedByChild.propertyChangedByChild  //这样数据就很轻松保持了一致性，而不用$emit消息到数据源来维护数据了！！！
```

5. 第4点和vuex的机制比较类似。你可以在需要共享给儿子组件的数据（起源于hosted by本组件）存放在一个localStore对象的属性中，将localStore对象作为属性值传给儿子组件，比如:pstore="localStore"，在儿子组件中，则可以直接操作pstore.parentData = somedatahandledbyson ,曲线救国，绕过了vuejs2.0不允许对属性赋值操作的限制。

6. 如果是需要共享给后代子孙的数据，则可以引入一种thisrootstore机制，所有这类数据作为thisrootstore的属性对象存在，后代以this.rootstore.xxx来引用它。

5和6的好处是剔除大部分不需要$emit事件来sync数据的冗余代码，更加易于实现组件功能的抽象和重用

7. 也可以考虑利用slot机制的特性： slot本身所在html js scope属于父组件，这样就可以以下面的形式来解决这个数据同步问题：

``` html
<!-- within parent template removeThisSon() resonsible for remove data which hosted by parent -->
<son v-for="son in sons">
  <div @click="removeThisSon(son)"> some operation affected parent data</div>
</son>
```

心法：对整个属性对象替换(赋值)，新增，或者删除操作必须由数据源来操作，但是对传入的属性对象的某些property修正，则可以在子组件内部直接操作，数据就同步反映到父组件中

心法：数据优先，你首先抽象驱动你的app的state，所有代码就围绕着这些个state的变迁，而让vuejs本身来执行构建和更新DOM的工作。

The whole idea is "data first". you define what the state of your application should look like, and let Vue build and update the DOM accordingly

通过prop向子组件传入父组件的函数作为callback，并且访问子组件的数据

父组件通过 props 给子组件传值，或者，父组件还可以通过子组件实例的方法来给子组件传参（如代码中的 open 方法）。

子组件可以通过 emit 触发事件来向上通信，或者，通过直接调用作为 prop 传进来的父组件方法也可以实现向上通信（如代码中的 changeNickname）。

[vue 状态管理的一点思考](https://zhuanlan.zhihu.com/p/29237682)
[vue-state-management-alternative/README-CN.md at master · kenberkeley/vue-state-management-alternative](https://github.com/kenberkeley/vue-state-management-alternative/blob/master/README-CN.md)


```html
<template>
<div v-show="isShow" class="test">
  <!-- slot 的运用 -->
  <slot></slot>
  <slot name="slot2"></slot>
  <template v-if="testProp"></template>
  <template v-else></template>
  <!-- 对于嵌套较深的组件，可以用 function-type-prop 来代替 emit 触发链 -->
  <div @click="changeNickname && changeNickname('小镇')"></div>
  <div @click="close" class="test_btn">{{btnText}}</div>
</div>
</template>
<script>
import Utils from '@/utils'
export default {
  props: {
    testProp: {
      type: [Number, String],
      required: true
    },
    changeNickname: Function
  },
  data () {
    return {
      isShow: false,
      btnText: '',
      closeFn: null
    }
  },
  methods: {
    close () {
      this.isShow = false
      this.closeFn && this.closeFn()
    },
    // 除了 poops 传参，函数传参也是一种方式
    open (btnText = '', closeFn) {
      this.isShow = true
      this.btnText = btnText
      this.closeFn = closeFn
    }
  }
}
</script>
<style lang="sass">
@import "common";
.test {
  background-image: url(~@img/test/bg.png);
}
</style>
```

slot 对于可复用组件来说意义重大，因为我们在实际的应用中，组件往往大同小异，看起来可以做成组件的模块总会或多或少差异的地方，通过参数来控制这些差异也是可行的，但非常不利于组件的扩展，所以这些地方就交给 slot 来应对，slot 的意思是插槽，意指我们能在父组件中需要的时候，给组件填充自定义内容。

父组件通过 props 给子组件传值，或者，父组件还可以通过子组件实例的方法来给子组件传参（如代码中的 open 方法）。

子组件可以通过 emit 触发事件来向上通信，或者，通过直接调用作为 prop 传进来的父组件方法也可以实现向上通信（如代码中的 changeNickname）。

### $props
[Vue.js 实用技巧（二）](https://zhuanlan.zhihu.com/p/25623356)

### $attrs
#### $attr 与 interitAttrs 之间的关系

> interitAttrs :

默认情况下父作用域的不被认作 props 的特性绑定 (attribute bindings) 将会“回退”且作为普通的 HTML 特性应用在子组件的根元素上。当撰写包裹一个目标元素或另一个组件的组件时，这可能不会总是符合预期行为。

通过设置 inheritAttrs 到 false，这些默认行为将会被去掉。而通过 (同样是 2.4 新增的) 实例属性 $attrs 可以让这些特性生效，且可以通过 v-bind 显性的绑定到非根元素上。

> 注意：这个选项不影响 class 和 style 绑定。


```javascript
// 子组件
<template>
   <div>
      {{first}}
   </div>
</template>
<script>
export default {
   name: 'demo',
   props: ['first']
}
</script>

// 父组件
<template>
  <div class="hello">
     <demo :first="firstMsg" :second="secondMessage"></demo>
  </div>
</template>

<script>
  import Demo from './Demo.vue'
  export default {
    name: 'hello',
    components: {
      Demo
    },
    data () {
      return {
        firstMsg: 'first props',
        secondMessage: 'second props'
      }
    },
  }
</script>
```

父组件在子组件中进行传递 firstMsg 和 secondMsg 两个数据，在子组件中，应该有相对应的 Props 定义的接收点。

如果在 props 中定义了，你会发现无论是 firstMsg 和 secondMsg 都成了子组件的接收来的数据了，可以用来进行数据展示和行为操作。

虽然在父组件中在子组件模版上通过 props 定义了两个数据，但是子组件中的 Props 只接收了一个，只接收了 firstMsg，并没有接收 secondMsg，没有进行接收的此时就会成为子组件根无素的属性节点。

### **事件代理**

当我们用 v-for 渲染大量的同样的 DOM 结构时，但是每个上面都加一个点击事件，这个会导致性能问题，那我们可以通过 html5 的 data 的自定义属性做事件代理。

#### **父组件改动**

```javascript
<template>
  <div class="hello" @click="ff">
     <demo :first="firstMsg" :data-second="secondMsg"></demo>
     <demo :first="firstMsg" :data-second="secondMsg"></demo>
     <demo :first="firstMsg" :data-second="secondMsg"></demo>
     <demo :first="firstMsg" :data-second="secondMsg"></demo>
  </div>
</template>

<script>
  import Demo from './Demo.vue'
  export default {
    name: 'hello',
    components: {
      Demo
    },
    data () {
      return {
        firstMsg: 'first props',
        secondMsg: 'secondMsg'
      }
    },
    methods: {
      ff (e) {
        if(e.target.dataset.second == 'secondMsg') {
            console.log('通过事件委托拿到了自定义属性')
        }
      }
    }
  }
</script>
```

经过改动之后，在父组件中，把向子组件传递的参数名改成了 html 自定义的 data-second 属性，同样在子组件中不进行 Props 接收，就顺其自然的成为了子组件每一个根节点的自定义属性。

通过事件冒泡的原理，然而可以从 e.target.dataset.second 就能找对应的dom节点进行逻辑操作。

同样，在子组件模版上可以绑定多个自定义属性，在子组件包裹的外层进行一次监听，通过 data 自定义属性拿到循环出来组件的对应的数据，进行逻辑操作。

interitAttrs = false 发生了什么 ？

```javascript
<template>
   <div>
      {{first}}
   </div>
</template>
<script>
export default {
   name: 'demo',
   props: ['first'],
   inheritAttrs: false,
}
</script>
```

对子组件进行一个改动，我们加上 inheritAttrs: false，从字面上的翻译的意思，取消继承的属性，然而 props 里仍然没有接收 seconed，发现就算 Props 里没有接收 seconed，在子组件的根元素上并没有绑定任何属性。

> $attrs

包含了父作用域中不被认为 (且不预期为) props 的特性绑定 (class 和 style 除外)。当一个组件没有声明任何 props 时，这里会包含所有父作用域的绑定 (class 和 style 除外)，并且可以通过 v-bind=”$attrs“ 传入内部组件——在创建更高层次的组件时非常有用。

在前面的例子中，子组件 props 中并没有接受 seconed，设置选项 inheritAttrs: false，同样也不会作为根元素的属性节点，整个没有接收的数据都被 $attr实例属性给接收，里面包含着所有父组件传入而子组件并没有在 Props里显示接收。

为了验证事实，可以在子组件中加上：

<pre style="font-size: 0.85em;font-family: Consolas, Inconsolata, Courier, monospace;font-size: 1em;line-height: 1.2em;margin: 1.2em 0px;">
created () {
console.log(this.`$attrs`)
}
</pre>

打印出来则是一个对象：{second: “secondMsg”, third: “thirdMsg”}

#### **注意**

想要通 $attr 接收，但必须要保证设置选项 inheritAttrs: false，不然会默认变成根元素的属性节点。

开头说了，最有用的情况则是在深层次组件运用的时候。创建第三层组件，作为第二层组件的子组件，在子组件引入的孙子组件，在模版上把整个 $attr 当数作数据传递下去，中间则并不用通过任何方法去手动转换数据。

``` javascript

// 子组件

<template>
   <div>
      <next-demo v-bind="`$attrs`"></next-demo>
   </div>
</template>

// 孙子组件
<template>
  <div>
      {{second}}{{third}}
  </div>
</template>

<script>
  export default {
     props : [ 'second' , 'third']
  }
</script>
```

孙子组件在 props 接收子组件中通过 `$attr` 包裹传来的数据，同样是通过父组件传来的数据，只是在子组件用了 $attrs 进行了统一接收，再往下传递，最后通过孙子组件进行接收。

依次类推孙子组件仍然不想接收，再传入下级组件，我们仍然需要对孙子组件实力选项进行设置选项 inheritAttrs: false，否则仍然会成为孙子组件根元素的属性节点。

从而利用 $attrs 来接收 props 为接收的数据再次向下传递是一件很方便的事件，深层次接收数据我们理解了，那从深层次向层请求改变数据如何实现。意思就是让顶层数据和最底层数据进行一个双向绑定。

#### $listener
listeners 可以认为是监听者。

向下如何容易的传递数据已经了解了,面临的问题是如何向顶层的组件如何改变数据，父子组件可以通过 v-model，.sync,v-on 等一系列方法，深层及的组件可以通过 $listeners 去管理。

`$listeners` 和 `$attrs` 两者表面层都是一个意思，`$attrs` 是向下传递数据，`$listeners` 是向下传递方法，通过手动去调用 `$listeners` 对象里的方法，则原理就是 `$emit` 监听事件，`$listeners` 也可以看成一个包裹监听事件的一个对象。

#### **父组件**

``` javascript
<template>
  <div class="hello">
     {{firstMsg}}
     <demo v-on:changeData="changeData" v-on:another = 'another'></demo>
  </div>
</template>

<script>
  import Demo from './Demo.vue'
  export default {
    name: 'hello',
    components: {
      Demo
    },
    data () {
      return {
        firstMsg: '父组件',
      }
    },
    methods: {
      changeData (params) {
         this.firstMsg = params
      },
      another () {
        alert(2)
      }
    }
  }
</script>
```

在父组件中引入子组件，在子组件模板上面进行 changeData 和 another 两个事件监听，其它这两个监听事件并不打算被触发，而是直接被调用,再简单的理解则是向下传递两个函数。

``` javascript
<template>
   <div>
      <p @click="$emit('another')">子组件</p>  
      <next-demo  v-on='`$listeners`'></next-demo>
   </div>

</template>
<script>
import NextDemo from './nextDemo.vue'
export default {
   name: 'demo',
   components: {
       NextDemo
   },
   created () {
     console.log(this.`$listeners`)
   },
}
</script>
```

在子组件中，引入孙子组件 nextDemo，在子组件中，像 `$attrs` 一样,可以用 $listeners 去整体接收监听的事件，{changeData: ƒ, another: ƒ} 以一个对象去接收。

此时在父组件中在子组件模板上监听的两个事件不但可以被子组件实例属性 $listeners 去整体接收，并且同时可以在子组件进行触发。

同样的在孙子 nextDemo 组件中，继续向下传递,通过 v-on 把整个 `$listeners` 所接收的事件传递到孙子组件中，只是通过 `$listeners` 把其所有在父组件拿到监听事件一并通过 $listeners 一起传递到孙子组件里。

#### **孙子组件**
``` javascript
<template>
  <div class="hello">
      <p @click='`$listeners`.changeData("change")'>孙子组件</p>
  </div>
</template>

<script>
export default {
  name: 'demo',
  created () {
      console.log(this.`$listeners`)
  },
}
</script>
```


依然能拿到从子组中传递过来的 `$listeners` 所有的监听事件,此时并不是通过 emit 只是针对于父子组件的双向通信，`$listeners` 包了一个对象，分别是 changeData 和 another，通过 $listeners.changeData(‘change’) 等于直接触发了事件，执行监听后的回调函数,就是通过函数的传递，调用了父组件的函数。

## 动态组件
你虽然可以通过以下代码实现动态插入和删除vue组件的需求，但是这种方式的问题是：在vue devtool中并未看到数据链的关系，我们还是建议使用v-if来实现这种应用场景。

``` javascript
methods:{
    attachNewPermission: function(){
        var vm = this;
        var html = '<async-example roleid='+this.roleid+' ></async-example> ';
        var vmtemp = Vue.extend({
            template: html,
            replace: false,
            el: function(){
                return vm.$el.getElementsByClassName('asyncloadednode')[0];
            }
        });
        new vmtemp();
    }
}

    import ExecPlayer from './components/pages/exercise/exec-player.vue'; //这里exec-player只是export了一个component option object

    var execplayercomp = Vue.extend(ExecPlayer); //这里通过传入定义好的component option object作为Vue.extend的参数，以写程序的方式获得了component的构造函数
    var execplayer = new execplayercomp({
    // 'el': '#execplayer',  //调用new xxx的方式来创建组件，如果给了el配置项，则无需再调用$mount
    // 需要注意的是这种方式创建的组件在devtool中并不会显示为rootvm的子组件，但是实际上他们是有父子关系的！！！
    // 如果在html代码中直接以 <exec-player></exec-player>调用的方式来composite组件的话，则在devtool中能够正确显示父子关系~！
        created(){
            this.exercises = rootvm.exercises;
        }
    }).$mount(document.getElementById('execplayer'));

```
## keep alive
1. 登录重定向到Login再回来时（不会触发created的ajax）
2. 菜单导航

## .vue
[Vue.js 的实用技巧（一）](https://zhuanlan.zhihu.com/p/25589193)
vue-template-loader which transforms the template into a JavaScript render function.
`<template>` 内的内容字符串会被提取出来，用来编译进 Vue 组件内的 template 选项。
当 vue-loader 检测到 babel-loader 或者 buble-loader 在项目中存在的时候，将会用它们去处理所有 `*.vue` 文件的 `<script>` 部分，所以我们就可以在 Vue 组件中用 ES2015

### Src Imports

如果你喜欢把你的 `*.vue` 组件拆分成多个文件，那么你可以用 `src` 属性导入外部文件，代码如下：

``` html
<template src="./template.html"></template>
<style src="./style.css"></style>
<script src="./script.js"></script>
```

需要注意的是 `src` 导入要遵循和 CommonJS 的 `require()` 调用一样的路径解析规则，这就是说你需要用以 `./` 开头的相对路径，并且你可以直接从已安装的 NPM 包内导入资源，例如：

``` html
<!-- 从已安装的 "todomvc-app-css" NPM 包内导入文件 -->
<style src="todomvc-app-css/index.css">
```
