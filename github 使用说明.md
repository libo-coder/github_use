## github 使用说明

### 本地  `pull`  到 `github` 远程仓库中

> 1. 在本地创建一个版本库（即文件夹），通过 `git init` 把它变成 $Git$ 仓库；
>
> 2. `cd` 进入到该目录，把项目复制到这个文件夹里面（粘贴后可以通过 `git status` 来查看当前的状态），再通过 `git add .` 把项目添加到仓库；[ 在这个过程中可以一直使用 `git status` 来查看当前的状态。]
>
> 3. 用 `git commit` 把项目提交到仓库。
>
>    ```nginx
>    git commit -m "first commit"		# 后面为注释内容
>    ```
>
> 4.  由于本地 $Git$ 仓库和 $Github$ 仓库之间的传输是通过 $SSH$ 加密的，所以连接时需要设置一下。[ 见下面 ]
>
> 5. 在 $Github$ 上创建一个 $Git$ 仓库
>
> 6. 在 $Github$ 上创建好 $Git$ 仓库之后我们就可以和本地仓库进行关联了，根据创建好的 $Git$ 仓库页面的提示，可以在本地仓库的命令行输入：
>
>    ```nginx
>    # origin 后面加的是 Github 上创建好的仓库的地址
>    git remote add origin https://github.com/libo-coder/remove_mark.git	
>    ```
>
> 7. 关联好之后我们就可以把本地库的所有内容推送到远程仓库（也就是 $Github$ ）上了，通过：
>
>    ```nginx
>    git push -u origin master
>    
>    # 由于新建的远程仓库是空的，所以要加上-u 这个参数，
>    # 等远程仓库里面有了内容之后，下次再从本地库上传内容的时候只需下面这样就可以了：
>    git push origin master
>    ```
>
> 8. 创建远程仓库的时候，如果勾选了 `Initialize this repository with a README`（就是创建仓库的时候自动给你创建一个`README`文件），由于新创建的那个仓库里面的`README`文件不在本地仓库目录中，这时我们可以通过以下命令先将内容合并再`push`：
>
>    ```nginx
>    git pull --rebase origin master
>    git push -u origin master
>    ```

### 本地 $Git$ 仓库与 $Github$ 仓库之间的连接

> 1. 查看是否安装了 $git$
>
>    ```nginx
>    git --version
>    ```
>
> 2. 初始化 $git$ 账户
>
>    ```nginx
>    git config --global user.name "libo"
>    git config --global user.email "mexingchen.li@gmail.com"
>    ```
>
> 3. 使用命令，检查 $SSH$ 是否已在电脑上存在
>
>    ```nginx
>    ls -al ~/.ssh
>    ```
>
> 4. 创建 $SSH\ KEY$。先看一下 `C` 盘用户目录下有没有`.ssh`目录，有的话看下里面有没有`id_rsa`和`id_rsa.pub`这两个文件，有就跳到下一步，没有就通过下面命令创建：
>
>    ```nginx
>    ssh-keygen -t rsa -C "mexingchen.li@gmail.com"
>    ```
>
>    然后默认保存路径，回车输入密码，再回车确认密码
>
> 5. 确定 $ssh-agent$ 程序已经产生了 $SSH\ key$
>
>    ```nginx
>    eval "$(ssh-agent-s)"
>    ```
>
> 6. 添加生成的 $SSH\ key$ 到 $ssh-agent$
>
>    ```nginx
>    ssh-add ~/.ssh/id_rsa
>    ```
>
>    然后输入密码即可
>
> 7. 找到 $id\_rsa.pub$ 文件的路径打开，里面保存的就是生成的 $SSH\ key$，全部复制
>
> 8. 进入 $git$ 账户，点击 $setting$，选择 $SSH\ key$，把复制好的 $SSH\ key$ 添加到自己的 $git$ 账户上面
>
> 9. 检查是否配置成功
>
>    ```nginx
>    git -T git@github.com
>    ```
>
>    如果出现 $Hi,\ libo-coder$，表明已经成功了。之后就可以使用 $git$ 了

### $Git$ 命令

> **查看、添加、提交、删除、找回，重置修改文件**
>
> ```nginx
> git help <command> 		# 显示command的help
> git show 				# 显示某次提交的内容 git show $id
> git co -- <file> 		# 抛弃工作区修改
> git co . 				# 抛弃工作区修改
> git add <file> 			# 将工作文件修改提交到本地暂存区
> git add . 				# 将所有修改过的工作文件提交暂存区
> git rm <file> 			# 从版本库中删除文件
> git rm <file> --cached 	 # 从版本库中删除文件，但不删除文件
> git reset <file> 		# 从暂存区恢复到工作文件
> git reset -- . 			# 从暂存区恢复到工作文件
> git reset --hard 		# 恢复最近一次提交过的状态，即放弃上次提交后的所有本次修改
> git ci --amend 			# 修改最后一次提交记录
> git revert <$id> 		# 恢复某次提交的状态，恢复动作本身也创建次提交对象
> git revert HEAD 		# 恢复最后一次提交的状态
> ```
>
> **查看提交记录**
>
> ```nginx
> git log git log <file> 	 # 查看该文件每次提交记录
> git log -p <file> 		 # 查看每次详细修改内容的diff
> git log -p -2 			# 查看最近两次详细修改内容的diff
> git log --stat 			# 查看提交统计信息
> ```
>
> **Git 本地分支管理：查看、切换、创建和删除分支**
>
> ```nginx
> git br -r 						 # 查看远程分支
> git br <new_branch> 			  # 创建新的分支
> git br -v 						 # 查看各个分支最后提交信息
> git br --merged 				 # 查看已经被合并到当前分支的分支
> git br --no-merged 				 # 查看尚未被合并到当前分支的分支
> git co <branch> 				# 切换到某个分支
> git co -b <new_branch> 			 # 创建新的分支，并且切换过去
> git co -b <new_branch> <branch>   # 基于branch创建新的new_branch
> git co $id 			# 把某次历史提交记录checkout出来，但无分支信息，切换到其他分支会自动删除
> git co $id -b <new_branch> 		 # 把某次历史提交记录checkout出来，创建成一个分支
> git br -d <branch> 				# 删除某个分支
> git br -D <branch> 				# 强制删除某个分支 (未被合并的分支被删除的时候需要强制)
> ```
>
> **git push 	# push所有分支**
>
> ```nginx
> git push origin master # 将本地主分支推到远程主分支
> git push -u origin master # 将本地主分支推到远程(如无远程主分支则创建，用于初始化远程仓库)
> git push origin <local_branch> # 创建远程分支， origin是远程仓库名
> git push origin <local_branch>:<remote_branch> # 创建远程分支
> git push origin :<remote_branch> #先删除本地分支(git br -d <branch>)，然后再push删除远程分支
> ```







