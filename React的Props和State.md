# React的Props和State
## React把组件看成是状态机，通过与用户的交互，实现不同的状态，从而改变ui，让用户界面和数据保持一致
> tip: 状态机由状态寄存器和组合逻辑电路构成，能够根据控制信号按照预先设定的状态进行状态转移，
  是协调相关信号动作、完成特定操作的控制中心。状态机简写为FSM。
~~~
// 创建一个扩展名为React.Component的ES6类
class Clock extends React.Component{
  // 添加一个类构造函数来初始化状态this.state，类组件应始终使用props调用基础构造函数
  construstor(props){
    super(props);
    this.state = {date: new Date()}
  },
  render(){
    return (
      // 在render里使用 this.state来改变当前时间
      <div>
        <h1>hello world!</h1>
        <h2>现在是{this.state.date.toLocaleTimeString()}.</h2>
      </div>
    )
  }
}
ReactDOM.render(
  <Clock />,
  document.getElementById('example')
)
~~~
## React生命周期
