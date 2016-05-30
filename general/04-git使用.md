#git操作流程

##普通用户
1. 切换到自己的分支例如:

   ```
   git checkout gss 
   ``` 
2. 从远程dev分支拉取最新代码:

   ```
   git pull origin dev
   ```
3. 开始自己的代码编写.
4. 查看代码状态:

   ```
   git status
   ```
4. 提交代码到暂存区:

   ```
   git add -A
   ```
5. 提交代码到本地版本库:

   ```
   git commit -m "commit a function"
   ```
6. 将本地版本库内容上传到以自己名字命名的远程分支:

   ```
   git push origin gss -m "push 说明"
   ```

##管理员
1. 登录程序运行的服务器.
2. 切换到远程有更新的分支上,例如远程gss分支更新,则切换到本地的gss分支:
   
   ```
   git checkout gss
   ```
3. 拉取这个分支最新代码:

   ```
   git pull origin gss
   ```
4. 切换到本地dev分支:

   ```
   git checkout dev
   ```
5. 先拉取远程dev分支代码:

   ```
   git pull origin dev
   ```
6. 查看本地dev分支与更新后的gss分支内容差异,然后合并:

   比较:
   ```
   git diff gss
   ```
   合并:
   ```
   git merge gss
   ```
7. 合并完成后,dev分支也成为最新的代码,然后上传到远程dev分支:

   ```
   git push origin dev -m "xxxx"
   ```

##其他功能

###查看修改内容
1. 查看工作区和暂存区的区别

   ```
   git diff
   ```
2. 查看工作区与版本库的区别

   ```
   git diff HEAD -- file.py
   ```
3. 查看暂存区与版本库的区别

   ```
   git diff --cached
   ```

###撤销修改
1. 撤销工作区的修改,回到最近一次git commit 或 git add时的状态:
   
   ```
   git checkout -- file 
   ```
2. 撤销add到暂存区的修改:

   ```
   git reset HEAD file
   ```
3. 撤销commit到版本库的内容,得采用版本回退:

   查看git提交日志,获取版本号:
   
   ```
   git log
   ```
   
   版本回退:
   
   ```
   git reset --hard 123456
   ```
   
   或者使用HEAD命令,HEAD^表示上一个版本,再上就是HEAD^^,或者HEAD~3:
   
   ```
   git reset --hard HEAD^
   ```

   如果反悔,想要回到最新的版本,先获取之前commit的版本id:
   
   ```
   git reflog
   ```
   
   然后再回退:
   
   ```
   git reset --hard 123456
   ```
   


   
