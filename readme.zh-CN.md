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
rarely used. It can be used instead of `componentWillReceiveProps` on a component that also has `shouldComponentUpdate` (but no access to previous props).
- `componentDidUpdate` - 也用于在属性和状态改变之后更新 DOM 。
also commonly used to update the DOM in response to prop or state changes.
- `componentWillUnmount` - here you can cancel any outgoing network requests, or remove all event listeners associated with the component.

#### Where in a React component should you make an AJAX request?
`componentDidMount` is where an AJAX request should be made in a React component. This method will be executed when the component “mounts” (is added to the DOM) for the first time. This method is only executed once during the component’s life. Importantly, you can’t guarantee the AJAX request will have resolved before the component mounts. If it doesn't, that would mean that you’d be trying to setState on an unmounted component, which would not work. Making your AJAX request in `componentDidMount` will guarantee that there’s a component to update.

#### What are controlled components?

In HTML, form elements such as `<input>`, `<textarea>`, and `<select>` typically maintain their own state and update it based on user input. When a user submits a form the values from the aforementioned elements are sent with the form. With React it works differently. The component containing the form will keep track of the value of the input in it's state and will re-render the component each time the callback function e.g. `onChange` is fired as the state will be updated. An input form element whose value is controlled by React in this way is called a "controlled component".

#### What are refs used for in React?

Refs are used to get reference to a DOM node or an instance of a component in React. Good examples of when to use refs are for managing focus/text selection, triggering imperative animations, or integrating with third-party DOM libraries. You should avoid using string refs and inline ref callbacks. Callback refs are advised by React.

#### What is a higher order component?

A higher-order component is a function that takes a component and returns a new component. HOC's allow you to reuse code, logic and bootstrap abstraction. The most common is probably Redux’s `connect` function. Beyond simply sharing utility libraries and simple composition, HOCs are the best way to share behavior between React Components. If you find yourself writing a lot of code in different places that does the same thing, you may be able to refactor that code into a reusable HOC.

<p>Exercises</p>

----
- Write an HOC that reverses it’s input
'- Write an HOC that supplies data from an API to it’s Passed Component
- Write an HOC that implements shouldComponentUpdate to avoid reconciliation.
- Write an HOC that uses React.Children.toArray to sort the children passed to it's Passed Component.


#### What advantages are there in using arrow functions?
Scope safety: Until arrow functions, every new function defined its own this value (a new object in the case of a constructor, undefined in strict mode function calls, the base object if the function is called as an "object method", etc.). An arrow function does not create its own this, the this value of the enclosing execution context is used. 
Compactness: Arrow functions are easier to read and write.
Clarity: When almost everything is an arrow function, any regular function immediately sticks out for defining the scope. A developer can always look up the next-higher function statement to see what the thisObject is.

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


