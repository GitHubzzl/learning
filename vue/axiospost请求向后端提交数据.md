# axiospost请求向后端提交数据

Axios向后端提交数据容易接收不到原因是传参方式是request payload,参数格式是json，而并非用的是form传参，所以在后台用接收form数据的方式接收参数就接收不到了。post表单请求提交时，使用的Content-Type是application/x-www-form-urlencoded，而使用原生AJAX的POST请求如果不指

定请求头RequestHeader，默认使用的Content-Type是text/plain;charset=UTF-8。

### 所以采取以下解决办法 

#### 步骤一：

```
安装 qs   : npm install qs --save    

在页面中引用 qs :   var qs = require('qs');

options.data = qs.stringify(data);
```

#### 步骤二：

> 这一步在前端基础工程里已经添加了

同时需要将请求头headers改为： 'Content-Type': 'application/x-www-form-urlencoded'

### 参考文献：

```
https://www.cnblogs.com/wangyawei/p/9006035.html
```



