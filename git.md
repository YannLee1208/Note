## git

> 包含了github使用以及git使用的流程、命令和常见问题总结

* github创建rep流程

```git
1. git init  
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/YannLee1208/Note.git
git push -u origin main
```





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