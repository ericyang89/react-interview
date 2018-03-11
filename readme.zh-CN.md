# React 面试题

下面是一些常见的 React 面试题.

- [React 怎么工作的 ?](#how-does-react-work)
- [What are the advantages of using React?](#what-are-the-advantages-of-using-react)
- [What is the difference between a Presentational component and a Container component?](#what-is-the-difference-between-a-presentational-component-and-a-container-component)
- [What are the differences between a class component and functional component?](#what-are-the-differences-between-a-class-component-and-functional-component)
- [What is the difference between state and props?](#what-is-the-difference-between-state-and-props)
- [Name the different lifecycle methods?](#name-the-different-lifecycle-methods)
- [Where in a React component should you make an AJAX request?](#where-in-a-react-component-should-you-make-an-ajax-request)
- [What are controlled components?](#what-are-controlled-components)
- [What are refs used for in React?](#what-are-refs-used-for-in-react)
- [What is a higher order component?](#what-is-a-higher-order-component)
- [What advantages are there in using arrow functions?](#what-advantages-are-there-in-using-arrow-functions)
- [Why is it advised to pass a callback function to setState as opposed to an object?](#why-is-it-advised-to-pass-a-callback-function-to-setState-as-opposed-to-an-object)
- [What is the alternative of binding `this` in the constructor?](#what-is-the-alternative-of-binding-this-in-the-constructor)
- [How would you prevent a component from rendering?](#how-would-you-prevent-a-component-from-rendering)
- [When rendering a list what is a key and what is its purpose?](#when-rendering-a-list-what-is-a-key-and-what-is-its-purpose)
- [What is the purpose of super(props)?](#what-is-the-purpose-of-super(props))
- [What is JSX?](#what-is-jsx)
- [What is equivalent of the following using React.createElement?](#what-is-equivalent-of-the-following-using-React.createElement)
- [What is `Children`?](#what-is-children)
- [What is state in react?](#what-is-state-in-react)
- [Why would you eject from create-react-app?](#why-would-you-eject-from-create-react-app)
- [What is redux?](#what-is-redux)
- [What is a store in redux?](#what-is-a-store-in-redux)
- [What is an action?](#what-is-an-action)
- [What is a reducer?](#what-is-a-reducer)
- [What is redux thunk used for?](#what-is-redux-thunk-used-for)
- [What is a pure function?](#what-is-a-pure-function)
- [What do you like about React?](#what-do-you-like-about-react)
- [What don't you like about React?](#what-dont-you-like-about-react)
- [Example projects](#example-projects)


#### React 怎么工作的 ?
React 创建了虚拟 DOM 。当组件中状态（state）改变时。第一步执行 “diff” 算法，找到虚拟 DOM 中改变的部分。第二步调和，也就是根据改变的虚拟 DOM 来更新 DOM。
React creates a virtual DOM. When state changes in a component it firstly runs a "diffing" algorithm, which identifies what has changed in the virtual DOM. The second step is reconciliation, where it updates the DOM with the results of diff.

#### 使用 React 有什么好处？
#### What are the advantages of using React?
- 很容易知道组件是怎么更新的，你只需要关注 render 函数。
- JSX 使得组件易读，也很容易看清楚组件是怎么陈列的，或者看清楚组件之间是怎么插入/组合（原文：plugged/combined ）的。
- 可以在服务端渲染 React。这样有利于 SEO 和性能。
- 很容易测试
- React 可以结合其他的框架一起使用 (Backbone.js, Angular.js) ， 因为他只是一个界面层。

#### 展示组件 (Presentational component) 和容器组件 (Container component) 的区别？
Presentational components are concerned with how things look. They generally receive data and callbacks exclusively via props. These components rarely have their own state, but when they do it generally concerns UI state, as opposed to data state.
展示组件专注于组件的展示。他们仅仅通过props接受数据和回调。他们很少有自己的状态 (state), 有也是UI的状态，而不是数据的状态。

容器组件专注于业务或逻辑。他们为展示组件或者其他的容器组件提供数据和行为。他们调用 Flux 的 actions，为展示组件提供回调函数。他们经常有状态，也经常作为数据的提供者。

Container components are more concerned with how things work. These components provide the data and behavior to presentational or other container components. They call Flux actions and provide these as callbacks to the presentational components. They are also often stateful as they serve as data sources. 

#### 类组件 (class component) 和函数组件 (functional component) 的区别？
- 类组件允许你使用额外的功能，例如内部状态和生命周期的钩子。也可以让你的组件可以使用全局存储 (store) 和拥有状态。

- 如果你的组件只是接受属性（props）展示到页面上， 他就是无状态的组件，可以使用一个纯函数。这样的组件可以叫做木偶组件或展示组件。

#### What is the difference between state and props?
#### 状态 (state) 和属性 (props) 的区别？
状态是一种有默认值的数据结构开始于组件挂载的时候。他会随着时间发生突变，通常是用户事件的结果。

属性(props,props是properties的缩写)数组件的配置。他们从上级获得，保持不变只到接受新的属性。组件不能改变他的属性，但是组件负责组合他们子组件的属性。属性不一定是纯数据，函数也可以作为属性传入。

#### 简述不同生命周期的方法。
- `componentWillMount`- 主要用于在根组件上进行 应用程序 (App) 的配置。
this is most commonly used for App configuration in your root component. 
- `componentDidMount` - 可以做一些 DOM 相关的设置，开始获取需要数据。如果你要设置事件监听，这也是个合适的地方。
here you want to do all the setup you couldn’t do without a DOM, and start getting all the data you need. Also if you want to set up eventListeners etc. this lifecycle hook is a good place to do that.
- `componentWillReceiveProps` - 这个生命周期主要用于指定属性改变的时候触发状态过渡。
this lifecyclye acts on particular prop changes to trigger state transitions.
- `shouldComponentUpdate` - 如果你担心浪费多余的渲染 (render) 次数， `shouldComponentUpdate` 是一个很好的提高性能的地方。他可以在组件接受新的属性的时候阻止渲染。你可以根据是否需要渲染，在shouldComponentUpdate中返回一个相应的布尔值。
is a great place to improve performance as it allows you to prevent a rerender if component receives new `prop`. shouldComponentUpdate should always return a boolean and based on what this is will determine if the component is rerendered or not.
- `componentWillUpdate` - 很少被使用。当组件也有`shouldComponentUpdate`的时候，可以用于替代 `componentWillReceiveProps` (但是无法获取上一次的属性)。
- `componentDidUpdate` - 也用于在属性和状态改变之后更新 DOM 。
- `componentWillUnmount` - 在这个方法内，你可以取消所有的网络请求，和移除组件相关的事件监听。

#### Where in a React component should you make an AJAX request?
#### 在 React 组件中，什么地方比较适合发送网络请求？
`componentDidMount` 就是在 React 组件内发送网络请求的地方。这个方法在组件挂载成功后会执行，并且只执行一次。一定要保证网络请求是在组件挂载成功之后发出的，这样才能保证网络请求返回的数据是在组件挂载之后的，也是这样才能保证组件会更新。

#### 什么是受控组件(controlled component)?

在 HTML 中，表单元素，例如：`<input>`, `<textarea>`和 `<select>`。他们自己维护他们自己的状态，并且根据用户的输入自动更新。当用户提交表单时，表单中上面提到的这些元素的值就会和表单一起被提交。在 React 中，完全不是这样的。包含表单的组件会跟踪元素的值。把这些值保持到组件的 state 中。当 `onChange`事件触发时，state 就会更新，然后组件的元素就会被重新渲染。这种表单中组件，在 React 中，被称为“受控组件”。


#### 在 React 中，refs 主要是干什么用的?

Refs 用于拿到 dom 节点的引用或者 React 实例的引用。例如：管理 text 标签的 focus；触发动画事件，或者集成第三方 DOM 库。你应该避免使用字符串refs，React 建议使用回调 refs。


#### 什么是高阶组件?

高阶组件是一个函数，这个函数的输入（函数的参数）是一个组件，输出（函数的返回值）是一个新的组件。高阶组件可以让你重用你的代码、逻辑和辅助抽象（原文：bootstrap abstraction）。
最常见的可能就是 Redux 的 `connect` 函数。除了简单的工具库和简单的组合，高阶函数是多个 React 组件共享行为的最好的方式。如果你发现你在不同的地方写同样的代码干同样的事，你应该就可以这些功能重构到高阶组件内。

练习：
----
- 写一个高阶组件反转输入。
- 写一个高阶组件，根据一个 API 请求数据，将这些数据提供给传入的组件。
- 写一个高阶组件，实现shouldComponentUpdate，避免不必要的重复渲染（原文：avoid reconciliation）。
- 写一个高阶组件，使用 React.Children.toArray 把他自己的子组件（children）排序，然后传给传入的组件。


#### 使用箭头函数的好处?
作用域安全：除了箭头函数，每个新的函数定义了他自己 this 的值（ this 在构造函数中是个新的对象，this在“严格模式”下的函数调用是 undefined，this 是对象，如果函数作为对象的方法调用的，等等）。箭头函数不创建他自己的this，而是指向他自己的执行环境（execution context）。
简洁：箭头函数易于读写。
清晰：当几乎所有的函数都使用箭头函数，一个普通的函数就很明显是定义作用域。开发者可以通过查找父级函数的声明，来知道 this 对象。（原文： A developer can always look up the next-higher function statement to see what the thisObject is.）

#### Why is it advised to pass a callback function to setState as opposed to an object?
Because `this.props` and `this.state` may be updated asynchronously, you should not rely on their values for calculating the next state.

#### What is the alternative of binding `this` in the constructor?
You can use property initializers to correctly bind callbacks. This is enabled by default in create react app.
you can use an arrow function in the callback. The problem here is that a new callback is created each time the component renders.

#### How would you prevent a component from rendering?
Returning null from a component's rendermethod does not affect the firing of the component's lifecycle methods.

#### When rendering a list what is a key and what is it's purpose?
Keys help React identify which items have changed, are added, or are removed. Keys should be given to the elements inside the array to give the elements a stable identity. The best way to pick a key is to use a string that uniquely identifies a list item among its siblings. Most often you would use IDs from your data as keys. When you don't have stable IDs for rendered items, you may use the item index as a key as a last resort. It is not recommend to use indexes for keys if the items can reorder, as that would be slow. 

#### What is the purpose of super(props)?

A child class constructor cannot make use of `this` until `super()` has been called. Also, ES2015 class constructors have to call `super()` if they are subclasses. The reason for passing `props` to `super()` is to enable you to access `this.props` in the constructor.

#### What is JSX?

JSX is a syntax extension to JavaScript and comes with the full power of JavaScript. JSX produces React "elements". You can embed any JavaScript expression in JSX by wrapping it in curly braces. After compilation, JSX expressions become regular JavaScript objects. This means that you can use JSX inside of if statements and for loops, assign it to variables, accept it as arguments, and return it from functions:

#### What is equivalent of the following using React.createElement?

Question:

```
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```

Answer:

```
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

#### What is `Children`?
`this.props.children` is a prop that is passed to components automatically. There are a number of methods available in the React API to work with this `prop`. These include `React.Children.map`, `React.Children.forEach`, `React.Children.count`, `React.Children.only`, `React.Children.toArray`.

#### What is state in react?
State is similar to props, but it is private and fully controlled by the component. State is essentially an object that holds data and determines how the component renders and behaves.

#### Why would you eject from create-react-app?
Until you eject you are unable to configure webpack or babel presets.

#### What is redux?
The basic idea of redux is that the entire application state is kept in a single store. The store is simply a javascript object. The only way to change the state is by firing actions from your application and then writing reducers for these actions that modify the state. The entire state transition is kept inside reducers and should not have any side-effects.

#### What is a store in redux?

The store is a javascript object that holds application state. Along with this it also has the following responsibilities:
- Allows access to state via `getState()`;
- Allows state to be updated via `dispatch(action)`;
- Registers listeners via `subscribe(listener)`;
- Handles unregistering of listeners via the function returned by `subscribe(listener)`.

#### What is an action?
Actions are plain javascript objects. They must have a type indicating the type of action being performed. In essence, actions are payloads of information that send data from your application to your store. 

#### What is a reducer?

A reducer is simply a pure function that takes the previous state and an action, and returns the next state.

#### What is Redux Thunk used for?

Redux thunk is middleware that allows you to write action creators that return a function instead of an action. The thunk can then be used to delay the dispatch of an action if a certain condition is met. This allows you to handle the asyncronous dispatching of actions. 

#### What is a pure function?
A pure function is a function that doesn't depend on and doesn't modify the states of variables out of its scope. Essentially, this means that a pure function will always return the same result given same parameters.


#### What do you like about react?
..... 

#### What don't you like about react?
.....

#### Example projects

- [React Spotify](https://github.com/Pau1fitz/react-spotify)
- [React Soundcloud](https://github.com/andrewngu/sound-redux)


