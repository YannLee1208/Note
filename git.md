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

    

