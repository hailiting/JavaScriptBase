## mongod --config /usr/local/etc/mongod.conf
## mongo
--  mongodb://127.0.0.1:27017 mongodb默认端口
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
