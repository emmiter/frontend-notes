### [Type of the Children props](https://facebook.github.io/react/tips/children-props-type.html)

通常情况下，某个组件的孩子(`this.props.children`)是一个包含着组件的数组:

```react
var GenericWrapper = React.createClass({
  componentDidMount: function() {
    console.log(Array.isArray(this.props.children)); // => true
  },

  render: function() {
    return <div />;
  }
});

ReactDOM.render(
  <GenericWrapper><span/><span/><span/></GenericWrapper>,
  mountNode
);
```

但是，当只有一个孩子时，`this.props.children`will be the single child component itself *without the array wrapper*. This saves an array allocation.

```react
var GenericWrapper = React.createClass({
  componentDidMount: function() {
    console.log(Array.isArray(this.props.children)); // => false

    // warning: yields 5 for length of the string 'hello', not 1 for the
    // length of the non-existent array wrapper!
    console.log(this.props.children.length);
  },

  render: function() {
    return <div />;
  }
});

ReactDOM.render(<GenericWrapper>hello</GenericWrapper>, mountNode);
```

