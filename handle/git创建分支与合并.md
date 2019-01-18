# git创建与合并分支

在版本回退里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即`master`分支。`HEAD`严格来说不是指向提交，而是指向`master`，`master`才是指向提交的，所以，`HEAD`指向的就是当前分支。

一开始的时候，`master`分支是一条线，Git用`master`指向最新的提交，再用`HEAD`指向`master`，就能确定当前分支，以及当前分支的提交点：

![img](https://images2015.cnblogs.com/blog/925240/201604/925240-20160423170116366-1271622497.png)

每次提交，`master`分支都会向前移动一步，这样，随着你不断提交，`master`分支的线也越来越长：

![img](https://images2015.cnblogs.com/blog/925240/201604/925240-20160423171754726-1548159783.png)

当我们创建新的分支，例如`dev`时，Git新建了一个指针叫`dev`，指向`master`相同的提交，再把`HEAD`指向`dev`，就表示当前分支在`dev`上：

![img](https://images2015.cnblogs.com/blog/925240/201604/925240-20160423171901538-103030485.png)

你看，Git创建一个分支很快，因为除了增加一个`dev`指针，改改`HEAD`的指向，工作区的文件都没有任何变化！

不过，从现在开始，对工作区的修改和提交就是针对`dev`分支了，比如新提交一次后，`dev`指针往前移动一步，而`master`指针不变：

![img](https://images2015.cnblogs.com/blog/925240/201604/925240-20160423172106413-2099839645.png)

假如我们在`dev`上的工作完成了，就可以把`dev`合并到`master`上。Git怎么合并呢？最简单的方法，就是直接把`master`指向`dev`的当前提交，就完成了合并：

![img](https://images2015.cnblogs.com/blog/925240/201604/925240-20160423172212929-611975577.png)

所以Git合并分支也很快！就改改指针，工作区内容也不变！

合并完分支后，甚至可以删除`dev`分支。删除`dev`分支就是把`dev`指针给删掉，删掉后，我们就剩下了一条`master`分支：

![img](https://images2015.cnblogs.com/blog/925240/201604/925240-20160423172333538-1672105116.png)

真是太神奇了，你看得出来有些提交是通过分支完成的吗？

![img](https://images2015.cnblogs.com/blog/925240/201604/925240-20160423174934679-1613515273.png)

![img](https://images2015.cnblogs.com/blog/925240/201604/925240-20160423175949741-1234972520.png)

下面开始实战。

首先，我们创建`dev`分支，然后切换到`dev`分支：

```
$ git checkout -b dev
Switched to a new branch 'dev'
```

`git checkout`命令加上`-b`参数表示创建并切换，相当于以下两条命令：

```
$ git branch dev
$ git checkout dev
Switched to branch 'dev'
```

然后，用`git branch`命令查看当前分支：

```
$ git branch
* dev
  master
```

`git branch`命令会列出所有分支，当前分支前面会标一个`*`号。

然后，我们就可以在`dev`分支上正常提交，比如对readme.txt做个修改，加上一行：

```
create new branch dev..
```

然后提交：

```
$ git add readme.txt
$ git commit -m "create new branch...."
[dev 45ae9a9] create new branch....
 1 file changed, 1 insertion(+)
```

现在，`dev`分支的工作完成，我们就可以切换回`master`分支：

```
$ git checkout master
Switched to branch 'master'
Your branch is up-to-date with 'origin/master'.
```

切换回`master`分支后，再查看一个readme.txt文件，刚才添加的内容不见了！因为那个提交是在`dev`分支上，而`master`分支此刻的提交点并没有变：

![img](https://images2015.cnblogs.com/blog/925240/201604/925240-20160423181854210-135268393.png)

现在，我们把`dev`分支的工作成果合并到`master`分支上：

```
$ git merge dev
Updating 90bc1f7..45ae9a9
Fast-forward
 readme.txt | 1 +
 1 file changed, 1 insertion(+)
```

`git merge`命令用于合并指定分支到当前分支。合并后，再查看readme.txt的内容，就可以看到，和`dev`分支的最新提交是完全一样的。

注意到上面的`Fast-forward`信息，Git告诉我们，这次合并是“快进模式”，也就是直接把`master`指向`dev`的当前提交，所以合并速度非常快。

当然，也不是每次合并都能`Fast-forward`，我们后面会讲其他方式的合并。

合并完成后，就可以放心地删除`dev`分支了：

```
$ git branch -d dev
Deleted branch dev (was 45ae9a9).
```

删除后，查看`branch`，就只剩下`master`分支了：

```
$ git branch
* master
```

因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在`master`分支上工作效果是一样的，但过程更安全。

### 小结

Git鼓励大量使用分支：

查看分支：`git branch`

创建分支：`git branch <name>`

切换分支：`git checkout <name>`

创建+切换分支：`git checkout -b <name>`

合并某分支到当前分支：`git merge <name>`

删除分支：`git branch -d <name>`

#### 解决冲突

人生不如意之事十之八九，合并分支往往也不是一帆风顺的。

准备新的`feature1`分支，继续我们的新分支开发：

```
$ git checkout -b feature1
Switched to a new branch 'feature1'
```

 

修改readme.txt最后一行，改为：

```
create new branch feature1..
```

 

在`feature1`分支上提交：

```
$ git add readme.txt
$ git commit -m "create new branch feature1 first modify"
[feature1 b4309b0] create new branch feature1 first modify
 1 file changed, 1 insertion(+)
```

切换到`master`分支：

```
$ git checkout master
Switched to branch 'master'
Your branch is ahead of 'origin/master' by 1 commit.
  (use "git push" to publish your local commits)
```

Git还会自动提示我们当前`master`分支比远程的`master`分支要超前1个提交。

在`master`分支上把readme.txt文件的最后一行改为：

```
goback master....
```

提交：

```
$ git add readme.txt
$ git commit -m "goback master first modify"
[master 0b56936] goback master first modify
 1 file changed, 1 insertion(+)
```

现在，`master`分支和`feature1`分支各自都分别有新的提交，变成了这样：

![img](https://images2015.cnblogs.com/blog/925240/201604/925240-20160423183358601-286358803.png)

这种情况下，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突，我们试试看：

```
$ git merge feature1
Auto-merging readme.txt
CONFLICT (content): Merge conflict in readme.txt
Automatic merge failed; fix conflicts and then commit the result.
```

果然冲突了！Git告诉我们，readme.txt文件存在冲突，必须手动解决冲突后再提交。`git status`也可以告诉我们冲突的文件：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
$ git status
On branch master
Your branch is ahead of 'origin/master' by 2 commits.
  (use "git push" to publish your local commits)
You have unmerged paths.
  (fix conflicts and run "git commit")

Unmerged paths:
  (use "git add <file>..." to mark resolution)

        both modified:   readme.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

我们可以直接查看readme.txt的内容：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
test git modify second
study git
three add
four add modify
five add modify
six add modify
seven add modify
eight add modify ...
create new branch dev..
<<<<<<< HEAD
goback master....
=======
create new branch feature1..
>>>>>>> feature1
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

Git用`<<<<<<<`，`=======`，`>>>>>>>`标记出不同分支的内容，我们修改如下后保存：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
test git modify second
study git
three add
four add modify
five add modify
six add modify
seven add modify
eight add modify ...
create new branch dev..
create new branch feature1..
goback master....
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

再提交：

```
$ git add readme.txt
$ git commit -m "fixed conflicts"
[master 0f3d64a] fixed conflicts
```

现在，`master`分支和`feature1`分支变成了下图所示：

![img](https://images2015.cnblogs.com/blog/925240/201604/925240-20160423184202945-1411793938.png)

用带参数的`git log`也可以看到分支的合并情况：

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```
$ git log --graph --pretty=oneline --abbrev-commit
*   0f3d64a fixed conflicts
|\
| * b4309b0 create new branch feature1 first modify
* | 0b56936 goback master first modify
|/
* 45ae9a9 create new branch....
* 90bc1f7 test name
* c1bdf43 test commit
* dd34c9a no add but commit,because use other parameter
* 4ed30d1 eight modify dify
* b45ca96 eight modify
* 9332d40 seven modify
* 72c6f9b six modify
* f64b5a0 five modify
* de8fd65 four modify
* 83a4b1e three modify
* 01c05cf two modify
* 1acafa7 first modify
* 09c1bba first git
```

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

最后，删除`feature1`分支：

```
$ git branch -d feature1
Deleted branch feature1 (was b4309b0).
```

### 小结

当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

用`git log --graph`命令可以看到分支合并图。

#### 参考

https://www.cnblogs.com/wangmingshun/p/5425150.html