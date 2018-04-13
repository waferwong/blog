[React 技术栈系列教程 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2016/09/react-technology-stack.html)

[JSX 简介 - React](https://doc.react-china.org/docs/introducing-jsx.html)
[ruanyf/react-demos: a collection of simple demos of React.js](https://github.com/ruanyf/react-demos)

[Web-Series/create-react-app.md at master · wxyyxc1992/Web-Series](https://github.com/wxyyxc1992/Web-Series/blob/master/React-And-Frontend-Engineering/%E5%88%9D%E7%AA%A5/create-react-app.md)
[React开发中常用的工具集锦 - 某熊的全栈之路 - SegmentFault 思否](https://segmentfault.com/a/1190000006086639)
[create-react-app/README.md at master · facebook/create-react-app](https://github.com/facebook/create-react-app/blob/master/packages/react-scripts/template/README.md#adding-a-css-preprocessor-sass-less-etc)

## React元素
元素事实上只是构成组件的一个部分
React 元素都是immutable 不可变的。当元素被创建之后，你是无法改变其内容或属性的。一个元素就好像是动画里的一帧，它代表应用界面在某一时间点的样子。

React DOM 首先会比较元素内容先后的不同，而在渲染过程中只会更新改变了的部分。

组件从概念上看就像是函数，它可以接收任意的输入值（称之为“props”），并返回一个需要在页面上展示的React元素。

组件的返回值只能有一个根元素。

所有的React组件必须像纯函数那样使用它们的props。

状态与属性十分相似，但是状态是私有的，完全受控于当前组件。

使用类就允许我们使用其它特性，例如局部状态、生命周期钩子
constructor(props) {
    super(props);
    this.state = {date: new Date()};
}
类组件应始终使用props调用基础构造函数。
构造函数是唯一能够初始化 this.state 的地方。

通过调用 setState() ，React 知道状态已经改变，并再次调用 render() 方法来确定屏幕上应当显示什么。
状态更新可能是异步的
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));
当你调用 setState() 时，React 将你提供的对象合并到当前状态。(浅合并)

父组件或子组件都不能知道某个组件是有状态还是无状态，并且它们不应该关心某组件是被定义为一个函数还是一个类。

这就是为什么状态通常被称为局部或封装。 除了拥有并设置它的组件外，其它组件不可访问。

组件可以选择将其状态作为属性传递给其子组件：

这通常被称为自顶向下或单向数据流。 任何状态始终由某些特定组件所有，并且从该状态导出的任何数据或 UI 只能影响树中下方的组件。
如果你想象一个组件树作为属性的瀑布，每个组件的状态就像一个额外的水源，它连接在一个任意点，但也流下来。

类的方法默认是不会绑定 this 的。


我推荐观看Preethi Kasireddy 在React2017大会上的一个演讲 https://www.youtube.com/embed/76FRrbY18Bs，主题是Redux vs. MobX，你可以从中知道他们各自的优缺点。
如果Redux或MobX对你的应用来说太重了，考虑一下容器组件https://medium.com/@learnreact/container-components-c0e67432e005模式。它可以通过使逻辑和表现分离来优化性能。它可以帮助查看API调用和其他逻辑所在的位置，可能包含你改进应用所需要的全部内容。

Dan Abramov有一系列学习视频叫做Redux入门https://egghead.io/courses/getting-started-with-redux。他们可以在Egghead.io上免费观看，是很好的学习资源

## Redux
view -> actionCreator -> action -> reducer -> newState -> container component

1. 不使用任何中间件
在view中发起异步请求，然后dispatch

问题：
1. 如果有多个类似的 action 触发场景，异步逻辑不能重用
2. 异步处理代码不能统一处理，最简单的例子就是节流

someAction.js
```js
function dispatchSomeAction(dispatch, payload) {
    // ..调用控制逻辑...
    dispatch({ type: 'SYNC_SOME_ACTION'})
    window.setTimeout(() => {
      dispatch({ type: 'ASYNC_SOME_ACTION' })
    }, 1000)
}
```

然后组件只需要调用：

```js
import {dispatchSomeAction} from 'someAction.js'

dispatchSomeAction(dispatch, payload);
```

基于这种方式上面的流程就改为了：

`view -> asyncActionDispatcher -> wait -> action -> reducer -> newState -> container component`

asyncActionDispatcher 和 actionCreator 是十分类似的, 所以简单而言就可以把它理解为 asyncActionCreator , 所以新的流程为：

`view -> asyncActionCreator -> wait -> action -> reducer -> newState -> container component`

但是上面的方法有一些缺点，同步调用和异步`调用的方式不相同`:
* 同步的情况: `store.dispatch(actionCreator(payload))`
* 异步的情况: `asyncActionCreator(store.dispatch, payload)`

通过 middleware 实现异步


A thunk is a function that wraps an expression to delay its evaluation.
简单来说一个 thunk 就是一个封装表达式的函数，封装的目的是延迟执行表达式



```js
// 1 + 2 立即被计算 = 3
let x = 1 + 2;

// 1 + 2 被封装在了 foo 函数内
// foo 可以被延迟执行
// foo 就是一个 thunk
let foo = () => 1 + 2;
```

redux-thunk 是一个通用的解决方案，其核心思想是让 action 可以变为一个 thunk ，这样的话:

1.  同步情况：dispatch(action)
2.  异步情况：dispatch(thunk)

> 拥有 dispatch 方法的组件为 redux 中的 container component

thunk 中间件的实现



```js
function createThunkMiddleware(extraArgument) {
  return ({ dispatch, getState }) => next => action => {
    if (typeof action === 'function') {
      return action(dispatch, getState, extraArgument);
    }

    return next(action);
  };
}

const thunk = createThunkMiddleware();
thunk.withExtraArgument = createThunkMiddleware;

export default thunk;
```

就这么简单，只有 14 行源码，但是这简短的实现却能完成复杂的异步处理，怎么做到的，我们来分析一下：

1.  判断如果 action 是 function 那么执行 action(dispatch, getState, ...)
    1.  action 也就是一个 thunk

    2.  执行 action 相当于执行了异步逻辑
        1.  action 中执行 dispatch

        2.  开始新的 redux 数据流，重新回到最开始的逻辑（thunk 可以嵌套的原因）

    3.  把执行的结果作为返回值直接返回

    4.  直接返回并没有调用其他中间件，也就意味着中间件的执行在这里停止了

    5.  可以对返回值做处理（后面会讲如果返回值是 Promise 的情况）

2.  如果不是函数直接调用其他中间件并返回

### thunk 的组合

根据 redux-thunk 的特性，可以做出很有意思的事情

1.  可以递归的 dispatch(thunk) => 实现 thunk 的组合；

2.  thunk 运行结果会作为 dispatch返回值 => 利用返回值为 Promise 可以实现多个 thunk 的编排;

thunk 组合例子：



```js
function thunkC() {
    return function(dispatch) {
        dispatch(thunkB())
    }
}
function thunkB() {
    return function (dispatch) {
        dispatch(thunkA())
    }
}
function thunkA() {
    return function (dispatch) {
        dispatch({type: 'THUNK_ACTION'})
    }
}
```

Promise 例子



```js
function ajaxCall() {
    return fetch(...);
}

function thunkC() {
    return function(dispatch) {
        dispatch(thunkB(...))
        .then(
            data => dispatch(thunkA(data)),
            err  => dispatch(thunkA(err))
        )
    }
}
function thunkB() {
    return function (dispatch) {
        return ajaxCall(...)
    }
}

function thunkA() {
    return function (dispatch) {
        dispatch({type: 'THUNK_ACTION'})
    }
}
```

源码吧



```js
import { isFSA } from 'flux-standard-action';

function isPromise(val) {
  return val && typeof val.then === 'function';
}

export default function promiseMiddleware({ dispatch }) {
  return next => action => {
    if (!isFSA(action)) {
      return isPromise(action)
        ? action.then(dispatch)
        : next(action);
    }

    return isPromise(action.payload)
      ? action.payload.then(
          result => dispatch({ ...action, payload: result }),
          error => {
            dispatch({ ...action, payload: error, error: true });
            return Promise.reject(error);
          }
        )
      : next(action);
  };
}
```

大概的逻辑就是：

1.  如果不是标准的 flux action，那么判断是否是 promise, 是执行 action.then(dispatch)，否执行 next(action)

2.  如果是标准的 flux action, 判断 payload 是否是 promise，是的话 payload.then 获取数据，然后把数据作为 payload 重新 dispatch({ ...action, payload: result}) , 否执行 next(action)

结合 redux-promise 可以利用 es7 的 async 和 await 语法，简化异步的 promiseActionCreator 的设计， eg:



```js
export default async (payload) => {
  const result = await somePromise;
  return {
    type: "PROMISE_ACTION",
    payload: result.someValue;
  }
}
```

如果对 es7 async 语法不是很熟悉可以看下面两个例子：

1.  async 关键字可以总是返回一个 Promise 的 resolve 结果或者 reject 结果



```js
async function foo() {
    if(true)
        return 'Success!';
    else
        throw 'Failure!';
}

// 等价于

function foo() {
    if(true)
        return Promise.resolve('Success!');
    else
        return Promise.reject('Failure!');
}
```

1.  在 async 关键字中可以使用 await 关键字，其目的是 await 一个 promise， 等待 promise resolve 和 reject

eg：



```js
async function foo(aPromise) {
    const a = await new Promise(function(resolve, reject) {
            // This is only an example to create asynchronism
            window.setTimeout(
                function() {
                    resolve({a: 12});
                }, 1000);
        })
    console.log(a.a)
    return  a.a
}

// in console
> foo()
> Promise {_c: Array[0], _a: undefined, _s: 0, _d: false, _v: undefined…}
> 12
```

可以看到在控制台中，先返回了一个 promise，然后输出了 12

async 关键字可以极大的简化异步流程的设计，避免 callback 和 thennable 的调用，看起来和同步代码一致。

## Action
Action 是把数据从应用（译者注：这里之所以不叫 view 是因为这些数据有可能是服务器响应，用户输入或其它非 view 的数据 ）传到 store 的有效载荷。它是 store 数据的唯一来源。一般来说你会通过 store.dispatch() 将 action 传到 store。

1.  用户的使用方式复杂
2.  不同身份的用户有不同的使用方式（比如普通用户和管理员）
3.  多个用户之间可以协作
4.  与服务器大量交互，或者使用了WebSocket
5.  View要从多个来源获取数据

1.  某个组件的状态，需要共享
2.  某个状态需要在任何地方都可以拿到
3.  一个组件需要改变全局状态
4.  一个组件需要改变另一个组件的状态

发生上面情况时，如果不使用 Redux 或者其他状态管理工具，不按照一定规律处理状态的读写，代码很快就会变成一团乱麻。你需要一种机制，可以在同一个地方查询状态、改变状态、传播状态的变化。

（1）Web 应用是一个状态机，视图与状态是一一对应的。

（2）所有的状态，保存在一个对象里面。

实际应用中，Reducer 函数不用像上面这样手动调用，`store.dispatch`方法会触发 Reducer 的自动执行。为此，Store 需要知道 Reducer 函数，做法就是在生成 Store 的时候，将 Reducer 传入`createStore`方法。

```
import { createStore } from 'redux';
const store = createStore(reducer);
```

### 异步
Redux本身只能处理同步的Action，但可以通过中间件来拦截处理其它类型的action，比如函数(Thunk)，再用回调触发普通Action，从而实现异步处理，在这点上所有Redux的异步方案都是类似的。

#### 乐观更新 optimistic update
多数异步场景都是`悲观更新`(求更好的翻译)的，即等到请求成功才渲染数据。而与之相对的`乐观更新`，则是**不等待请求成功，在发送请求的同时立即渲染数据**。

最常见的例子就是微信等聊天工具，发送消息时消息**立即**进入了对话窗，如果发送失败的话，在消息旁边再作补充提示即可。这种交互"乐观"地相信请求会成功，因此称作`乐观更新`。

由于`乐观更新`发生在用户操作时，要处理它，意味着**必须有action表示用户的初始动作**

在上面redux-thunk的例子中，我们看到了`GET_DATA`, `GET_DATA_SUCCESS`、`GET_DATA_FAILED`三个action，分别表示`初始动作`、`异步成功`和`异步失败`，其中第一个action使得redux-thunk具备乐观更新的能力。

而在redux-promise中，最初触发的action被中间件拦截然后过滤掉了。原因很简单，redux认可的[action](http://redux.js.org/docs/basics/Actions.html)对象是 _plain JavaScript objects_，即简单对象，而在redux-promise中，初始action的payload是个Promise。

另一方面，使用`status`而不是`type`来区分两个异步action也非常值得商榷，按照redux对action的定义以及社区的普遍实践，个人还是倾向于使用不同的type，用同一type下的不同status区分action额外增加了一套隐形的`约定`，甚至不符合该redux-promise作者自己所提倡的`FSA`，体现在代码上则是在switch-case内再增加一层判断。

Just Component React Router V4 遵循了 React 的理念：万物皆组件。
声明式（Declarative）
可组合 （Composability）

在 React Router 4 中，你可以将各种组件及标签放进 <Router>组件中，他的角色也更像是 Redux 中的 <Provider>。不同的是<Provider>是用来保持与 store 的更新，而<Router>是用来保持与 location 的同步。

<Route onEnter={checkAuth} path='dashboard' component={Dashboard} />
这段代码是指在渲染 dashboard 组件的时候需要经过一层鉴权。这听起来像是在 Dashboard 的 componentDidMount 生命周期里去做一些事情？的确就是这样。

关于路由重定向: 使用Redirect..from..to的格式,注意位置需要在定义to路由的后面,比如to="/home",重定向就需要写在Route path="/home" 后面
关于404路由匹配,默认写在路由末尾,前面的路由都不匹配时,自动匹配404
``` javascript
import {withRouter} from 'react-router-dom';

goBack(){
    this.props.history.goBack();
}  
goDetail(){
    this.props.history.push('/detail');
}  
goDetailWithParam(item){
    this.props.history.push({pathname : '/cart',state:{item}});
}

<span className="ico" onClick={this.goBack.bind(this)}>
    <i className="iconfont">&#xe501;</i>
</span>
//这里的item来自for循环的每一项
<li onClick={this.goDetailWithParam.bind(this,item)} key={encodeURI(item.imgUrl)}>

export default withRouter(Header);
```
引入withRouter之后,就可以使用编程式导航进行点击跳转, 需要注意的是export default的暴露如上面所写,如果结合redux使用,则暴露方式为: withRouter(connect(...)(MyComponent))
调用history的goBack方法会返回上一历史记录
调用history的push方法会跳转到目标页,如上面goDetail方法
跳转传参: push()可以接收一个对象参数,跳转之后,通过this.props.location.state接收


``` JavaScript
render() {
    if(this.props.logined) {
      return (
        <Redirect to="/user"/>
      )
    }
    return (
      <div>
          <input type="text" value={this.state.value} onChange={this.handleChange} />
          <a onClick={() => { this.toLogin(this.state.value) }}>登录</a>
      </div>
    )
  }
```
