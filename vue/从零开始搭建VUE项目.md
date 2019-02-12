#　从零开始搭建VUE项目



## 环境安装和初始化工程

```
$ npm install -g vue-cli
$ vue init webpack my-project
$ cd my-project
$ npm install
$ npm run dev
```



## 安装 less

> 首先vue开发环境已经安装成功

当所有东西都 准备好之后 ：

**第一步：**

安装less依赖，`npm install less less-loader --save`

**第二步：**

修改webpack.config.js文件，配置loader加载依赖，让其支持外部的less,在原来的代码上添加

```javascript
{
	test: /\.less$/,
	loader: "style-loader!css-loader!less-loader",
},
```

现在基本上已经安装完成了，然后在使用的时候在style标签里加上lang=”less”里面就可以写less的代码了(style标签里加上 scoped 为只在此作用域 有效)

**第三步：**

在Vue-cli2.x的时候 给loader加配置项是方式是这样的

```javascript
{ loader: 'less-loader', options: { javascriptEnabled: true } }
```

在Vue-Cli3.0中需要这样写vue.config.js：

```javascript
module.exports = {
  css: {
    loaderOptions: { // 向 CSS 相关的 loader 传递选项
      less: {
        javascriptEnabled: true
      }
    }
  }
}

```

这样配置解决：使用iView自定义主题运行项目时报错 Inline JavaScript is not enabled. Is it set in your options

main.js中引入less文件报错，解决方案：

```
import '!style-loader!css-loader!less-loader!@/assets/css/base.less'
```



## 安装  vuex

```
npm install vuex --save
```



## 安装 iView

```
npm install iview --save
```



## 安装 js-cookie

```
npm i js-cookie
```



## 安装axios

```
npm install axios
```

