## createStackNavigator提供转场过度效果，android从屏幕底部淡入，ios从屏幕右侧划入
### api
``createStackNavigator(RouterConfigs,StackNavigatorConfig)``
· RouteConfigs: 告诉导航器，该路由呈现什么 
· StackNavigatorConfig: 配置导航器路由样式
~~~
└── navigators/AppNavigators.js
├── page
│   ├── HomePage.js
│   ├── Login.js
│   ├── Page1.js
│   ├── Page2.js
│   ├── Page3.js
│   ├── Page4.js
│   └── Page5.js
├── index.js
└── yarn.lock
~~~
### ``AppNavigators.js``
~~~
import { createStackNavigator } from 'react-navigation';
import React from 'react'
import { Button } from 'react-native'

import HomePage from '../page/HomePage';
import Page1 from '../page/Page1';
import Page2 from '../page/Page2';
import Page3 from '../page/Page3';
import Page4 from '../page/Page4';
import Page5 from '../page/Page5';


export const AppStackNavigator = createStackNavigator({
    HomePage: {
        screen: HomePage
    },
    Page1: {
        screen: Page1,
        navigationOptions: ({ navigation }) => ({
            title: `${navigation.state.params.name}页面名`
        })
    },
    Page2: {
        screen: Page2,
        navigationOptions: {
            // 静态配置
            title: 'this is page02'
        }
    },
    Page3: {
        screen: Page3,
        navigationOptions: (props) => {
            const { navigation } = props;
            const { state, setParams } = navigation;
            const { params } = state;
            return {
                title: params.title ? params.title : 'page3',
                headerRight: (
                    <Button
                        title={params.mode === 'edit' ? '保存' : '编辑'}
                        onPress={() => setParams({ mode: params.mode === 'edit' ? '' : 'edit' })}
                    />
                )
            }
        }
    },
    Page4: {
        screen: Page4,
        navigationOptions: {
            // 静态配置
            title: 'this is page02'
        }
    },
})
~~~
### ``index.js``
~~~
import { AppRegistry } from 'react-native';
import { createAppContainer } from 'react-navigation'
import { AppStackNavigator } from './navigators/AppNavigators';
import { name as appName } from './app.json';
const AppStackNavigatorContainer = createAppContainer(AppStackNavigator);
AppRegistry.registerComponent(appName, () => AppStackNavigatorContainer);
~~~
### ``HomePage.js``
~~~
import React, { Component } from 'react';
import { Button, StyleSheet, Text, View } from 'react-native';

type Props = {};
export default class HomePage extends Component<Props> {
  static navigationOptions = {
    title: 'Home',
    headerBackTitle: '返回123'
  }
  render() {
    const { navigation } = this.props;
    return (
      <View style={styles.container}>
        <Button 
          title="go to page1"
           onPress={()=>{
             navigation.navigate('Page1', {name:'动态的'})
           }}
        />
        <Button 
          title="go to page2"
           onPress={()=>{
             navigation.navigate('Page2')
           }}
        />
        <Button 
          title="go to page3"
           onPress={()=>{
             navigation.navigate('Page3', {name:'Devio'})
           }}
        />
        <Text style={styles.welcome}>Welcome to HomePage!</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
});
~~~
