# React全家桶后台管理框架-学习笔记

```
https://github.com/yezihaohao/react-admin
```



### 2019/12/12 学习react第1天

#### 开发笔记：

```
npm i antd
npm i react-document-title
```



import SiderCustom from './components/suder-custom.jsx'; 写成了 import SiderCustom from './components/suder-custom';   **没有写 .jsx** 报错；

误删了src/serviceWorker.js  报错，调试错误两小时

#### 完成进度：

1.初始化工程 first-blood

2.完成了Footer

#### 晚上学习计划：

- redux

- antd

- react-router

- react-redux   （http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_three_react-redux.html）

------



### 2019/12/13 学习react第2天

#### 开发笔记：

1.完成了App.js中模块结构拆分



------



### 2019/12/14 学习react第3天

#### 开发笔记：

```
npm install redux --S

npm install react-redux --S

参考链接：https://segmentfault.com/a/1190000015684895#articleHeader1
```

1.Provider：它是react-redux 提供的一个 React 组件，作用是把state传给它的所有子组件，也就是说 当你用Provider传入数据后 ，下面的所有子组件都可以共享数据，十分的方便。使用：把Provider组件包裹在最外层的组件。

2.connect：四个参数([mapStateToProps], [mapDispatchToProps], [mergeProps], [options])，connect的使用方法是：把指定的state和指定的action与React组件连接起来，后面括号里面写UI组件名。

































