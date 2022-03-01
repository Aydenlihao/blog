---
title: React 组合vs继承
date: 2020-08-20 14:03:48
tags:
  - React
category: JavaScript
---

有些组件无法提前知晓它们子组件的具体内容，所以我们建议这些组件使用一个特殊的 children prop 来将他们的子组件传递到渲染结果中：

```javaScript
function FancyBorder(props) {
  return (
    <div className={'FancyBorder FancyBorder-' + props.color}>
      {props.children}
    </div>
  );
}
```

使得使用组件时，可以将任意组件作为子组件传递给它们。

```javaScript
function Dialog(props) {
  return (
    <FancyBorder color="blue">
      <h1 className="Dialog-title">
        {props.title}
      </h1>
      <p className="Dialog-message">
        {props.message}
      </p>
      {props.children}
    </FancyBorder>
  );
}

class SignUpDialog extends React.Component {
  constructor(props) {
    super(props);
    this.handleChange = this.handleChange.bind(this);
    this.handleSignUp = this.handleSignUp.bind(this);
    this.state = {login: ''};
  }

  render() {
    return (
      <Dialog title="Mars Exploration Program"
              message="How should we refer to you?">
        <input value={this.state.login}
               onChange={this.handleChange} />
        <button onClick={this.handleSignUp}>
          Sign Me Up!
        </button>
      </Dialog>
    );
  }

  handleChange(e) {
    this.setState({login: e.target.value});
  }

  handleSignUp() {
    alert(`Welcome aboard, ${this.state.login}!`);
  }
}
```

使用这种组件的方法，类似于我们 slot 的使用，在父组件中嵌入子组件，父组件中就可以通过 prop children 获取子组件的内容。不过如果子组件要进行操作，不需要通过父组件调用函数，组件在嵌入的地方调用指定函数。
