## 启动mongod
### mongod --config /usr/local/etc/mongod.conf
### mongo
--  mongodb://127.0.0.1:27017 mongodb默认端口

## 常见错误
~~~
2019-01-14T11:35:18.234+0800 I CONTROL  [main] Automatically disabling TLS 1.0, to force-enable TLS 1.0 specify --sslDisabledProtocols 'none'
2019-01-14T11:35:18.269+0800 I CONTROL  [initandlisten] MongoDB starting : pid=47187 port=27017 dbpath=/data/db/ 64-bit host=hailitingdeMBP
2019-01-14T11:35:18.269+0800 I CONTROL  [initandlisten] db version v4.0.5
2019-01-14T11:35:18.269+0800 I CONTROL  [initandlisten] git version: 3739429dd92b92d1b0ab120911a23d50bf03c412
2019-01-14T11:35:18.269+0800 I CONTROL  [initandlisten] allocator: system
2019-01-14T11:35:18.269+0800 I CONTROL  [initandlisten] modules: none
2019-01-14T11:35:18.269+0800 I CONTROL  [initandlisten] build environment:
2019-01-14T11:35:18.269+0800 I CONTROL  [initandlisten]     distarch: x86_64
2019-01-14T11:35:18.269+0800 I CONTROL  [initandlisten]     target_arch: x86_64
2019-01-14T11:35:18.269+0800 I CONTROL  [initandlisten] options: { storage: { dbPath: "/data/db/" } }
2019-01-14T11:35:18.273+0800 I STORAGE  [initandlisten] exception in initAndListen: NonExistentPath: Data directory /data/db/ not found., terminating
2019-01-14T11:35:18.273+0800 I NETWORK  [initandlisten] shutdown: going to close listening sockets...
2019-01-14T11:35:18.273+0800 I NETWORK  [initandlisten] removing socket file: /tmp/mongodb-27017.sock
2019-01-14T11:35:18.273+0800 I CONTROL  [initandlisten] now exiting
2019-01-14T11:35:18.274+0800 I CONTROL  [initandlisten] shutting down with code:100
~~~
### 原因分析：
mongo非正常关闭导致
#### 解决方法
在bin目录下新建./data/ 和./log/文件夹，进入log文件夹，vim mongodb.log
到bin下
~~~
./mongod --dbpath ./data/
~~~
~~~
./mongo
~~~

## 下载，安装，启动mongodb
~~~
brew updata
brew install mongodb
// 启动mongodb
mongod --config /user/local/etc/mongod.conf
// 连接mongodb service
mongo
~~~

### 常用命令
~~~
// 查看所有
show dbs
// 创建数据库
use data_parson_info
// 查看当前数据库
db
~~~





## node链接 mongodb
~~~
const  DB_URL = 'mongodb://localhost:27017';
mongoose.connect(DB_URL);
mongoose.connection.on('connected',function(){
    console.log('mongo connect success');
})
~~~
## mongoose使用
### connect链接数据库
### 定义文档模型，Schema和model新建模型
~~~
const User = mongoose.model('user', new mongoose.Schema({
  user:  {type: String, require:  true},
  age: {type:Number, require: true}
}))
~~~
### 代一个数据库文档对应一个模型，通过模型对数据库 进行操作
  增删改查 
    find,findOne 查找数据 
    updata  更新数据
    Remove 删除数据
~~~
// 新增数据
User.create({
    user: 'hai',
    age: 13
},function(err, doc){
    if(!err){
        console.log(doc)
    }else{
        console.log(err)
    }
})
// 删
User.remove({
    user:'hai'
},function(err,doc){
    if(!err){
        console.log('delete success')
        User.find({},function(e,d){
            console.log(d)
        })
    }
})
// 改 
User.update({'user':'imooc'},{'$set':{age:26}},function(err,doc){
    console.log(doc)
})
// 查找数据
app.get('/data', function(req,res){
    User.find({},function(err,doc){
        res.json(doc)
    })
})
User.find({user:'xiaoming'},function(err,doc){
    res.json(doc)
})
User.findOne({user:'xiaoming'},function(err,doc){
    res.json(doc)
})
~~~
