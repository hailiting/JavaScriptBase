### 1，函数的绑定
### 2, 用immutatble对对象操作
### 3, pureComponent  ||  shouldComponentUpdata(nextProps,nextState){}
### 4, reselect对redux优化
~~~
import React from 'react';
import {Map,is} from 'immutable';

// // reselect优化redux选择器
// import {createSelector} from 'reselect';
// const numSelector = createSelector(
//   state =>state,
//   // 第二个函数的参数是第一个的返回值
//   state=>({num:state*2})
// )
// // 装饰器模式
// @connect(
//   state=>numSelector(state),
//   {add....}
// )

// 性能优化，索引值
Map(v=> <div key={v}>{v}</div>)
// 下面这样写除去提示外，没有任何效果
Map((v,i)=> <div key={i}>{v}</div>)





let objimm = Map({name: 1, title:"imooc", b: { a: 1 }});
let objimm02 = Map({name:1, title:"imooc", b: { a: 1 }});
console.log(is(objimm,objimm02));

// immutablejs
/**
 * 减少内存使用
 * 并发安全
 * 降级项目复杂度
 * 便于比较复杂数据，定制shouldComponentUpdate方便
 * 时间旅行功能（新的数组）
 * 函数编程
 * 
 * 
 * 学习成本
 * 库的大小  seamless-immutable 
 * 
 */
// react=》只做浅层对比
// 递归对比，复杂度太高，不可接受 
function compareObj(obj1, obj2) {
  if (obj1 === obj2) {
    return true;
  }
  if (Object.keys(obj1).length !== Object.keys(obj2).length) {
    return false;
  }
  for (let k in obj1) {
    if (typeof obj1[k] === 'object') {
      return compareObj(obj1[k], obj2[k])
    } else if (obj1[k] !== obj2[k]) {
      return false;
    }
  }
  return true
}
console.log(compareObj(objimm, objimm02));


class App extends React.Component {
  constructor(props) {
    super(props);
    this.state = Map({
      num: 0,
      title: 'test',
    });
    this.handleClick = this.handleClick.bind(this);
    this.handleTitleChangeClick = this.handleTitleChangeClick.bind(this);
  }
  handleClick() {
    this.setState(
      this.state.set('num', this.state.get('num')+1)
      // {num: this.state.num + 1}
    )
  }
  handleTitleChangeClick() {
    this.setState(
      this.state.set('title',this.state.get('title')+1)
      // {title: this.state.title + this.state.num,}
    )
  }
  // react_perf   Performece =>  运行
  render() {
    return (
      <div>
        <h2>App，{this.state.num}</h2>
        <button onClick={this.handleClick}>btn01</button>
        <button onClick={this.handleTitleChangeClick}>btn02</button>
        <Dome title={this.state.get('title')}></Dome>
      </div>
    );
  }
}
class Dome extends React.PureComponent {
  shouldComponentUpdate(nextProps, nextState) {
    return is(nextProps, this.props);
  }
  render() {
    return <h2>I am dome {this.props.title}</h2>
  }
}
export default App;

~~~
