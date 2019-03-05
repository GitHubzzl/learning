# Windows 10 安装 node-sass 提示需要安装 Visual C++ 2015 Build Tools 的解决方案

通常，如果我们的项目依赖 [node-sass](https://github.com/sass/node-sass) ，默认执行 npm install  命令时，将会从互联网上下载其 C++ [源代码](https://www.baidu.com/s?wd=%E6%BA%90%E4%BB%A3%E7%A0%81&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd)进行编译。[Windows](https://www.baidu.com/s?wd=Windows&tn=24004469_oem_dg&rsv_dl=gh_pl_sl_csd) 系统下，我们需要下载安装 [Visual C++ 2015 Build Tools](http://landinghub.visualstudio.com/visual-cpp-build-tools) 来完成编译。安装过程虽然很简单，但是该程序需要占用大约 7G 的存储空间，这对于仅仅是想使用 node-sass 的人来说是非常不实用的。本文将介绍如何更加方便的在 Windows 环境下安装 node-sass 组件。

对于需要编译的情况，我们可以选择直接使用编译好的 node-sass 二进制文件，为了在国内也有良好的体验，使用 cnpm 作为镜像源。最终，我们只需要在项目根目录执行以下命令

```
npm install --save node-sass --registry=https://registry.npm.taobao.org --disturl=https://npm.taobao.org/dist --sass-binary-site=http://npm.taobao.org/mirrors/node-sass
```



参考：https://blog.csdn.net/tang05709/article/details/81253735