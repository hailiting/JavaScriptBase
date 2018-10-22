## 事件处理
#### 传参
~~~
<button onClick={(e)=>this.deleteRow(id,e)}>Delete Row</button>
<button onClick={this.deleteRow.bind(this,id)}>Delete Row</button>
~~~
## 条件渲染
简单的条件渲染

~~~
function UserGreeting(props){
  return <h1>欢迎回来</h1>;
}
function GuestGreeting(props){
  return <h1>请先注册！</h1>
}
function Greeting(props){
  const isLoggedIn = props.isLoggedIn;
  if(isLoggedIn){
    return <UserGreeting />;
  }
  return <GuestGreeting />
}
ReactDOM.render(
  <Greeting isLoggedIn = {false} />,
  document.getElementById('root')
);
~~~
#### 元素变量
~~~
import React from 'react';
import ReactDOM from 'react-dom';
// import PropTypes from 'prop-types'
import './index.css';
import * as serviceWorker from './serviceWorker';
////////////////////////////////////////
function UserGreeting(props){
    return <h1>欢迎回来！</h1>
}
function GuestGreeting(props){
    return <h1>请先注册</h1>
}
function Greeting(props){
    const isLoggedIn= props.isLoggedIn;
    if(isLoggedIn){
        return <UserGreeting />
    }
    return <GuestGreeting />
}
function LoginButton(props){
    return (
        <button onClick = {props.onClick}>登陆</button>
    )
}
function LogoutButton(props){
    return (
        <button onClick = {props.onClick}>退出</button>
    )
}
///////////////////////////////////////
class LoginControl extends React.Component{
    constructor(props){
        super(props);
        this.handleLoginClick = this.handleLoginClick.bind(this);
        this.handleLogoutClick = this.handleLogoutClick.bind(this);
        this.state = {isLoggedIn: false};
    }
    handleLoginClick(){
        this.setState({isLoggedIn: true});
    }
    handleLogoutClick(){
        this.setState({isLoggedIn: false});
    }
    render(){
        const isLoggedIn = this.state.isLoggedIn;
        let button = null;
        if(isLoggedIn){
            button = <LogoutButton onClick = {this.handleLogoutClick} />;
        } else {
            button = <LoginButton onClick={this.handleLoginClick} />;
        }
        return (
            <div>
                <Greeting isLoggedIn={isLoggedIn} />
                {button}
            </div>
        )
    }
}
ReactDOM.render(
    <LoginControl />,
    document.getElementById('root')
);
serviceWorker.unregister();
~~~
### && 与运算符
~~~
function Mailbox(props){
    const unreadMessages = props.unreadMessages;
    return (
        <div>
            <h1>Hello!</h1>
            {unreadMessages.length > 0 && 
            <h2>您有{unreadMessages.length}条未读消息</h2>}
        </div>
    );
}
const messages = ['React','Re: React','Re:Re: React'];
ReactDOM.render(
    <Mailbox unreadMessages={messages} />,
    document.getElementById('root')
)
~~~
### 三目运算符
~~~
// condition ? true:false
render(){
  const isLoggedIn = this.state.isLoggedIn;
  return (
    <div>
      {isLoginedIn ? (
        <LogoutButton onClick = {this.handleLogoutClick} />
      ) : (
        <LoginButton onClick = {this.handleLogoutClick} />
      )
      }
    </div>
  );
}
~~~
### 阻止组件渲染
~~~
function WarningBanner (props){
    if(!props.warn){
        return null;
    }
    return (
        <div className="warning">
            警告！
        </div>
    );
}
class Page extends React.Component{
    constructor(props){
        super(props);
        this.state = {showWarning: true};
        this.handleToggleClick = this.handleToggleClick.bind(this);
    }
    handleToggleClick(){
        this.setState(prevState =>({
            showWarning: !prevState.showWarning
        }));
    }
    render(){
        return(
            <div>
                <WarningBanner warn={this.state.showWarning} />
                <button onClick={this.handleToggleClick}>
                    {this.state.showWarning ? '隐藏':'显示'}
                </button>
            </div>
        )
    };
}
ReactDOM.render(
    <Page />,
    document.getElementById('root')
)
~~~
