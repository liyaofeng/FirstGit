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