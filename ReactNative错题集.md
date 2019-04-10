### ``React Native version mismatch``
出现这个bug会有两个情况
#### 1，有其他不同版本的RN工程以开发模式运行，这时我们只需关闭产生冲突的命令行窗口，问题就解决了
#### 2，在Android/iOS工程中配置的RN库版本与JS工程中配置的RN库版本不一致也会导致这个问题，这种情况下，只需将android/app/build.gradle下的RN库默认配置如下修改 
~~~
...
  // 配置前
  compile 'com.facebook.react:react-native:+'
  // 配置后
  compile ('com.facebook.react:react-native:0.54.3'){force = true}
...
~~~
