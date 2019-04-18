## 模拟器调出开发者菜单
### IOS 
~~~
command || Ctrl + D
~~~
### Android 
~~~
command || Ctrl + M
~~~
## 真机上
摇一摇
## 开发者菜单结构
~~~
》 Reload => 重新加载JS代码
》 Debug JS Remotaly
》 Enable Live Reload  => 持续加载，整个热更新
》 Start Systrace
》 Enable Hot Reloading  => 热加载，仅更新当前页面
》 Toggle Inspector
》 Show Pert Monitor
》 Cancel
~~~
## warnings
### 1，手动触发  ``console.warn()``
### 2，``console.disableYellowBox = true`` 手动禁止warnings
### 3，``console.ignoredYellowBox = ['Warning: ...'];``来忽略相应的Warnin
