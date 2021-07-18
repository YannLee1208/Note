## git

> 包含了github使用以及git使用的流程、命令和常见问题总结

* github创建rep流程

```shell l
1. git init  
2. git add . --把当前文件夹内的add进本地git仓库
3. git commit -m "first commit" -- commit进本地仓库

4. github上创建仓库 获取ssh或者http github上setting里面设置key和本地的isa_key.pub绑定
5. git remote add origin https://github.com/YannLee1208/Note.git
6. git push -u origin main 
--由于新建的远程仓库是空的，所以要加上-u这个参数，等远程仓库里面有了内容之后，下次再从本地库上传内容的时候只需下面这样就可以了：
	git push origin main
```

* github更新

第一步：查看当前的git仓库状态，可以使用git status

`git status`

第二步：更新全部

`git add *`

第三步：接着输入git commit -m “更新说明”

`git commit -m “更新说明”`

第四步：先`git pull`,拉取当前分支最新代码（也就是获取GitHub上的最新代码信息，更新本地代码）

`git pull`

第五步：push到远程master分支上（修改本地代码后，再更新GitHub上的代码）

`git push origin master`

**先pull，再push**



* 常用命令

`git remote -v` 

查看所有origin之类的别名所指向的网址



### 分支

`git branch (branchname)` ： 创建分支

`git branch ` : 列出所有分支.  `git init` 的时候默认创建 `main` 分支

`git branch -d (branchname) ` :  删除分支

`git checkout (branchname)` ：切换分支

`git checkout -b (branchname)  ` 创建分支并切换到该分支`

`git merge ` ：分支合并 **合并完以后一般删除分支**



### pull

**fetch**

`git fetch`执行后完成两个步骤：

1. 从远程仓库下载本地仓库中缺失的提交记录
2. 更新远程分支指针（如origin/master）

即git fetch实际上将本地仓库中的远程分支更新成了远程仓库相应分支最新的状态

注意：

git fetch并不会改变你本地仓库的状态，也不会修改你磁盘上的文件，git fetch为单纯的下载操作。

`git fetch origin/master` + `git merge origin/master` = `git pull`：下载并更新为远程仓库的内容，即同步

git fetch 的参数
类似于git push的参数方法，git fetch的参数非常类似，他们的概念是相同的，方向是相反的（此处为下载而非上传）

\<place>参数

git fetch origin \<place>：从远程\<place>分支上拉取到本地对应的分支上


执行git fetch origin foo命令后，会从远程foo分支下载，并更新本地的o/foo分支，没有更新本地的非远程分支foo

\<source>:\<destation>参数

命令能够直接更新本地分支，不过不能在检出当前分支上干这件事，在其他分支上可以。fetch的两个参数与git push是正好相反的：

\<source>指的是远程仓库中的位置
\<destation>是要放置提交的本地仓库的位置


执行 git fetch origin foo~1:bar，Git将foo~1解析成一个 origin 仓库的位置，然后将那些提交记录下载到了本地的 bar 分支（一个本地分支）上。注意由于我们指定了目标分支，foo 和 o/foo 都没有被更新：


如果目标分支不存在，即本地分支不存在目标分支情况，会和 git push 一样，Git 会在 fetch 前自己创建立本地分支, 就像是 Git 在 push 时，如果远程仓库中不存在目标分支，会自己在建立一样。

**pull**

> git pull 其实就是fetch 后面跟merge的缩写，可以理解为使用同样的参数执行git fetch，然后再merge你所抓到的提交记录

参数
只有\<place>参数：

git pull origin foo相当于：

git fetch origin foo; git merge o/foo

有\<source>和\<destation>参数：

git pull origin bar~1:bugFix相当于：

git fetch origin bar~1:bugFix; git merge bugFix，注意：可不在bugFix分支

例子
初始状态：注意本地在master分支上


目标状态：


执行 git pull origin bar:foo，从远程分支上bar拉取更新的到本地，并创建本地分支foo，同时将该分支合并到master分支上：


执行 git pull origin master:side，从远程分支上master拉取更新的到本地，并创建本地分支side，同时将该分支合并到master分支上：





### 问题

* `failed to push some refs to  https://github.com/xxx.git`
  * 如果在创建远程仓库的时候，勾选了Initialize this repository with a README（就是创建仓库的时候自动给你创建一个README文件, 那么在push的时候就会报错
  * 方案
    * `$ git pull --rebase origin master`
* `src refspec main does not match any`
  * 原因如下
    * 本地git仓库目录下为空
    * 本地仓库add后未commit
  * 方法
    * 加入文件以后再commit过

* `git pull origin master` 时 `fatal: refusing to merge unrelated histories`
  * `git pull origin master –allow-unrelated-histories`

* `Fatal: fatal: unable to access 'https://github.com/xxx': OpenSSL SSL_connect: SSL_ERROR_SYSCALL in connection to github.com:443`

  * `git config --global --add remote.origin.proxy ""`

  

* ```
  error: Pulling is not possible because you have unmerged files.
  hint: Fix them up in the work tree, and then use 'git add/rm <file>'
  hint: as appropriate to mark resolution and make a commit.
  fatal: Exiting because of an unresolved conflict.
  ```

  * `git commit -m "resolved merge conflicts"`
  * 然后再push

