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
