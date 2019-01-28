## Express 是一个简洁灵活的nodejs web框架。
### 核心特性
> 可以设置中间件来响应HTTTP请求。
> 定义路由表，用于执行不同的HTTP请求动作。
> 可以通过模板传递参数来动态渲染HTML页面。
## 安装express
~~~
npm install express --save
// 查看版本号
npm list express
~~~
#### 常用的中间件
* body-parser  -nodejs中间件，用于处理JSON,Raw,Text和URL编码的数据
* cookie-parser 解析cookie的工具，通过req.cookies可以取到传过来的cookie，并把他们转为对象
* multer -nodejs中间件，用于处理enctype="multipart/form-data"(设置表单的mime编码)的表单数据 
~~~

~~~

~~~
const express = require('express');
const app = express();
app.get('/',function(req,res){
  res.send('<h1>水电费是的发送到</h1>')
})
app.listen(9093,function(){
  console.log('Node app start at port 9093')
})
~~~
###### app.get、app.post分开开发get post接口
###### app.use 使用模块
###### body-parser、cookie-parser整理数据结构和获取权限
~~~
const express = require('express')
const bodyParser = require('body-parser');
const cookieParser = require('cookie-parser);
const app = express()
app.use(cookieParser());
app.use(bodyParser.json());
~~~
#### 数据库
##### mysql
##### mongodb

