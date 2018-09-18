# 一， 如果解决nodejs回调黑洞或回调金字塔这个问题
Async, Promise, Generator
要求：
找出某个目录最大文件
~~~
var findLargest = require('./findLargest')
findLargest('./path/to/dir',function(er,filename){
  if(er) return console.error(er)
  console.log('largest file was:',filename)
})
~~~
1,嵌套代码
~~~
var fs=require('fs')
var path=require('path')
module.exports=function(dir,cb){
  fs.readdir(dir,function(er,files){ [1]
    if(er) return cb(er)
    var counter = files.length
    var errored = false
    var stats=[]
    files.forEach(function(file,index){
      fs.stat(path.join(dir,file),function(er,stat){  [2]
        if(errored) return 
        if(er){
          errored=true
          return cb(er)
        }
        stats[index] = stat [3]
        if(--counter == 0){  [4]
          var largest = stats
            .filter(function(stat){
              return stat.isFile()  [5]
            })
            .reduce(function(prev,next){  [6]
              if(prev.size > next.size) return prev
              return next
            })
            cb(null,files[stats.indexOf(largest)])  [7]
        }
      })
    })
  })
}
~~~
2, Promise
Promise提供了错误处理和函数式编程
Q模块（promise类库）
~~~
var fs = require('fs')
var path = require('path')
var Q = require('q')
var fs_readdir = Q.denodeify(fs.readdir)[1]
var fs_stat = Q.denodeify(fs.stat)
module.exports = function(dir){
  return fs_readdir(dir)
    .then(function(files){
      var promises = files.map(function(file){
        return fs_stat(path.join(dir,file))
      })
      return Q.all(promise).then(function(stats){
        return [files, stats]
      })
    })
    .then(function(data){
      var files = data[0]
      var stats = data[1]
      var largest = stats
                    .filter(function(stat){
                      return stat.isFile()
                    })
                    .reduce(function(prev,next){
                      if(prev.size>next.size) return prev
                      return next
                    })
                    return files[stats.indexOf(largest)]
    })
}
~~~
3, Generator 类库（co）
Generator特别的语法funcion*()，通过这种超能力，可以控制或继续执行异步操作
~~~
var co = require('co')
var thunkify = require('thunkify')
var fs = require('fs')
var path = require('path')
var readdir = thunkify(fs.readdir)
var stat = thunkify(fs.stat)
module.exports = co(
  function* (dir){
    var files = yield readdir(dir)
    var stats = yield files.map(function(file){
      return stat(path.join(dir,file))
    })
    var largest = stats
                  .filter(function (stat){return stat.isFile})
                  .reduce(function(prev,next){
                    if(prev.size>next.size) return prev
                    return next
                  })
    return files[stats.indexOf(largest)]
  }
)
~~~

~~~
try{}catch(er){}
~~~
