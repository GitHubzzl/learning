# 设置npm全局路径

nodejs下载安装完成后

```
npm config ls 或者 npm config list
```

可查看全局路径：prefix = "C:\\Program Files\\nodejs\\node_modules\\npm\\node_modules"

npm 默认的全局安装路径为该路径，将包都下载在C盘中不是我们想要的结果。一般建议修改在nodejs的安装目录下的node_modules中

输入以下命令重新修改全局路径：

```
npm config set prefix "C:\Users\admin\AppData\Roaming\npm"   //  正确

npm config set prefix "C:\\Program Files\\nodejs\\node_modules\\npm"  // 错误
```

