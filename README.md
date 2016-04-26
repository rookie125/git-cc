## git 工作中常用命令

查看常用的帮助信息

`$ git help`

查看所有的帮助信息

`$ git help -a`

查看git 配置信息

`$ git config --list`

#### 从头开始
##### 新建一个项目

```
$ mkdir work && cd work
$ git init

```

##### 新建一个文件并用`status`查看状态

```
$ git status

On branch master

Initial commit

nothing to commit (create/copy files and use "git add" to track)
```

##### 新建一个文件并查看状态

```
$ touch REANDE.md
$ git status

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

	index.html

nothing added to commit but untracked files present (use "git add" to track)
```

##### 使用`git add <file>`命令将工作目录的文件添加到暂存区

```
$ git add index.html
$ git status

On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   index.html
```


##### 添加到緩存区之后使用`git commit` 进行提交

```
$ git commit -m '提交的描述信息, 添加 index.html 文件'

master (root-commit) 09d7829] 提交的描述信息, 添加 index.html 文件
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 index.html

```


##### 提交之后可以使用`log`查看提交的信息

```
$ git log
$ git log --online
$ git log --online --decorate
```

##### 再次修改文件，使用`diff`可以查看工作目录和上次提交的对比

```
$ git diff <file>

$ git diff --staged
# 暂存区和上次提交的比较
```


##### 使用`git`来进行撤销操作(`HEAD`代表最近一次提交，--代表当前分支)

```
$ git checkout HEAD -- <file>
```

##### 使用git来撤销到最近一次的上一次提交（`^`符号代表上一次提交，几个`^`代表上几次）

```
$ git checkout HEAD^ -- <file>
```

##### 恢复指定提交到提交之前的一个版本

```
$ git revert <id>
```

##### 设置头部指针，也是回滚版本的一个好用方法

```
$ git reset <id>
reset可以设置头部指针，之后的一些提交会从当前指针开始，以前的提交将会被覆盖（相当于消失）
```

##### `git` 分支 `branch`

```
$ git branch
* master

$ git branch <branch-name>
$ git checkout <branch-name>
Switched to branch 'branch-name'
```

* 查看分支：`$ git branch`
* 创建分支：`$ git branch <name>`
* 切换分支：`$ git checkout <name>`
* 创建+切换分支：`$ git checkout -b <name>`
* 合并某分支到当前分支：`$ git merge <name>`
* 删除分支：`$ git branch -d <name>`
* 强制删除分支：`$ git branch -D <name>`


##### bug分支
###### 当你接到一个bug的任务时，很自然地你想创建一个issue分支来修复它，但是，当前正在dev上进行的工作还没有提交

```
$ git status

On branch dev
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	test.html

nothing added to commit but untracked files present (use "git add" to track)
```

###### 切换分支前提是当前工作目录是干净的，但是又不想提交当前未完成的开发，这时候可以使用`stash`命令，可以把当前工作目录的东西“备份”起来，等以后再“还原”继续开发

```
$ git stash

Saved working directory and index state WIP on dev: 09d7829 add index.html file
HEAD is now at 09d7829 add index.html file
```

###### bug修复好了，想要还原之前的工作目录继续进行开发

###### 查看一下我们的“备份”列表

```
$ git stash list

stash@{0}: WIP on dev: 09d7829 add index.html file
```

###### 恢复我们的工作目录有两种方法

###### 1.`git stash apply`，`apply`恢复后，`stash`内容并不删除，你需要用`git stash drop`来删除；
###### 2.`git stash pop`，恢复的同时把`stash`内容也删了

```
$ git stash pop

On branch dev
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)

	new file:   test.html

Dropped refs/stash@{0} (fa28f0641a4f1a1fcaf19d31bbf57409986be72e)
```

###### 可以`stash`多次，恢复其中一次的时候只需要指定一下索引

```
$ git stash apply stash@{0}
$ git stash drop stash@{0}

$ git stash pop stash@{0}
```






