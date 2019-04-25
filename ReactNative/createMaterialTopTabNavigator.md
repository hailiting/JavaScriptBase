
~~~
yarn add react-native-vector-icons
react-native link react-native-vector-icons
~~~
## ``createBottomTabNavigator``
## ``createMaterialTopTabNavigator(RouteConfigs, TabNavigatorConfig)``
~~~
title: 可以用做headerTitle和tabBarLabel的备选通用标题
swipeEnabled: 是否容许tab之间的滑动切换，默认容许
tabBarIcon:设置TabBar图标
tabBarLabel: 设置tabbar标签 
tabBarOnPress: Tab被点击的回调函数，（navigation, defaultHandler）
tabBarTTestID: 用于在测试中找到该选项卡按钮的ID;
~~~
#### ``TabNavigatorConfig``
~~~
tabBarOptions: {
  labelStyle: {
    fontSize: 12,
  },
  tabStyle: {
    width: 100,
  },
  style: {
    backgroundColor: 'blue',
  }
}
~~~
