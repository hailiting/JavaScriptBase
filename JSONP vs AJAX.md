## JSONP产生的背景

    1，ajax请求存在跨域问题（无论是静态页面，还是动态网页，web服务，WCF...只要是跨域，一律不准）
    2，web页面调用js文件时不受跨域影响（包含src这个属性的，都拥有跨域能力，比如script,img,iframe）
    3，如果web端想跨域访问数据，只有在远程服务器上设法把数据装进js格式的文件里，供客户端调用和进一步处理
    4，在我们已经知道的数据格式里，json（纯字符数据格式）最符合要求。
      4.1，纯字符数据格式可以简洁的描述复杂的数据；
      4.2，被js原生支持
    5，所以跨域的解决方案之一就是，web客户端通过调用脚本一模一样的方式，来调用跨域服务器上动态生成的js格式文件（一般以json为后缀），
    这样=>服务器生成动态json,客户端获取动态数据。
    6，这样的方式渐渐形成一种非正式传输协议，人们称它为jsonp。
      jsonp的一个要点是容许用户传递一个callback参数给服务端，然后服务端返回数据时会将这个callback参数作为函数名来包裹json数据，
      这样客户端就可以随意定制自己的函数来实现自动处理返回发数据。

## jsonp客户端的具体实现
#### 1：远程服务器（remoteserver.com）上有一个remote.js文件
~~~
alert('我是远程文件！')
~~~
#### 2，本地服务器（localserver.com）上一个jsonp.html页面
~~~
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title></title>
    // 会调用成功
    // 
    <script type="text/javascript" src="http://remoteserver.com/remote.js"></script>
</head>
<body>
</body>
</html>
~~~
#### 3，在jsonp.html定义一个函数，然后远程传入数据进行调用
~~~
// remote.js
localHandler({'result':'bababa...'})
// jsonp.html
<html xmlns="http://www.w3.org/1999/xhtml"></html>
<head></head>
<script>
    var localHandler = function(data){
        console.log('i am local function,used by long removejs,data:'+ data.result)
    }
</script>
<script src="http://192.168.1.196/remove.js"></script>
~~~
#### 4，告诉远程js知道他应该调用本地的哪一个函数=》动态生成js脚本
~~~
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title></title>
    <script type="text/javascript">
        var flightHandler = function(data){
            alert(data.result)
        }
        // 服务器就会根据传过来的参数动态生成页面所需要的数据
        var url = "http://192.168.1.196/remove.aspx?code=asdf&&callback=weee"
        var script = document.createElement('script');
        script.setAttribute('src',url);
        document.getElementsByTagName('head')[0].appendChild(script)
    </script>
</head>
~~~

## JSONP和AJAX相同点与不同点
  #### 相同点
        使用方法和目的都一样，都是请求一个url，然后把服务器返回的数据进行处理，因此jQuery和ext等框架都把jsonp作为ajax的一种形式进行封装。
  #### 不同点：
        jsonp不是ajax的特例，jsonp是一种方式或者说是非强制性协议
        ajax的核心是通过XmlHttpRequest获取非本页内容，而jsonp的核心是动态添加script标签来调用服务器提供js脚本
        ajax和jsonp的区别不在于是否跨域，ajax通过服务端代理一样可以实现跨域，jsonp本身也不排斥同域的数据的获取
        
