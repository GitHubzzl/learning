# MongoDB4.0 在 windows 下的安装

1.下载地址： <https://www.mongodb.com/download-center#community>

2.在安装目录 data 文件夹下创建 新的文件夹 db(我的目录：E:\MongoDB\data\db)，在 log 文件夹下创建新文件 mongo.log(E:\MongoDB\log\mongo.log)

3.打开命令行，cd 到安装目录的 bin 文件夹下（或者在改目录下，在地址栏输入cmd），在cmd中输入命令 mongod –dbpath E:\MongoDB\data\db ，出现如下图，即成功。

主要参考：

https://blog.csdn.net/ztx114/article/details/78326573

https://blog.csdn.net/dorma_bin/article/details/80851230





