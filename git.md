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

