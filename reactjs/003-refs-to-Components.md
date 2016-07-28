## [Refs to Components](https://facebook.github.io/react/docs/more-about-refs.html)

干啥的？ 就是获取React 组件的引用。 在组件内部，你可以使用`this`获取；也可以使用`ref`属性来获得你自己组件的引用。

它们按如下方式工作:

```react
var MyComponent = React.createClass({
  handleClick: function() {
    // Explicitly focus the text input using the raw DOM API.
    if (this.myTextInput !== null) {
      this.myTextInput.focus();
    }
  },
  render: function() {
    // The ref attribute is a callback that saves a reference to the
    // component to this.myTextInput when the component is mounted.
    return (
      <div>
        <input type="text" ref={(ref) => this.myTextInput = ref} />
        <input
          type="button"
          value="Focus the text input"
          onClick={this.handleClick}
        />
      </div>
    );
  }
});

ReactDOM.render(
  <MyComponent />,
  document.getElementById('example')
);
```

