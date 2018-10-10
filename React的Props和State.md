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
React生命周期为三种状态  
1，初始化；
2，更新；
3，销毁；
### 初始化：
getDefaultProps() 
> 设置默认的props，也可以用dufaultProps设置组件的默认属性
getInitialState()
> 使用es6的class语法时是没有这个钩子函数的，可以直接在constructor中定义this.state.此时可以访问this.props
componentWillMount()
> 组件初始化时调用，以后组件更新不调用，整个生命周期只调用一次，此时可以修改state
render
> react最重要的步骤，创建虚拟dom，进行diff算法，更新dom树都在此进行，此时就不能在更改state了
componentDidMount  
> 组件渲染之后调用，只调用一次
### 更新：
##### 阶段一：
属性（props）改变
componentWillReceiveProps(nextProps)
> 组件初始化时不调用，组件接受新的props时调用
##### 阶段二：
状态(state)改变
shouldComponentUpdate(nextProps,nextState)
> react关于性能的重要一环。对比props和state，节约资源
componentWillUpdate(nextProps,nextState)
> 组件初始化不调用，只有在组件将要更新时才调用，此时可以修改state
render()
> 组件渲染
componentDidUpdate()
> 组件初始化时不调用，组件更新完成后调用，此时可以获取dom节点
### 卸载：
componentWillUnmount
> 组件将要卸载的时候调用，一些事件监听和定时器需要在此时清楚。




