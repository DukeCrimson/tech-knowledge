分支的本质
================================
Git 中的分支，其实本质上仅仅是个指向commit对象的可变指针,就是从某个提交对象往回看的历史.每次commit提交之后,指针都会向前移动.git init之后会使用 master 作为分支的默认名字.

**git branch XXX** 创建分支XXX  

仅仅是创建了分支XXX,即新建一个指针XXX,指向当前的commit对象.并没有切换到XXX分支.

**git checkout XXX** 切换到XXX分支

**git checkout -b XXX** 创建XXX分支,并切换到XXX分支

**git branch -a** 查看本地及远程分支

**git merge bugfix** 将bugfix分支合并到当前分支
实际上是将当前分支向前移动，指向bugfix所指的commit对象，所以叫快进合并。

**git ls-files -s** 查看暂存区文件

**git branch -d branchname** 删除分支

**git branch -m branchName newbranchName** 重命名分支

**git remote** 查看已设置的远程分支

**git remote show branchName** 查看远程分支详细信息

**git remote -v** 查看远程分支地址

**git remote add origin url** 添加远程仓库

**git remote rename oldName newName** 重命名远程分支

**git remote rm xx** 删除远程分支

**git checkout -b origin/branchName** 
检出对应分支的代码.并自动创建检出和远程分支名字一样的本地分支

**git fetch** 只拉取远程仓库代码到本地，不自动合并，取得的新提交会导入本地自动建立的分支中，并可以切换这个名为FETCH_HEAD的分支。
也可以将这个分支合并到自己本地某个分支中。

**git push 本地分支名字 远程仓库/分支名字** 推送到远程分支

代码的撤销与回滚
==============================
本地撤销：

①文件被修改，未add —— git checkout filename

②对多个文件执行git add，但只想提交一部分 —— git reset HEAD filename

③执行git add，但想撤销对其的修改 —— 

    git checkout filename 撤销修改

④已在本地进行了多次git commit操作，现在想撤销到其中某次Commit
    git reset [--hard|soft|mixed|merge|keep] [commit|HEAD


远程回滚

①撤销指定文件到指定版本 —— 
    查看指定文件的历史版本 git log <filename>
    回滚到指定commitID git checkout <commitID> <filename>

②删除最后一次远程提交 —— 
    
    方法一：使用revert
        
        git revert HEAD
        
        git push origin master
    
    方式二：使用reset
        
        git reset --hard HEAD^
        
        git push origin master -f
    
    区别：
        revert是放弃指定提交的修改，但是会产生一次新的提交，之前的历史记录都在
        
        reset是将HEAD指针指到指定提交，历史记录中不会出现放弃的提交记录。

③回滚某次提交
    
    git log（找到要回滚的commitId）
    
    git revert commitId

④删除某次提交
    
    git log --oneline -n5
    
    git rebase -i "commitId"^ ^号指的是commitId的前一次提交

####git stash

暂时存储代码，stash是仅在本地仓库的概念。
    
    git stash (save 'stash-name') 存储暂存代码
    git stash list 查看暂存列表
    git stash apply stash@{0} 将暂存代码拉回代码库
    git stash drop stash@{0} 删除某个stash
    git stash clear 删除所有的stash
    git stash branch newBranch 从stash创建一个新的分支
    
    git push origin branchname 在远程新建分支，并将本地的当前分支提交上去
    git branch --set-upstream-to origin/remotebranchName localbranchName
    本地分支与远程分支相关联