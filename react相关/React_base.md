## VirtualDom模型
~~~
<h2>
  hello imooc i love React& Rdux
</h2>
=>
"use strict"
React.createElement(
  'h2',
  null,
  'hello imooc i love React& Rdux'
)
// 
<h2 data-id='imooc' style='color: red'>
  <p>hello imooc i love React& Rdux</p>
</h2>
=>
'use strict'
React.createElement(
  'h2',
  {'data-id':'imooc',style: 'color: red'}
  React.createElement(
    'p',
    {'data-name':'react rocks!'},
    'hello imooc i love React& Rdux'
  )
)
~~~
## 生命周期
~~~
Inital render
constructor() => 
componentWillMount() => 
componentDidMount()=>
componentWillUnmount()
父组件render
componentWillReceiveProps()=>
// return true   render()
// return false  不渲染页面
shouldComponentUpdate()[this.setState()]
=>
componentWillUpdate()[this.forceUpdate()]=>
render() => 
componentDidUpdate()=>
componentWillUnmount()
~~~
~~~
...
// 5, 10 ...
shouldCompomentUpdata(nextProps,nextState){
  if(nextState.num%5==0){
    return ture
  }
  return false
}
...
~~~
## this.setState({},()=>{})
1, setState是异步的
2, setState只提交一次修改到队列里，等满足一定条件时，react会合并队列中的所有修改，触发update，更新this.state
3, 不能再render里调用setState
## Diff
## Redux
### 新建保险箱
#### createStore()
#### getState()
### 订阅，每次state修改，都会执行listener
#### subScribe(listener)
### 提交状态变更的申请
#### dispatch()
#### subScribe(listener)
~~~
// mini.redux.js
expoert function createStore(reducer){
  currentState = {}
  currentListener = []
  function getState(){
    return currentState
  }
  function subScribe(listener){
    currentListener.push(listener)
  }
  function dispatch(action){
    currentState = reducer(currentState, action)
    currentListener.map(v=>v())
  }
  dispatch({type: '@type/init'})
  return {getState, subScribe, dispatch}
 }
~~~
~~~
// 使用mini.redux
import {createStore} from 'mini.redux'
function counter(state = 0,action){
  console.log(state,action)
  switch (action.type){
    case
  }
}
~~~
