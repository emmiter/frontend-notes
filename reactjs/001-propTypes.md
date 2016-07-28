## [PropTypes](https://facebook.github.io/react/docs/reusable-components.html)

## PropTypes是[可重用组件](https://facebook.github.io/react/docs/reusable-components.html)这一节里的一小节，用于`Prop Validation`的。 我把可重用组件这一节的其他几点也都给整理了。

顾名思义，就是在说属性的类型。

之所以要谈属性的类型，那就得提到`Reusable Components`可重用组件这个东西。React的设计思想就是使用功能单一，合理分割，精心设计的组件来快速开发。那么随着项目越来越大，***确保开发者正确地使用里某个组件***这件事就变得十分重要。



幸运地是，React为开发者提供了这个`PropTypes`属性。 `React.PropTypes` 导出了一些列`validators`，用来确保你的组件接收到的数据是正确的，合法的。如果不收到的数据是非法的，控制台就会打出一条警告。***使用的时候也很简单，从React模块中导入`PropTypes`，在用的地方指定这个属性就成。***

> 为了性能考虑，只在开发环境中做`propTypes`属性值合法性检查。就是说如果你在开发环境中检查好了，确认组件都有被正确使用，那你线上环境的代码就不要做这个检查了。 再就是注意`propTypes`的大小写区别。
>
> ```javascript
> //UserInput.jsx
> improt React, {Component, PropTypes} from 'React';
>
> export default class UserInput extends Component {
>   static propTypes = {
>     className: PropTypes.string,
>     increment: PropTypes.func.isRequired
>   }
> }
> //那么在使用到UserInput组件的地方
> function inc(value) {
>   return value ++;
> }
> <UserInput className=123 increment=inc></UserInput>
> //控制台就会报错说className应该要是一个字符串，而你提供了一个数字
> ```
>
> 

### Default Prop Values

React允许开发者声明式地为`props`指定默认值：

```javascript
//官方code,非es6写法
var ComponentWithDefaultProps = React.createClass({
  getDefaultProps: function() {
    return {
      value: 'default value'
    };
  }
  /* ... */
});
```

`getDefaultProps()`的返回结果会被缓存住，用以确保`this.props.value`在没有被父组件指定值的情况，能给它一个默认值。这种默认值方式允许开发者安全地使用`props`，而不像以前那样子需要开发者自己手动去写一写重复地检查代码，还要自己来管理... 是不是很爽很方便。

### Transferring Props: A Shortcut

React组件的常见类型是以某种简单地方式继承一个基本的HTMl元素。开发者需要经常复制一些HTML attributes 并把它们传递到自己的组件中的底层HTMl元素上去。那么为了少打点字… 少感谢苦力活，可以使用*JSX spread*语法来完成这件事情:

```javascript
var CheckLink = React.createClass({
  render: function() {
    // This takes any props passed to CheckLink and copies them to <a>
    return <a {...this.props}>{'√ '}{this.props.children}</a>;
  }
});

ReactDOM.render(
  <CheckLink href="/checked.html">
    Click here!
  </CheckLink>,
  document.getElementById('example')
);
```

 这个*JSX spread*其实和 es6 中[对象的扩展运算符](http://es6.ruanyifeng.com/#docs/object#对象的扩展运算符)是一样的功能，具体干了啥事情，举个简单的🌰那就明白了:

```javascript
var fruit = ['apple','banana','melon']
var food = ['rice', 'noodle', ...fruit, 'orange'];
food // ["rice", "noodle", "apple", "banana", "melon", "orange"]

//就是把该变量的值全部copy过来
```

### Mixins

在React中，组件是最好的重用代码的方法，但有时候吧，相去甚远的组件之间可能会公用一些常用的功能。有时也被称作[cross-cutting concerns](https://en.wikipedia.org/wiki/Cross-cutting_concern)。React 就提供了`mixins`来解决这个问题。

一个常见的使用情景，当一个组件想在某个时间间隔内更新自身的时候。当然了，可以使用 `Window.setInterval()`,但是很重要的一点是，为了节省内存，当你不再需要它的时候一定要记得清除掉。React 提供了一组[生命周期方法](https://facebook.github.io/react/docs/working-with-the-browser.html#component-lifecycle)，让你得以获得组件将要被创建或销毁的时机。

让我们使用这些方法创建一个简单的`mixin`来提供一个简便的`setInterval()`函数，当组件销毁的时候，它将会被自动清除。

```react
var SetIntervalMixin = {
  componentWillMount: function() {
    this.intervals = [];
  },
  setInterval: function() {
    this.intervals.push(setInterval.apply(null, arguments));
  },
  componentWillUnmount: function() {
    this.intervals.forEach(clearInterval);
  }
};

var TickTock = React.createClass({
  mixins: [SetIntervalMixin], // Use the mixin
  getInitialState: function() {
    return {seconds: 0};
  },
  componentDidMount: function() {
    this.setInterval(this.tick, 1000); // Call a method on the mixin
  },
  tick: function() {
    this.setState({seconds: this.state.seconds + 1});
  },
  render: function() {
    return (
      <p>
        React has been running for {this.state.seconds} seconds.
      </p>
    );
  }
});

ReactDOM.render(
  <TickTock />,
  document.getElementById('example')
);
```

A nice feature of mixins is that if a component is using multiple mixins and several mixins define the same lifecycle method (i.e. several mixins want to do some cleanup when the component is destroyed), all of the lifecycle methods are guaranteed to be called. Methods defined on mixins run in the order mixins were listed, followed by a method call on the component.

### ES6 Classes 很熟悉啦~ 

The API is similar to `React.createClass` with the exception of `getInitialState`. Instead of providing a separate `getInitialState` method, you set up your own `state` property in the constructor. Just like the return value of `getInitialState`, the value you assign to`this.state` will be used as the initial state for your component.

Another difference is that `propTypes` and `defaultProps` are defined as properties on the constructor instead of in the class body.

```javascript
export class Counter extends React.Component {
  constructor(props) {
    super(props);
    this.state = {count: props.initialCount};
    this.tick = this.tick.bind(this);
  }
  tick() {
    this.setState({count: this.state.count + 1});
  }
  render() {
    return (
      <div onClick={this.tick}>
        Clicks: {this.state.count}
      </div>
    );
  }
}
Counter.propTypes = { initialCount: React.PropTypes.number };
Counter.defaultProps = { initialCount: 0 };
```

> 因为有了babel, 所以propTypes和defaultProps都可以写在类的内部了。

### No Autobinding

Methods follow the same semantics as regular ES6 classes,意味着他们不会自动绑定`this`到实例。需要开发者显示使用`.bind(this)`或者箭头函数

### No Mixins

一句话，ES6中不支持mixin,react团队在想办法能在先用的es6中使用mixins

### Stateless Functions

所谓的无状态函数，大体上就是构造函数了...

```javascript
function HelloMessage(props) {
  return <div>Hello {props.name}</div>;
}
ReactDOM.render(<HelloMessage name="Sebastian" />, mountNode);
```

或者ES6的箭头函数写法:

```javascript
const HelloMessage = (props) => <div>Hello {props.name}</div>;
ReactDOM.render(<HelloMessage name="Sebastian" />, mountNode);
```

