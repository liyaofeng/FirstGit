创建版本库
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit

将目录变成版本管理仓库
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/

将文件添加到git仓库
$ git add readme.txt

将文件提交到仓库
$ git commit -m "wrote a readme file"
[master (root-commit) cb926e7] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt

查看仓库状态
$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#    modified:   readme.txt
#
no changes added to commit (use "git add" and/or "git commit -a")

查看文件修改的内容
$ git diff readme.txt 
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.

从最近开始查看提交日志
$ git log
commit 3628164fb26d48395383f8f31179f24e0882e1e0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Tue Aug 20 15:11:49 2013 +0800

    append GPL

commit ea34578d5496d7dd233c827ed32a8cd576c5ee85
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Tue Aug 20 14:53:12 2013 +0800

    add distributed

commit cb926e7ea50ad11b8f9e909c05226233bf755030
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Mon Aug 19 17:51:55 2013 +0800

    wrote a readme file

简单查看提交日志
$ git log --pretty=oneline
3628164fb26d48395383f8f31179f24e0882e1e0 append GPL
ea34578d5496d7dd233c827ed32a8cd576c5ee85 add distributed
cb926e7ea50ad11b8f9e909c05226233bf755030 wrote a readme file

返回上个版本，head表示当前版本，head^^表示上上个版本，head~100表示上100个版本
$ git reset --hard HEAD^
HEAD is now at ea34578 add distributed

返回指定版本
$ git reset --hard 3628164
HEAD is now at 3628164 append GPL

查看命令日志
$ git reflog
ea34578 HEAD@{0}: reset: moving to HEAD^
3628164 HEAD@{1}: commit: append GPL
ea34578 HEAD@{2}: commit: add distributed
cb926e7 HEAD@{3}: commit (initial): wrote a readme file

查看工作区和最新代码库的区别
$ git diff HEAD -- readme.txt 
diff --git a/readme.txt b/readme.txt
index 76d770f..a9c5755 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,4 +1,4 @@
 Git is a distributed version control system.
 Git is free software distributed under the GPL.
 Git has a mutable index called stage.
-Git tracks changes.
+Git tracks changes of files.

让工作区回到最近的暂存区或者仓库代码
$ git checkout -- readme.txt

丢弃暂存区的内容
$ git reset HEAD readme.txt
Unstaged changes after reset:
M       readme.txt

删除文件
$ git rm test.txt
rm 'test.txt'
$ git commit -m "remove test.txt"
[master d17efd8] remove test.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt

SSH加密，主目录下运行
$ ssh-keygen -t rsa -C "youremail@example.com”

id_rsa为私密钥匙，id_rsa.pub为公钥，复制id_rsa.pub的内容
iMacTest:~ test$ cd .ssh
iMacTest:.ssh test$ ls -a
.		..		id_rsa		id_rsa.pub

仓库目录下运行，将本地仓库和给他github仓库关联
$ git remote add origin git@github.com:michaelliao/learngit.git

将本地仓库的内容推送到github仓库，第一次加上-u参数，不仅把内容推送到其他分支，还把自己和其他分支关联起来
$ git push -u origin master
Counting objects: 19, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (19/19), done.
Writing objects: 100% (19/19), 13.73 KiB, done.
Total 23 (delta 6), reused 0 (delta 0)
To git@github.com:michaelliao/learngit.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.

第一次推送内容后，使用以下命令提价
$ git push origin master

从远程仓库克隆
$ git clone git@github.com:michaelliao/gitskills.git
Cloning into 'gitskills'...
remote: Counting objects: 3, done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Receiving objects: 100% (3/3), done.
$ cd gitskills
$ ls
README.md

创建并切换分支
$ git checkout -b dev
Switched to a new branch 'dev'

-b参数表示创建并切换，相当于以下两条命令
$ git branch dev
$ git checkout dev
Switched to branch 'dev'

查看当前分支
$ git branch
* dev
  master

切换分支
$ git checkout master
Switched to branch 'master'

合并分支
$ git merge dev
Updating d17efd8..fec145a
Fast-forward
 readme.txt |    1 +
 1 file changed, 1 insertion(+)

删除分支
$ git branch -d dev
Deleted branch dev (was fec145a).

合并分支，不使用Fast Forward，本次合并好创建一个新的commit，所以要加上-m
$ git merge --no-ff -m "merge with no-ff" dev
Merge made by the 'recursive' strategy.
 readme.txt |    1 +
 1 file changed, 1 insertion(+)

查看分支历史
$ git log --graph --pretty=oneline --abbrev-commit
*   7825a50 merge with no-ff
|\
| * 6224937 add merge
|/
*   59bc1cb conflict fixed
...

存储工作现场
$ git stash
Saved working directory and index state WIP on dev: 6224937 add merge
HEAD is now at 6224937 add merge

获取存储的工作现场列表
$ git stash list
stash@{0}: WIP on dev: 6224937 add merge

恢复工作现场，使用git stash apply 命令不会把存储的工作现场删除，要手动执行git stash drop 命令来删除，git stash pop 恢复的同时把内容也删除了
$ git stash pop
# On branch dev
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       new file:   hello.py
#
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   readme.txt
#
Dropped refs/stash@{0} (f624f8e5f082f2df2bed8a4e09c12fd2943bdd40)

如果分支别有合并，删除失败，可以使用强制删除
$ git branch -D feature-vulcan
Deleted branch feature-vulcan (was 756d4af).

查看远程库信息
$ git remote
origin

远程库详细信息，没有推送权限看不到push
$ git remote -v
origin  git@github.com:michaelliao/learngit.git (fetch)
origin  git@github.com:michaelliao/learngit.git (push)

1111111111111111111111
3333333333333333333333