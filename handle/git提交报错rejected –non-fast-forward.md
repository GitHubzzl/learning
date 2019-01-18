# git提交报错rejected –non-fast-forward



## 1）错误原因

文件冲突，本地的代码和远程Repository中的文件个数不一致（即远程Repository中存在本地项目中不存在的文件）或本地得项目不是在远程Repository代码的基础上修改的。



## 2）解决方案

```javascript
git pull origin master –allow-unrelated-histories 
git push -u origin master -f
```

