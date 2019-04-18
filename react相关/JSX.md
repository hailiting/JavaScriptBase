## 获取子节点 ``this.props.children``
~~~
class NodeList extends React.Component {
  render(){
    return (
      <ol>
        {
          React.Children.map(this.props.children,(child)=>{
            return <h1>{child}</h1>
          })
        }
      </ol>
    )
  }
}
export default NodeList;
import NodeList from './NodeList';
....
render(){
  return (
    <NodeList>
      <span>1111</span>
      <span>2222</span>
      <span>3333</span>
    </NodeList>
  )
}
~~~
## ``PropTypes`` 类型检查
~~~
import PropTypes from 'prop-types';
class MyTitle extends React.Component {
  static propTypes = {
    title: PropTypes.string.isRequired,
  }
  render(){
    return <h1>title: {this.props.title}</h1>
  }
}
ReactDOM.render(
  <MyTitle />,
  ...
)
~~~
## ``defaultProps``用来设置组件属性的默认值
~~~
class MyTitle extends React.Component {
  static defaultProps = {
    shortName: 'MyTitle',
  }
  render(){
    return <h1>{this.props.shortName}</h1>
  }
}
~~~
## ref属性（获取真实的DOM节点）
~~~
class Alert extends React.Component {
  showAlert(message){
    alert(`Debug: ${message}`);
  }
  render(){
    return null;
  }
}
class MyTitle extends React.Component {
  onClick = ()=>{
    this.refs.alert.showAlert('MyTitle');
  }
  render(){
    return <div>
        <h1 onClick={this.onClick}>Click me</h1>
        <Alert ref="alert" />
      </div>
  }
}
ReactDOM.render(<MyTitle />, document.getElementById('root'));
~~~
## ``componentWillMount`` 与 ``componentWillReceiveProps``  将被抛弃
~~~
componentWillMount => componentDidMount
// componentWillReceiveProps => getDerivedStateFromProps
class ExampleComponent extends React.Component {  
  state = {};
  static getDerivedStateFromProps(nextProps, prevState) {
    if(prevState.someMirroredValue !== nextProps.someValue){
      return {
        derivedDate: computeDerivedState(nextProps),
        someMirroredValue: nextProps.someValue,
      }
    }
    return null
  }
}

~~~
