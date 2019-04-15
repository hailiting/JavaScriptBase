### ``react-navigation``导航组件
在``react-navigation``中有以下七种类型的导航器
> createStackNavigator: 类似于普通的Navigator，屏幕上方导航栏；
> createBottomTabNavigator: 相当于IOS里的TabBarController,屏幕下方的标签栏；
> createDrawerNavigator: 抽屉效果，侧边滑出；
> createSwitchNavigator: SwitchNavigator 的用途是一次只显示一个页面；

· Screen navigation prop - 屏幕导航属性：通过navigation完成屏幕间的调度操作，例如打开另一个屏幕；
· Screen navigationOptions - 屏幕导航选项：通过navigationOptions可以定制导航器显示屏幕的方式，例如：头部标题，选项卡标签等；

#### 导航器所支持的``Props``
~~~
const SomeNav = createStackNavigator/createBottomTabNavigator/createMaterialTopNavigator({
  // config
})
<SomeNav
  screenProps={xxx}
  ref={nav=>{navigation:nav;}}
  onNavigationStateChange=(prevState, newState, action)=>{
  }
/>
~~~
###### 1，``screenProps``向子屏幕传递额外的数据，子屏幕可以通过``this.props.screenProps``获取到该数据;
###### 2，``ref``=>获取到``navigation``;
###### 3，``onNavigationStateChange(prevState, newState, action)``
