### 1,  ``React Native version mismatch``
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
### 2, 发现安卓真机版本与实际版本不一样
~~~
adb kill-server
adb start-server
adb reverse tcp:8081 tcp:8081
npm start
~~~
### 3, 嵌套ScrollView解决方案
~~~
import React, { Component } from 'react';
import { View, ScrollView } from 'react-native';

export default class App extends Component {
  constructor() {
    super();
    this.state = {
       enabled:true
    };
  }
  
  render() {
  return (
    <ScrollView scrollEnabled={this.state.enabled}>
      <View style={ {height:600,backgroundColor:'violet'}}></View>
      <View style={ { height: 2000, backgroundColor: 'red' }} >
      <ScrollView
        onTouchStart={(ev) => {this.setState({enabled:false }); }}
        onMomentumScrollEnd={(e) => { this.setState({ enabled:true }); }}
        onScrollEndDrag={(e) => { this.setState({ enabled:true }); }}
        style={ { margin: 10, maxHeight: 200 }}
    >
        <View style={ { height: 200, backgroundColor: 'blue' }} />
        <View style={ { height: 200, backgroundColor: 'pink' }} />
         <View style={ { height: 200, backgroundColor: 'blue' }} />
        <View style={ { height: 200, backgroundColor: 'pink' }} />
        <View style={ { height: 200, backgroundColor: 'blue' }} />
        <View style={ { height: 200, backgroundColor: 'pink' }} />
        <View style={ { height: 200, backgroundColor: 'blue' }} />
        <View style={ { height: 200, backgroundColor: 'pink' }} />
        <View style={ { height: 200, backgroundColor: 'blue' }} />
        <View style={ { height: 200, backgroundColor: 'pink' }} />
        <View style={ { height: 200, backgroundColor: 'blue' }} />
        <View style={ { height: 200, backgroundColor: 'pink' }} />
      </ScrollView>
      </View>
    </ScrollView>
  );
}
}
~~~
