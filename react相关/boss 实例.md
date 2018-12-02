1, react脚手架
~~~
create-react-app imooc-react-chat
~~~
2, 环境配置
2.1 暴露环境
~~~
yarn eject
# Remove untracked files, stash or commit any changes, and try again.
# 解决方案
# git add .
# git commit -am "Save before ejecting"
~~~
3.2, 安装antd-mobile
~~~
yarn add antd-mobile --save
## 按需加载
yarn add babel-plugin-import --save
// package.json
{
  ...
  "babel":{
    ...
    "plugins":[
      ["import",{libraryName: "antd-mobile",style:"css"}]
    ]
  }
}
~~~
2.3, http请求框架 axios
~~~
yarn add axios --save
// package.json
{
  ...
  "proxy": "http://localhost:9093" // 请求重定向
}


~~~
2.4 cookie
~~~
yarn add cookie-parser --save
~~~
2.5 redux三件套
~~~
yarn add redux --save
yarn add redux-thunk --save
yarn add react-redux --save
yarn add babel-plugin-transform-decorators-legacy --save
// package.json 支持@connect装饰符
{
  ...
  "babel":{
    ...
    "plugins":[
      [
        ...// antd懒加载
      ],
      ["@babel/plugin-proposal-decorators", { "legacy": true }]
    ]
   }
}
~~~
