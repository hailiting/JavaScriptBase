# package.json 插件解读
## dependencies 开发依赖环境
### antd
阿里巴巴UI框架
### classnames
类名组合框架
### es6-promise
支持promise写法
### es6-shim
ES6 兼容 ES5
### immutable
原理：immutable实现的原理是Persistent Structure(持久化数据结构)，也就是当旧数据创建新数据时，要保证数据同时可用且不变。同时为避免deepCopy把所有节点都复制一遍带来的性能损耗，immutable使用了Structural Sharing(结构共享)，即如果对象树中一个节点发生变化，只修改这个节点和受他影响的父节点，其他则进行共享。
immutable 有两个库
1，immutablejs
2, seamless-immutable
常用方法： ``Collection``, ``List``, ``Map``, ``Set``, ``Record``, ``Seq``.
~~~~
// 原始写法
let foo = {
    a: {
        b: 1
    }
}
let bar = foo;
bar.a.b = 2;
console.log(foo.a.b) // 2
console.log(foo === bar) // true

// 使用 immutable.js 后
import Immutable from 'immutable';
foo = Immutable.fromJS({a:{b:1})
bar = foo.setIn(['a', 'b'],2); // 使用setIn赋值
console.log(foo.getIn(['a','b'])); // 使用getIn取值，打印1
console.log(foo===bar); // 打印 false

// 使用 seamless-immutable.js 后
import SImmutable from 'seamless-immutable';
foo = SImmutable({a:{b:1}})
bar = foo.merge({a: {b:2}})
console.log(foo.a.b) // 1
console.log(foo === bar // false
~~~~
#### 优点
1，Immutable 降低了Mutable带来的复杂度
2，节省内存
3，Undo/Redo, Copy/Paste, 甚至时间旅行这些功能做起来小菜一碟
4，并发安全
5，拥抱函数式编程
#### 缺点
1，学习新的api
2, 增加了资源文件大小
3，容易与原生对象混淆
#### 更多认识
~~~
import Immutable from 'immutable';
import Cursor from 'immutable/contrib/cursor';
let data = Immutable.fromJS({a: {b:{c:1}}});
let cursor = Cursor.from(data, ['a', 'b'], newData =>{
    console.log(newData);
})
cursor.get('c') // 1
cursor = cursor.update('c',x=>x+1)
cursor.get('c'); // 2
~~~
### isomorphic-fetch 
支持ajax请求
#### fetch-新一代的Ajax API
Ajax半遮半掩的底层API是备受诟病的一件事情。XMLHttpRequest并不是转为ajax设置的。虽然各种框架对xhr的封装已经足够好，但我们可以做到更好。window.fetch方法，在最新版本发Firefox和Chrome已经得到支持。
1，语法简介，更加语义化
2，基于标准的Promise实现，支持asynic/await
3，同构方便，使用isomorphic-fetch
~~~
// url 必须的, options 可选
fetch('/some/url', {
    method: 'get'
}).then(response =>{
    console.log(response.json())
}).then(
    data=>{
        console.log(data)
    }
).catch(err=>{
    // 出错在这处理
})
~~~
##### 设置请求头
~~~
// 创建一个空的headers对象
var headers = new Headers();

// 添加 append 请求头信息
headers.append('Content-Type', 'text/plain');
headers.append('X-My-Custom-Header', 'CustomValue');

// 判断（has），获取（get）， 以及修改（set）请求头的值。
headers.has('Content-Type'); // true
haeders.get('Content-Type'); // 'text/plain'
headers.set('Content-Type', 'application/json');

// 删除请求头信息
header.delete('X-My-Custom-Header');

// 创建对象时设置初始化信息
var headers =  new Headers({
    'Content-Type': 'text/plain',
    'X-My-Custom-Header': 'CustomValue'
})
~~~
##### Request
~~~
var request = new Request(url, {
    method: 'POST',
    mode: 'cors', // 可以设置 cors, no-cors, same-origin
    credentials: 'omit', // 设置cookies是否随请求一起发送。可设置： omit, same-origin
    redirect: 'follow', // follow, error, manual
    integrity: 'subresource'，
    headers:  new Headers({
        'Content-Type': 'text/plain'
    })
})
// 使用
fetch(request).then(function(){
    /* handle response */
})
~~~
##### Response
1，json格式
~~~
fetch(url).then(response=>{
    return response.json()
}).then(res=>{
    console.log(res)
})
~~~
2, 返回HTML/text
~~~
fetch(url).then(res=>{
    return res.text()
}).then(text=>{
    console.log(text)
})
~~~
3，发送form表单数据
~~~
// from data
var form = document.querySelector('form');
fetch(url,{
    method: 'post',
    body: new FormDate(form)
})
// JSON
fetch(url,{
    method: 'post',
    body: JSON.stringify({
        name: 'xxx',
        blog: 'url'
    })
})
~~~
4，图像处理
~~~
fetch(url).then(res=>{
    return response.blob()
}).then(imgBlob=>{
    document.querySelector('img').src = URL.createObjectURL(imgBlob);
})
~~~
### React
React是一个用于构建用户界面的JAVASCRIPT库，React主要用于构建UI，是MVC里的V框架。
### react-cookie
在任何地方都可以获取、设置和删除Cookie和Cookie实例
#### Cookie.save
~~~
// domain 域
// path cookie 共享的根目录
// maxAge 生存期
Cookie.save(
    key,
    cookie[key],
    {
        domain,
        path: '/',
        maxAge: new Date().setDate(new Date().getDate +30)
    }
)
~~~
##### Simple Example
~~~
// Root.jsx
import React from 'react';
import App from './App';
export default function Root(){
    return (
        <CookiesProvider>
            <App />
        </CookiesProvider>
    )
}
~~~
~~~
App.jsx
import React, { Component } from 'react';
import { instanceOf } from 'prop-types';
import { withCookies, Cookies } from 'react-cookie';

import NameForm from './NameForm';

class App extends Component{
    static propTypes = {
        cookies: instanceOf(Cookies).isRequired
    };
    constructor(props) {
        super(props);
        const { cookies } = props;
        this.state = {
            name: cookie.get('name') || 'Ben'
        };
    }
    handleNameChange(name){
        const { cookies } = this.props;
        cookie.set('name', name, { path: '/' });
        this.setState({name});
    }
    render(){
        const { name } = this.state;
        return {
            <div>
                <NameForm name={name} onChange={this.handleNameChange.bind(this)} />
                {this.state.name && <h1> hello {this.state.name} !</h1>}
            </div>
        }
    }
}
export default withCookie(App);
~~~
##### Server-Rendering Example
~~~
// server.js
require('@babel/register);
const express = require('express');
const serverMiddleware = require('./src/server').default;
const cookiesMiddleware = require('universal-cookie-express');
const app = express();

app
    .use('/assets',express.static('dist'))
    .use(cookiesMiddleWare())
    .use(serverMiddleware);
app.listen(8080, function(){
    console.log('listen 8080')
})
~~~
~~~
// ./src/server.js
import React from 'react';
import ReactDOMServer from 'react-dom/server';
import { CookiesProvider } from 'react-cookie';

import Html from './components/Html'
import App from './components/App'

export default function middleware(req, res){
    const markup = ReactDOMServer.renderToString(
        <CookiesProvider cookies= {req.universalCookies}>
            <App />
        </CookiesProvider>
    );
    const html = ReactDOMServer.renderToStaticMarkup(<Html markup={markup} />)
    res.send('<!DOCTYPE html' + html);
}
~~~
### react-dom
Dom和服务器渲染的入口点，渲染Dom元素。
### react-intl
react-intl 是 Yahoo 公司出品的用于react app国际化的组件，提供了用于格式化日期、数字和字符串的API、复数和处理翻译。
#### 第一步：新建语言包
en-US.json文件用于书写英文名称、zh-CN用于书写中文名
英文名词： en-US.json
~~~
    "HELLO_WORLD": “Hello world”
~~~
中文： zh-CN.json
~~~
{
    "HELLO_WORLD": "你好 世界！"
}
~~~
#### 第二步：配置使用
react-intl使用方式类似于react-redux，同样在顶层提供一个IntlProvider为下层组件提供数据。所以在将会用到的国际化语言包配置的最顶层组件文件中配置使用IntlProvider.
~~~
import React, { Component } from 'react';
import ReactDOM from 'react-dom';
import { IntlProvider, FormattedMessage } from 'react-intl';
// 导入语言包，路径为你语言包所在路径
import enUS from './en-US.json';
import zhCN from './zh-CN.json';

class App extends Component {
    render() {
        return (
            <IntlProvider locale= "en" message = { zhCN }>
                <FormattedMessage id="HELLO_WORLD" />
            </IntlProvider>
        )
    }
}
ReactDOM.render(<App />, document.getElementById('app'))
~~~
###### I18N=> 其来源于英文单词internationalization的首末字符i和n,18为中间的字符数。是国际化的简称。
#### API
这个中间用于react树的i18n上下文。
##### 配置属性
~~~
type IntlConfig={
    // 当前语言环境
    local?: string,
    // 格式化对象
    formats?: object,
    // 语言包
    message?: {
        [id: string]: string
    },
    // 默认语言环境
    defaultLocale?: string="en",
    // 默认格式化对象
    defaultFormats?: Object={},
    // 文本组件，用于设置默认的消息DOM结点类型
    textComponent? node='span',
}
~~~
##### Prop Types
~~~
props: IntlConfig & {
    children: ReactElement,
    initialNow?: any
}
~~~
``IntlProvider``，只能接收一个子组件。
~~~
const App = ({importantDate})=>(
    <div>
        <FormattedDate
            value={importantDtae}
            year='numeric'
            month=’long‘
            day='numeric'
            weekday='long'
            />
    </div>
)
ReactDOM.render(
    <IntlProvider locale={navigator.language}>
        <App importantDate={new Date(13444456666)} />
    </IntlProvider>,
    document.getElementById('container')
)
~~~
如果navigator.language是fr
~~~
<div><span>mardi 5 avril 2016</span></div>
~~~
用于格式化日期，使用了formatDate和Intl.DateTimeFormat的API.
Prop Types:
~~~
props: DateTimeFormatOptions & {
    value: any,
    format?: string,
    children?: (formattedDate: string)=> ReactElement
}
~~~
~~~
<FormattedDate 
    value={new Date(23444444444)}
    year="numeric"
    month="long"
    day="2-digit"
/>
// 渲染后
<span>April 05, 2016</span>
~~~
#### 用于字符串组件化
React Intl提供了两个组件用于格式化字符串
``<FormattedMessage>``
``<FormattedHTMLMessage>``
<FormattedMessage>具有更好的富文本格式化能力并具有更高的性能。推荐使用<FormattedMessage>.如果要格式化的字符串包含HTML，可以使用<FormattedHTMLMessage>
##### 语法
简单的
~~~
Hello, {name}
~~~
复杂
~~~
Hello, {name}, you have {
    itemCount,
    plural,
    =0{no items}
    one{ # item}
    other {# items}
}
~~~
##### 消息描述符，用于定义应用程序的默认消息/字符串
* id： 唯一，消息的标识符
* description: 为翻译器如何在UI中使用而定义上下文
* defaultMessage: 默认消息
###### 例子
~~~
type MessageDescriptor = {
    id: string,
    defaultMessage?: string,
    description?: string | object,
}
props: MessageDescriptor & {
    value?: object,
    tagName?: string,
    children?: (
        ...formattedMessage: Array<ReactElement>
    )=> ReactElement,
}
<FormattedMessage
    id="app.greeting"
    description='Greeting to Welcome the user to the app'
    defaultMessage='Hello, {name}!'
    values={{
        name: 'Eric'
    }} />
// 最终渲染结果
<span> Hello Eric!</span>
~~~
### react-redux
组件 -> action -> reducer -> state -> 组件
#### store: 就一个作用-》数据分发。 store-> view。把数据给view，展示页面。
主要功能：
1，维护整个应用： state；
2，提供getState()方法获取state;
3，提供dispatch(action)方法更新state;
4，通过subscribe(listener)注册监听器
#### action
action: 提供一些状态函数，store数据就来源于action，需要至少一个type, type是这个指令的唯一标识，其他元素是传递给这个指令的state的值，这个指令有组件触发，然后传递到reducer。
~~~
export const editTodo = (id, text)=>({
    type: types.EDIT_TODO,
    id,
    text
})
export const completeAll=()=>({
    type: types.COMPLETE_ALL
})
~~~
#### reducer
reducer: 如果action申明了要做什么，那么具体区改变（更新）state，就是reducer做的事情。action约定了一个type，然后reducer遇到这个type，就去做一个事。
~~~
export default function todos(state=initialState, action){
    switch(action.type) {
        case ADD_TODO:
            return [
                {
                    id: state.reduce(
                        (maxId, todo)=>Math.max(todo.id, maxId, -1) + 1,
                    ),
                    completed: false,
                    text: action.text
                },
                ...state
            ]
        case DELETE_TODO:
            return state.filter(todo =>
                todo.id !== action.id
            )
        case EDIT_TODO:
            return state.map(todo=>{
                todo.id === action.id ? {...todo,completed: !todo.completed} : todo
            })
        ...
        default:
            return state
    }
}
~~~
