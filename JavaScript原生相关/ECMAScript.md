### Es5  扩展了Object,  Array, Function等功能
### Es6  
> 类，
~~~
class Animal{
  constructor(name,color){
    this.name = name;
    this.color = color;
  }
  toString(){
    console.log('name: '+this.name+',color: '+this.color)
  }
}
var  animal  = new Animal('dog', 'white');
animal.toString();
// obj.hasOwnProperty(prop)    判断某个对象是否含有指定的属性
// prop 字符串 或 Symbol 
animal.hasOwnProperty('name'); // true
animal.hasOwnProperty('toString'); // false
animal.__proto__.hasOwnProperty('toString');  // true

class Cat extends Animal {
  constructor(action){
    super('cat', 'white');
    this.action  = action;
  }
  toString(){
    console.log(super.toString());
  }
}
var cat = new Cat('catch');
cat.toString();

cat instanceof Cat; // true
cat instanceof Animal; // true


~~~

> 模块化，
~~~
export classname
import classname from ...
// 一条import语句可以同时导入默认函数和其他变量
// import defaultMethod, {otherMethod} from 'xxx.js';

~~~
> 箭头函数，
~~~
// 每一次.bind(this)，都是产生一个新的函数
// RN卸载监听器
class PauseMenu extends React.Component{
  constructor(props){
    super(props);
    this._onAppPaused = this.onAppPaused.bind(this);
  }
  componentWillMount(){
    AppStateIOS.addEventListener('change',this._onAppPaused);
  }
  componentWillUnmount(){
    AppStateIOS.removeEventListener('change', this._onAppPaused);
  }
  onAppPaused(event){
  }
}
~~~
> 函数参数默认值
> 模板字符串
> 解构赋值
~~~
var a,b =  [3,4]
[b,a] = [a,b]
~~~
> 延展操作符
~~~
function sum(x,y,z){
  return x+y+z;
}
const numbers = [1,2,3];
sum.apply(null, numbers);
sum(...number)
// tip  伪数组转真数组   Array.prototype.push.apply(arr01,[])
~~~
> 对象属性简写
> Promise
~~~
var waitSencond  =  new Promise(function(resolve,reject){
  setTimeout(resolve, 1000)
})
waitSencond
  .then(
    function(){
      console.log('hello'); // 1s后输出'Hello'
      return waitSecond;
    }
  )
  .then(
    function(){
      console.log('hi'); // 2s后输出'hi'
    }
   )
~~~
> Let与Const
### Es7  
> includes，
~~~
arr.includes(x) // includes函数用来判断数组里是否包含一个指定的值 包含为 true, 否则为 false
arr.includes(x) === arr.indexOf(x)>=0
~~~
> 指数操作符
~~~
** === Math.pow()
~~~
### Es8  
> aync/await, 
~~~
login(userName){
  return new Promise((resolve, reject)=>{
    setTimeout(()=>{
      resolve('1001')
    },2000)
  })
}
getData(userId){
  return new Promise((resolve, reject)=>{
    setTimeout(()=>{
      userId==='1001'? resolve('success'): reject('fail')
    },2000)
  })
}
// 不使用async/await
doLogin(userName){
  this.login(username)
    .then(this.getData)
    .then(result=>{
      console.log(result);
    })
}
// 使用async/await
async doLogin01(username){
  const userId = await this.login(username)
                  .catch(console.log); // 捕捉单个错误  try {} catch(e){}
  const result = await this.login(userId);
  console.log(result)
}
doLogin01('name').catch(console.log)
// Promise.all 并发执行
async function charCountAdd(data1, data2){
  const [a,b] = await Promise.all([login(data1),login(data2)])
  return a+b
}
~~~
> Object.values(),
~~~
const obj = {a:1,b:2,c:3};
const vals = Object.keys(obj).map(v=>obj[v]); [1,2,3]
===
const vals = Object.values(obj); [1,2,3]
~~~
> Object.entries(),
~~~
for(let [key,value] of Object.entries(obj1)){
  console.log(`key: ${key}, value: ${value}`)
}
~~~
> String padding
> 函数参数列表结尾容许逗号
> Object.getOwnPropertyDescriptors()
