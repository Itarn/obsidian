-   git commit

	-   git commit -am‘message’ 自动添加到暂存区并直接生成一个 commit
	-   git commit --amend 修改最近分支的提交信息

-   **比较暂存区和HEAD所含文件的差异**

	-   git diff --cached || --staged

-   **比较暂存区与工作区所含文件的差异**

	-   git diff
	-   git diff -- 文件名

-   **修改最近分支的提交信息**

	-   git commit --amend

-   **修改老旧的提交信息,此时分支未分享**

	-   git rebase -i commitID
		-   说明：commitID 为 要修改某节点的父节点 commitID
	-   在 rebase 编辑模式下，通过命令 reword 修改该节点的 msg

	-   自动进入 msg 修改模式

-   **把连续的commid合成一个**

	-   git rebase -i commitID
		-   说明：commitID 为 要修改某节点的父节点 commitID
	-   在 rebase 编辑模式下，通过命令 squash 合并该节点的 msg

	-   自动进入 msg 修改模式

-   **把不连续的commid合成一个**

	-   git rebase -i commitID
		-   说明：commitID 为 要修改某节点的父节点 commitID
	-   在 rebase 编辑模式下

	-   把不连续的 commitID 放在一个基准 commid 后 HEAD
	-   基准 commid 不变

	-   其他 commid squash 合并该节点的 msg

-   自动进入 msg 修改模式

-   **正确删除文件的方法**

	-   git rm 文件名

-   **主分支合并分支，保证干净的提交历史**

	-   git merge --no-commit

-   **feature 本地分支 rebase 后，推送到远端 feature 分支**

	-   git push --force origin feature
	-   git push **_--force-with-lease_** origin feature 有警告

-   **暂存的修改并入最近的一次 commit，并且不会修改这次 commit 的信息（这样 Git 也就不会打开一个文件编辑界面了）**

	-   git commit --amend --no-edit

-   **暂存区恢复成和 HEAD 的一样**

	-   全部：git reset HEAD
	-   部分：git reset HEAD -- 文件名

	-   git diff --cached

-   **工作区恢复成暂存区一样**

	-   git checkout -- 文件名

-   **消除最近的几次提交**

	-   git reset --hard commitID

-   **远程回滚 强推**

	-   git push -f origin master

-   **看看不同提交的指定文件的差异**

	-   git diff commitID1 commitID2 -- 文件名
	-   git diff 分支名1 分支名2 -- 文件名

-   **开发中临时加塞**

	-   git stash apply
	-   git stash pop

-   当远端没有本地分支执行 git push 时，会有提示，去掉提示

	-   git config --global push.default current

-   删除远程分支

	-   git push origin -d f_coupon_alan

-   查看当前文件的提交历史

	-   git log filename
	-   git show commit_id

### Tag 相关

-   **push 单个 tag**

	-   git push origin [tagname]

-   **push 所有 tag**

	-   git push --tags
	-   git push origin --tags

-   删除远程便签

	-   git push origin :refs/tags/标签名

-   移动标签

	-   git tag -f tagname commitid
	-   git push --tags -f

-   展示所有标签

	-   git tag -l

### Swith 相关

-   切换到上次分支

	-   git switch -

-   创建新分支

	-   git switch -c

### 基础
-   git config

	-   作用域

		-   --local
		-   --global

		-   --system

	-   查看

		-   --global -l

-   git mv a b 重命名
-   git log

	-   git log --all 查看所有分支的历史
	-   git log --all --graph 查看图形化的 log

	-   git log --oneline 查看单行的简洁历史。
	-   git log --oneline -n4 查看最近的四条简洁历史。

	-   git log --oneline --all -n4 --graph 查看所有分支最近 4 条单行的图形化历史。
	-   git help --web log 跳转到git log 的帮助文档网页

-   git cat-file -t 命令 ， 查看 git 对象的类型
-   git cat-file -p 命令， 查看 git 对象的内容

-   git cat-file -s 命令， 查看 git 对象的大小
-   ls -al 命令， 表示列出当前目录下的所有文件（包括隐藏文件）