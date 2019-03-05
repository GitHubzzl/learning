# git提交报错



## 1.rejected –non-fast-forward

### 1）错误原因

文件冲突，本地的代码和远程Repository中的文件个数不一致（即远程Repository中存在本地项目中不存在的文件）或本地得项目不是在远程Repository代码的基础上修改的。



### 2）解决方案

```javascript
git pull origin master –allow-unrelated-histories 
git push -u origin master -f
```



## 2.账户密码修改过无法认证成功

![1548664362861](C:\Users\admin\AppData\Roaming\Typora\typora-user-images\1548664362861.png)



## 3.关于git push 后出现remote: HTTP Basic: Access denied等相关报错问题

如果是公司git的项目，用户名是不带邮箱后缀