# vue中使用less

> 首先vue开发环境已经安装成功

当所有东西都 准备好之后 ：

#### 第一步：

安装less依赖，`npm install less less-loader --save`

#### 第二步：

修改webpack.config.js文件，配置loader加载依赖，让其支持外部的less,在原来的代码上添加

```javascript
{
	test: /\.less$/,
	loader: "style-loader!css-loader!less-loader",
},
```

现在基本上已经安装完成了，然后在使用的时候在style标签里加上lang=”less”里面就可以写less的代码了(style标签里加上 scoped 为只在此作用域 有效)

```
<style lang="less" scoped>
@import './index.less'; //引入全局less文件

</style>

