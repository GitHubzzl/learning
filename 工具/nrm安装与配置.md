# nrm安装与配置

### 1.什么是nrm

nrm 是一个 npm 源管理器，允许你快速地在 npm 源间切换。

### 2.安装nrm

在命令行执行命令，npm install -g nrm，全局安装nrm。

### 3.使用

执行命令nrm ls查看可选的源。

```javascript
nrm ls                                                                                                                                    
*npm --- https://registry.npmjs.org/
cnpm --- http://r.cnpmjs.org/
taobao - http://registry.npm.taobao.org/
eu ----- http://registry.npmjs.eu/
au ----- http://registry.npmjs.org.au/
sl ----- http://npm.strongloop.com/
nj ----- https://registry.nodejitsu.com/
```



其中，带*的是当前使用的源，上面的输出表明当前源是官方源。

### 4.切换

如果要切换到taobao源，执行命令nrm use  <registry>。

```javascript
nrm use taobao
```

### 5.增加

你可以增加定制的源，特别适用于添加企业内部的私有源，执行命令 nrm add <registry> <url>，其中reigstry为源名，url为源的路径。

```javascript
nrm add registry http://192.168.10.127:8081/repository/npm-public/
```

### 6.删除

执行命令nrm del <registry> 删除对应的源。

```javascript
nrm use taobao
```

###　7.测试速度
你还可以通过 nrm test 测试相应源的响应时间。

```javascript
nrm test npm                                                                           

npm ---- 1328ms
```



​		