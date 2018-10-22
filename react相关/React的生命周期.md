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
~~~
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import * as serviceWorker from './serviceWorker';

class Clock extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            date: new Date()
        };
    }
    // 组件输出到DOM后执行componentDidMount()
    componentDidMount() {
        this.timerID = setInterval(
            () => this.tick(),
            1000
        )
    }
    // 卸载的时候调用
    componentWillUnmount(){
        clearInterval(this.timerID);
    }
    tick(){
        this.setState({
            date: new Date()
        });
    }
    render(){
        return (
            <div>
                <h1>HELLO WORLD</h1>
                <h2>现在是{this.state.date.toLocaleTimeString()}.</h2>
            </div>
        )
    }
}
ReactDOM.render(
    <Clock />,
    document.getElementById('root')
)
/**
 * 1，当<Clock/>被传递给ReactDOM.render()时，React调用Clock组件的构造函数。由于Clock需要显示当前时间，所以使用包含当前时间的对象来初始化this.state.稍后在更新这个状态。
 * 2，React然后调用Clock组件的render()方法，这时React了解屏幕上应该显示什么内容，然后React更新DOM以匹配Clock的渲染输出。
 * 3，当Clock的输出插入DOM中时，React调用componentDidMount()生命周期钩子。在其中，Clock组件要求浏览器设置一个定时器，每秒调用一次tick().
 * 4，浏览器每秒调用tick()方法。在其中，Clock组件通过使用包含当前时间的对象调用setState()来调度UI更新。通过调用setState(), react知道状态的改变，并再次调用render()方法来明确屏幕上应当显示什么。這一次，render()方法中的this.state.date将不同，所以渲染输出将包含更新的时间，并相应的更新DOM。
 * 一旦Clock组件被从Dom中移除，React会调用ComponentWillUnmount()这个钩子函数，定时器也就会被清除。
 **/
serviceWorker.unregister();
~~~


