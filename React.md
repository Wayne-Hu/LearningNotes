# React
## Components
React is all about modular, composable components.

> var Clazz = React.createClass();其中ClassName==首字母必须大写==！
> 一个render里面只能有一个父节点

```javascript
var CommentBox = React.createClass({
  render: function() {
    return (
      // div在这里并非是真正的DOM节点，只是React的div组件
      <div className="commentBox">
        Hello, world! I am a CommentBox.
      </div>
    );
  }
});
React.render(
  <CommentBox />,
  document.getElementById('content')
);
```

## Using Props
* this.props.data
* this.props.children

```javascript
var Comment = React.createClass({
  render: function() {
    return (
      <div className="comment">
        <h2 className="commentAuthor">
          {this.props.author}
        </h2>
        {this.props.children}
      </div>
    );
  }
});
```
通过组件的父组件传入进来的数据被当做property，可以通过**this.props**来访问这些属性，通过**this.props.children**来访问嵌套的elements。

### 支持Markdown
首先添加markdown支持的类库

```javascript
<script src="https://cdnjs.cloudflare.com/ajax/libs/marked/0.3.2/marked.min.js"></script>
```
然后使用marked()来渲染markdown格式，但直接渲染不行，因为有可能会导致XSS攻击，所以应该采用下面的方式：

```javascript
var rawMarkup = marked(this.props.children.toString(), {sanitize: true});
<span dangerouslySetInnerHTML={{__html: rawMarkup}} />
```

### 建立data model
```javascript
var data = [
  {author: "Pete Hunt", text: "This is one comment"},
  {author: "Jordan Walke", text: "This is *another* comment"}
];

var CommentBox = React.createClass({
  render: function() {
    return (
      <div className="commentBox">
        <h1>Comments</h1>
        <CommentList data={this.props.data} />
        <CommentForm />
      </div>
    );
  }
});

React.render(
  <CommentBox data={data} />,
  document.getElementById('content')
);
```
可以通过url来从服务器获取动态数据

```javascript
<CommentBox url="comments.json" />
```
对于**props**来说，它是不可变的，如果想要可变的数据，需要用**state**

## Reactive state
* getInitialState()
* componentDidMount()
* this.state.data
* this.setState()

```javascript
// getInitialState()在组件的生命周期中只执行一次。
getInitialState: function() {
  return {data: []};
},
// 当组件被rendered时，该方法由React自动调用。
componentDidMount: function() {
  // 调用this.setState()用来改变state值
  this.setState({data: data});
}

<CommentList data={this.state.data} />
```

* **Autobinding**
* **Event Delegation**

> 减少state的使用，通用方式是定义一些纯粹的渲染组件，在定义父组件将这些渲染组件包裹起来，通过父组件来动态改变数据，子组件通过**props**来访问数据。

## Form交互
* onSubmit
* ref
* e.preventDefault()
* React.findDOMNode()
* onCommentSubmit
* this.props.onCommentSubmit()

```javascript
handleSubmit: function(e) {
  // 阻止浏览器执行提交
  e.preventDefault();
  // 其它处理代码...
  // 使用React.findDOMNode()查找refs组件
  React.findDOMNode(this.refs.author);
}
render: function() {
    return (
      // onSubmit绑定处理函数
      <form className="commentForm" onSubmit={this.handleSubmit}>
        // 使用ref定义form组件的子组件名称
        <input type="text" placeholder="Your name" ref="author" />
        <input type="text" placeholder="Say something..." ref="text" />
        <input type="submit" value="Post" />
      </form>
    );
  }
}
```

```javascript
handleCommentSubmit: function(comment) {
    // TODO: submit to the server and refresh the list
},
render: function() {
  return (
    // ...
    // 在render中使用onCommentSubmit将组件方法和子组件的回调绑定
    // 在子组件中就可以调用this.props.onCommentSubmit()来回调方法了
    <CommentForm onCommentSubmit={this.handleCommentSubmit} />
    // ...
)}
```

> 交互不止用于Form中，也可以用于其它的标签，例如\<button onClick={this.handleClick}>click\</button>，以及其它标签都可以使用，==只需要将事件处理方法放入普通HTML的事件处理属性中即可==！
> If you'd like to use React on a touch device such as a phone or tablet, simply call ==React.initializeTouchEvents(true);== to enable touch event handling.

## 其它
==区分Owner-Ownee关系和Parent-Children关系==
In React, **an owner is the component that sets the props of other components**.