- [git基础配置](#git基础配置)
- [git submodule](#git-submodule)
- [git giff](#git-giff)
- [撤销操作](#撤销操作)
- [分支功能](#分支功能)
  * [对tag代码进行修改](#对tag代码进行修改)
- [git设置多账号](#git-----)
- [git comment规范](#git-comment规范)


## git基础配置
```
git config --global user.name  "用户名"
git config --global user.email "邮箱"
```

## git submodule
添加submodule

```
git submodule add [submodule本地或者远程地址] [submodule名]
示例：
git submodule add ../moduleA.git moduleA
git submodule add git@github.com/xxx/moduleA.git moduleA

```

添加完submodule，会生成.gitmodules文件

```
[submodule "moduleA"]
    path = moduleA
    url = git@github.com:xxx/moduleA.git
```

删除submodule

```
git rm --cached moduleA
rm -rf moduleA
rm .gitmodules
vim .git/config
```

拉取submodule代码到本地

```
git submodule update
```

单独更新某个submodule代码

```
cd moduleA
git pull
```

### 备注问题

**1.git submodule update后，会显示modified files status**

解决方式：https://stackoverflow.com/questions/6006494/git-submodule-modified-files-status

**2.How to change the remote repository for a git submodule**

You should just be able to edit the .gitmodules file to update the URL and then run git submodule sync to reflect that change to the superproject and your working copy.

**3.克隆带子模块的版本库**

方法一，先clone父项目，再初始化submodule，最后更新submodule，初始化只需要做一次，之后每次只需要直接update就可以了，需要注意submodule默认是不在任何分支上的，它指向父项目存储的submodule commit id

```
git clone project.git project2
cd project2
git submodule init
git submodule update
```

方法二，采用递归参数--recursive，需要注意同样submodule默认是不在任何分支上的，它指向父项目存储的submodule commit id。

```
git clone project.git project3 --recursive
```

## git giff

```
diff里面a表示前面那个变量，b表示第二个变量
HEAD     commit版本
Index    staged版本
```

### diff两个branch

```
// diff between 两个分支
git diff branch1..branch2   

// diff from他们共同的祖先
git diff branch1...branch2  

// diff本地分支和远程分支的不同(--stat仅列出不同的文件)
git diff --stat master origin/master

```

## 撤销操作

### 撤销工作区的修改

```
$ git status
On branch master
Changes not staged for commit:
	modified:   readme.txt

$ git checkout -- file xxx.txt
```

### 撤销暂存区的提交

```
$ git add readme.txt
$ git status
On branch master
Changes to be committed:
    modified:   readme.txt

$ git reset HEAD <file>
```

### 撤销commit的提交

```
$ git log
commit 6b953d44c732a6914be3f13b0d9172b6fd28b86e (HEAD -> master)
Author: xxxxx
Date:   Sun Apr 7 22:10:15 2019 +0800

    commit message xxxx

commit 70daeafb4cebe0a7ce1b8308e0c9b9ab1fda0208 (origin/master)
Author: xxxx
Date:   Sun Apr 7 21:30:43 2019 +0800

    commit message yyyy
$ git reset --hard 6b953d44c732a6914be3f13b0d9172b6fd28b86e // 撤销这次提交
```

### 本地修改冲突时的的保留和撤销

如果本地修改后，在做git pull时，跟线上版本有冲突，会出现如下的错误

```
$ git pull
error: Your local changes to the following files would be overwritten by merge:
        xxxx/xxx.go
        yyyy/yyy.go
Please, commit your changes or stash them before you can merge.
```

如果保留本地所做的改动，仅仅merge线上的代码, 处理方法如下:

```
git stash
git pull
git stash pop
```

如果希望线上版本的文件完全覆盖本地工作版本，方法如下:

```
git reset --hard
git pull
```

## 分支功能
### 分支创建

```
// 分支创建并切换
$ git checkout -b dev
Switched to a new branch 'dev'

等同于

$ git branch dev
$ git checkout dev
Switched to branch 'dev'

$ git branch
* feature_dobly_audio   ## *号指向那个分支，代表HEAD指向哪个分支
  master

```

### 分支合并

```
$ git checkout master   // 切到master分支
$ git merge dev			 // 将dev合并到master
```

### 分支删除

```
// 删除本地分支
$ git branch -d dev
error: The branch 'dev' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature_dobly_audio'
```
如果分支没有被合并到master，通过-d删除不了，如果非要删除，可以用-D强制删除。

```
// 删除远程分支
$ git push origin :branch-name
```

### 分支冲突解决

```
$ git merge feature_dobly_audio
Auto-merging simple/main.cpp
CONFLICT (content): Merge conflict in simple/main.cpp
Automatic merge failed; fix conflicts and then commit the result.

$ git status  // 可以查看具体冲突文件
```

打开冲突的文件，具体如下：

```
#include<iostream>
using namespace std;

<<<<<<< HEAD
void hdr10() {
    cout << "hdr10" << endl;
}
=======
void say(const string& content)
{
    cout << "say " << content << endl;
}

>>>>>>> feature_dobly_audio
```
git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容

修改冲突后的代码如下：

```
#include<iostream>
using namespace std;

void hdr10() {
    cout << "hdr10" << endl;
}

void say(const string& content)
{
    cout << "say " << content << endl;
}

```

重新提交文件

```
$ git commit -a -m "confict resulotion"
$ git push origin master
```

5.分支冲突处理(accept mine or accept others)
The solution is very simple. git checkout <filename> tries to check out file from the index, and therefore fails on merge.

What you need to do is (i.e. checkout a commit):

To checkout your own version you can use one of:

```
git checkout HEAD -- <filename>
or

git checkout --ours -- <filename>
or

git show :2:<filename> > <filename> # (stage 2 is ours)
```

To checkout the other version you can use one of:

```
git checkout test-branch -- <filename>
or

git checkout --theirs -- <filename>
or

git show :3:<filename> > <filename> # (stage 3 is theirs)
You would also need to run 'add' to mark it as resolved:

git add <filename>
```

### 对tag代码进行修改

```
基于指定tag版本创建一个分支
git checkout -b local_branch tag_name

添加新文件代码
git add .

提交变更
git commit -m “紧急修复说明”

删除本地tag
git tag -d tag_name

将本地最新代码发布成tag版本
git tag tag_name

将本地tag发布到远程
git push origin :tag_name

本地代码推送到新的远程tag
git push origin tag_name
git fetch origin

```

## git设置多账号

## git comment规范
Commit message 都包括三个部分：Header，Body 和 Footer。

```
<type>(<scope>): <subject>
// 空一行
<body>
// 空一行
<footer>
```
type用于说明 commit 的类别，只允许使用下面7个标识。

* feat：新功能（feature）
* fix：修补bug
* docs：文档（documentation）
* style： 格式（不影响代码运行的变动）
* refactor：重构（即不是新增功能，也不是修改bug的代码变动）
* test：增加测试
* chore：构建过程或辅助工具的变动
