---
title: react简介
tags:
  - react
categories:
  - react
abbrlink: de3ba3c
date: 2017-09-18 11:04:58
---

# react-study1

标签（空格分隔）： react

---

## 一、react简介

* 专注视图层
    可以与其他框架搭配，构建大型应用.
* 虚拟dom，性能(dom操作性能消耗最大)。
    真实页面对应一个 DOM 树。
    * 传统：传统页面的开发模式中，每次需要更新页面时，都要手动操作 DOM 来进行更新
    * `每次数据更新后`，重新计算 Virtual DOM，并和上一次生成的 Virtual DOM 做对比，对发生变化的部分做批量更新。React 也提供了直观的 shouldComponentUpdate 生命周期回调，来减少数
据变化后不必要的 Virtual DOM 对比过程，以保证性能

* [函数式编程(react的精髓)](#fun)
* [jsx语法](#jsx)

<span id = "fun"></span>
## 二、函数式编程

* 对比
    * 命令式编程：命令式编程解决的是做什么的问题，执行命令,命令式编程关心解决问题的步骤
    * 函数式编程：是一种"编程范式"（programming paradigm），主要思想是把运算过程尽量`写成一系列嵌套的函数调用`,函数式编程关心数据的映射
* 特点
    * 函数是"第一等公民"，指的是函数与其他数据类型一样，处于平等地位，可以赋值给其他变量，也可以作为参数，传入另一个函数，或者作为别的函数的返回值
    * 只用"表达式"，不用"语句"
"表达式"（expression）是一个单纯的运算过程，`总是有返回值`；"语句"（statement）是`执行某种操作，没有返回值`。函数式编程要求，只使用表达式，不使用语句。也就是说，每一步都是单纯的运算，而且都有返回值。
    * 没有"副作用"
函数式编程强调没有"副作用"，意味着函数要保持独立，所有功能就是返回一个新的值，没有其他行为，尤其是不得修改外部变量的值。
    * 不修改状态
函数式编程只是返回新的值，不修改系统变量。
    * 引用透明
引用透明（Referential transparency），指的是函数的运行不依赖于外部变量或"状态"，只依赖于输入的参数，任何时候只要参数相同，引用函数所得到的返回值总是相同的。
* 意义
    * 代码简洁，开发快速
函数式编程大量使用函数，减少了代码的重复，因此程序比较短，开发速度较快。
    * 接近自然语言，易于理解（demo）
    * 更方便的代码管理
函数式编程不依赖、也不会改变外界的状态，只要给定输入参数，返回的结果必定相同。因此，每一个函数都可以被看做独立单元，很有利于进行单元测试（unit testing）和除错（debugging），以及模块化组合。
    * 易于"并发编程"

<span id = "jsx"></span>
<!-- more -->
## 三、 jsx语法

### 1. jsx的由来

* 描述
虚拟元素可以理解为真实元素的对应，它的构建与更新都是在内存中完成的，并不会真正渲染到 DOM 中去。在 React中创建的虚拟元素可以分为两类，**DOM 元素（DOM element）**
与**组件元素（component element）**，分别对应着原生 DOM 元素与自定义元素，而 JSX 与创建元素的过程有着莫大的关联
* dom元素的，react的创建元素类似

```
<button class="btn btn-blue">
  <em>Confirm</em>
</button>

{
 type: 'button',
 props: {
   className: 'btn btn-blue',
   children: [{
  type: 'em',
  props: {
 children: 'Confirm'
  }
   }]
  }
}
ps: 在 React 中，到处都是可以复用的元素，这些元素并不是真实的实例，它只是让 React 告诉
开发者想要在屏幕上显示什么。我们无法通过方法去调用这些元素，它们只是不可变的描述对象
```

* 组件元素，react的创建元素类似

```
const Button = ({ color, text }) => {
 return {
 type: 'button',
   props: {
  className: `btn btn-${color}`,
  children: {
 type: 'em',
 props: {
   children: text,
 },
  },
   },
  };
}
//创建组件元素的json格式
{
 type: Button,
 props: {
   color: 'blue',
   children: 'Confirm'
  }
}
```
### 2. jsx的基本语法

* 基本语法
    定义标签时，只允许被一个标签包裹;
    标签一定要闭合
* 元素类型
    dom元素： 标签首字母为`小写字母`
    组件元素：标签首字母对应`大写首字母`
* 注释
    {/* 节点注释 */}
    条件注释：

    ```
    <!--[if IE]>
    <p>Work in IE browser</p>
    <![endif]-->
    {
        (!!window.ActiveXObject || 'ActiveXObject' in window) ?
        <p>Work in IE browser</p> : ''
    }
    ```
* 元素属性
    class 属性改为 className；
    for 属性改为 htmlFor；
    在写自定义属性的时候，都由标准写法改为小驼峰写法
* Boolean 属性
    省略 Boolean 属性值会导致 JSX 认为 bool 值设为了 true。要传 false 时，必须使用属性表达式

    ```
    <Checkbox checked={true} />
    <Checkbox checked />
    <Checkbox checked={false} />
    ```
* 展开属性
    可以使用 ES6 rest/spread 特性来提高效率

    ```
    const data = { name: 'foo', value: 'bar' };
    const component = <Component name={data.name} value={data.value} />;
可以写成：
const data = { name: 'foo', value: 'bar' };
const component = <Component {...data} />;
    ```
### 3. JavaScript 属性表达式

```
const person = <Person name={window.isLoggedIn ? window.name : ''} />;
```
### 4.html转义

React 会将所有要显示到 DOM 的字符串转义，防止 XSS。

* 直接使用 UTF-8 字符
* 使用对应字符的 Unicode 编码查询编码；
* 使用数组组装 <div>{['cc ', <span>&copy;</span>, ' 2015']}</div>；
* 直接插入原始的 HTML
* React 提供了 dangerouslySetInnerHTML 属性。它的作用就是避免 React 转义字符，在确定必要的情况下可以使用它：

```
<div dangerouslySetInnerHTML={{__html: 'cc &copy; 2015'}} />
```
## 四、React组件

### 1. 狭义上的组件，UI组件。

**说明**：组件主要围绕在交互动作上的抽象，针对这些交互动作，利用 `JavaScript 操作 DOM 结构或 style 样式`来控制。一般会有 3 个部分组件：`结构、样式和交互行为`

* [其他知识点Class](http://es6.ruanyifeng.com/#docs/class)
* [demo实例](https://github.com/xiaowangmm2/react-demo/tree/master/react-component-demo)
* 规范标准组件的信息
    * **基本的封装性**。尽管说JavaScript没有真正面向对象的方法，但我们还是可以通过实例化的方法来制造对象。
    * **简单的生命周期呈现**。最明显的两个方法 constructor 和 destroy，代表了组件的挂载和卸载过程。但除此之外，其他过程（如更新时的生命周期）并没有体现。
    * **明确的数据流动**。这里的数据指的是调用组件的参数。一旦确定参数的值，就会解析传进来的参数，根据参数的不同作出不同的响应，从而得到渲染结果。
* mvc架构的演变，模板引擎的加入，可以解决view层
* 弊端：通过改变 class 控制 style 来显示或隐藏。这样的逻辑一旦复杂，就存在大量的 DOM 操作，
开发及维护成本相当高。

### 2. 广义上的组件，带有业务含义和数据的 UI 组件组合

这类组件不仅有交互动作，更重要的是有`数据与界面之间的交互`。

* Web Components
* react组件： React组件基本上由3个部分组成——属性（props）、状态（state）以及生命周期方法
**说明**：React 组件可以接收参数，也可能有自身状态。一旦接收到的参数或自身状态有所改变，React组件就会执行相应的生命周期方法，最后渲染。整个过程完全符合传统组件所定义的组件职责。
    ![组件](http://chuantu.biz/t6/46/1505202253x1944864576.png)
* 对比
    * React 自定义元素是库自己构建的，与 Web Components 规范并不通用；
    * React 渲染过程包含了模板的概念，即 1.2 节所讲的 JSX；
    * React 组件的实现均在方法与类中，因此可以做到相互隔离，但不包括样式；
    * React 引用方式遵循 ES6 module 标准。

### 3. react组件创建

* React.createClass
```
const Button = React.createClass({
 getDefaultProps() {
   return {
  color: 'blue',
  text: 'Confirm',
   };
  },

 render() {
   const { color, text } = this.props;

   return (
  <button className={`btn btn-${color}`}>
    <em>{text}</em>
  </button>
   );
  }
});
```
* ES6 classes

```
import React, { Component } from 'react';

class Button extends Component {
 constructor(props) {
   super(props);
  }

 static defaultProps = {
   color: 'blue',
  text: 'Confirm',
  };

 render() {
   const { color, text } = this.props;

   return (
  <button className={`btn btn-${color}`}>
    <em>{text}</em>
  </button>
   );
  }
}
```

* 无状态函数(无状态组件)
它不存在 state，也没有生命周期方法,无状态组件。不像上述两种方法在调用时会创建新实例，它`创建时始终保持了一个实例`，避免了不必要的检查和内存分配，做到了内部优化。

```
function Button({ color = 'blue', text = 'Confirm' }) {
 return (
   <button className={`btn btn-${color}`}>
  <em>{text}</em>
   </button>
  );
}
```

* es6与es5差异
![差异](http://chuantu.biz/t6/47/1505266423x2890149518.png)

## 五. react数据流

* 概念
> 在 React 中，数据是自顶向下单向流动的，即从父组件到子组件。这条原则让组件之间的关系变得简单且可预测。
>
state 与 props 是 React 组件中最重要的概念。如果顶层组件初始化 props，那么 React会向下遍历整棵组件树，重新尝试渲染所有相关的子组件。而 state只关心每个组件自己内部的状态，这些状态只能在组件内改变。把组件看成一个函数，那么它接受了props作为参数，内部由 state 作为函数的内部参数，返回一个 Virtual DOM 的实现。
* state
* props


## 六. react生命周期

* [当组件在挂载或卸载时](#render)
* [当组件接收新的数据时，即组件更新时](#update)

![生命周期](http://chuantu.biz/t6/47/1505265743x2890174297.png)

<span id="render"></span>

### 组件挂载、卸载

```
import React, { Component, PropTypes } from 'react';

class App extends Component {
 static propTypes = {
  // 挂载过程 执行一次
  };

 static defaultProps = {
  // 挂载过程 执行一次
  };

 constructor(props) {
 // 挂载过程 执行一次
   super(props);

   this.state = {
  // ...
   };
  }

 componentWillMount() {
 // if setState 挂载过程 render一次
  }
 componentDidMount() {
 // if setState 挂载过程 render两次
  }
 componentWillUnmount() {
  // 卸载过程执行
  // 我们常常会执行一些清理方法，如事件回收或是清除定时器。
  }
 render() {
   return <div>This is a demo.</div>;
  }

}
```
<span id="update"></span>

### 数据更新过程

说明：更新过程指的是父组件向下传递 props或组件自身执行setState 方法时发生的一系列更新动作。

```
import React, { Component, PropTypes } from 'react';

class App extends Component {
 componentWillReceiveProps(nextProps) {
 // this.setState({})
  }

 shouldComponentUpdate(nextProps, nextState) {
 // return true;
  }

 componentWillUpdate(nextProps, nextState) {
 // 不能执行 setState
  }

 componentDidUpdate(prevProps, prevState) {
 // ...
  }

 render() {
   return <div>This is a demo.</div>;
  }
}
```
1. state更新

如果组件自身的 state更新了，那么会依次执行shouldComponentUpdate、componentWillUpdate 、render 和 componentDidUpdate。

2. shouldComponentUpdate
shouldComponentUpdate 是一个特别的方法，它接收需要更新的 props 和 state，让开发者增加必要的条件判断，让其在需要时更新，不需要时不更新。因此，当方法返回false的时候，组件不再向下执行生命周期方法。

## 七. React 与 DOM

### ReactDOM

1. findDOMNode获取dom

```
componentDidUpdate
componentDidMount() {
 // this 为当前组件的实例
 const dom = ReactDOM.findDOMNode(this);
 }
```

2. refs,组件被调用时会新建一个该组件的实例，而refs就会指向这个实例。如果是无状态组件，render会返回null。无状态组件挂载时只是方法调用，没有新建实例.
refs 同样支持字符串。对于 DOM 操作，不仅可以使用 findDOMNode 获得该组件 DOM，还可以使用 refs 获得组件内部的 DOM。

```
componentDidMount() {
// myComp 是 Comp 的一个实例，因此需要用 findDOMNode 转换为相应的 DOM
 const myComp = this.refs.myComp;
 const dom = findDOMNode(myComp);
 }
```

## 八、相关demo

[地址](https://github.com/xiaowangmm2/react-demo/tree/master/react-component-demo)

## 相关链接：
* [react官网](https://facebook.github.io/react/)
* [阮一峰函数式编程](http://www.ruanyifeng.com/blog/2017/02/fp-tutorial.html)
* [fed函数式编程](http://taobaofed.org/blog/2017/03/16/javascript-functional-programing/)
* [柯里化](https://gist.github.com/jcouyang/b56a830cd55bd230049f)
* [webcomponents阮一峰](http://javascript.ruanyifeng.com/htmlapi/webcomponents.html)
* [webcomponents](http://sentsin.com/web/1089.html)




