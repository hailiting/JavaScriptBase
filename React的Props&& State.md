### Props
#### state和props主要区别在于props是不可变的。而state可以根据与用户交互来改变。所以一些容器组件需要定义state来更新和修改数据，而子组件只能用
      props来传递
###### 使用Props
~~~
function HelloMessage(props){
  return <h1>Hello {props.name}</h1>;
}
const element = <HelloMessage name="hai"/>;
ReactDOM.render(
  element,
  document.getElementById('root')
);
~~~
###### 默认Props
~~~
class HelloMessage extends React.Component{
  render(){
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}
HelloMessage.defaultProps={
  name: 'hai'
};
const element = <HelloMessage/>
ReactDOM.render(
  element,
  document.getElementById('root')
)
~~~
### State和Props组合使用
通过父组件上使用state,通过在子组件上使用props将值传递到子组件上。
在render函数中，我们设置name和site来获取传递过来的数据
~~~
class WebSite extends React.Component{
  constructor(){
    super();
    this.state = {
      name: "hai",
      site: "杭州"
    }
  }
  render(){
    return (
      <div>
        <Name name={this.state.name} />
        <Link site={this.state.site} />
      </div>
    )
  }
}
class Name extends React.Component{
  render(){
    return (
      <h1>{this.props.name}</h1>
    );
  }
}
class Link extends React.Component{
  render(){
    return(
      <a href={this.props.site}>
        {this.props.site}
      </a>
    );
  }
}
ReactDOM.render(
  <WebSite />,
  document.getElementById("root")
)
// WebSite设置state，Name和Link用props来调用state，最终在WebSite里显示
~~~
