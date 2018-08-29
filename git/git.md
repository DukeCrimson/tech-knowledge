####分支的本质
Git 中的分支，其实本质上仅仅是个指向commit对象的可变指针,就是从某个提交对象往回看的历史.每次commit提交之后,指针都会向前移动.git init之后会使用 master 作为分支的默认名字.

**git branch XXX** 创建分支XXX  

仅仅是创建了分支XXX,即新建一个指针XXX,指向当前的commit对象.并没有切换到XXX分支.

**git checkout XXX** 切换到XXX分支

**git checkout -b XXX** 创建XXX分支,并切换到XXX分支



