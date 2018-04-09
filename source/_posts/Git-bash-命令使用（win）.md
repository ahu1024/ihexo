---
title: Git bash 命令使用（win）
tags:
  - Git
date: 2018-03-28 09:31:08
updated: 2018-03-28 09:31:08
---

>Git for Windows 主要提供了一个轻量的、本地化的git 命令工具，提供了命令行下的全功能界面操作，可以从windows命令行执行git命令. *NIX 用户 应该会觉得很顺手, 在这个仿真环境下，使用git命令跟linux 和 UNIX 一样一样的。
...................................................................................................


## Git概念

- **工作区：** 就是你在电脑上看到的目录，比如目录下`testgit`里的文件(`.git`隐藏目录版本库除外)。或者以后需要再新建的目录文件等等都属于工作区范畴。

- **版本库(Repository)：** 工作区有一个隐藏目录`.git`,这个不属于工作区，这是版本库。其中版本库里面存了很多东西，其中最重要的就是`stage`(暂存区)，还有Git为我们自动创建了第一个分支`master`,以及指向`master`的一个指针`HEAD`。
- **分支策略**: 在实际开发中，我们应该按照几个基本原则进行分支管理：首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；干活都在dev分支上，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的单独分支，时不时地往dev分支上合并就可以了。
- **多人协作**： 
    - 首先用git push origin branch-name推送自己的修改；
    - 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
    - 如果合并有冲突，则解决冲突，并在本地提交；
    - 没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！
    - 如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。


## Git安装

- [Git download...](git-scm.com) 下载完成后，一路默认安装完毕，桌面右击，右键菜单出现 `git bash`,恭喜你已经安装成功！

## Git配置

- 创建用户信息
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

- 创建`SSH Key`,在用户目录下查看是否存在`.ssh`目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果有的话，直接跳过此如下命令，如果没有的话，打开git bash，输入如下命令：
```
ssh-keygen  -t rsa –C “youremail@example.com”
//得到id_rsa（私钥不能泄露出去），id_rsa.pub（公钥，可以放心地告诉任何人）。
```

- 关联认证信息，登录github,打开`settings`中的`SSH Keys`页面，然后点击`Add SSH Key`,填上你的标题，在Key文本框里黏贴`id_rsa.pub`文件的内容。

## Git建仓
- 仓库分为远程仓库和本地仓库，可以建好远程仓库然后克隆到本地仓库，也可以建好本地仓库和远程仓库，将本地仓库和远程仓库进行关联。

### 本地仓库
- 打开git bash
```
cd d:       //进入d盘
cd www      //进入www文件夹
mkdir guong //创建guong文件夹
cd guong    //进入guong文件夹
pwd         //显示当前目录路径
git init    //初始化当前目录变成git可以管理的仓库，文件新增`.git`文件夹（勿动
```

- 在目录下新建`test.txt`,执行`git bash`
```
git add test.txt                //将文件添加暂存区
git commit -m '提交test.txt文件' //'提交test.txt文件'为注释
git status                      //查看暂存区和仓库状态
```

- 在test.txt中添加一行文本` ”第一行文本添加，文件已被修改“ `,执行`git bash`
```
git status        //查看暂存区和仓库状态
    //此处显示 modified: test.txt，文件已被修改
git diff test.txt //查看文件具体修改内容
    //此处显示文本内的详细更改
git add test.txt                //将文件添加暂存区
git commit -m '提交test.txt文件' //'第二次提交test.txt文件'为注释
git status                      //查看暂存区和仓库状态
    //此处显示，文件没有修改
git log                         //查看commit提交详细记录
git log –pretty=oneline         //查看commit提交简要记录
git reset  –hard HEAD~1         //将仓库回退到前一个版本
git reflog                      //查看历史版本号
git reset  -hard 版本号          //通过版本号回退到指定版本
git checkout --test.txt     
/***  
  *将test.txt文件在工作区做的修改全部撤销,分两种情况：
  *1·test.txt自动修改后，还没有放到暂存区，使用 撤销修改就回到和版本库一模一样的状态。
  *2·另外一种是test.txt已经放入暂存区了，接着又作了修改，撤销修改就回到添加暂存区后的状态。
  *注意：命令git checkout — readme.txt 中的 — 很重要，如果没有 — 的话，那么命令变成创建分支了。
  */
```

### 远程仓库
- 以上我们创建了本地的仓库-`guong`，现在我们必须创建远程仓库-`guong.github.io`，创建完毕。
- Git 支持许多数据传输协议。`git:// 协议` ;`http(s):// 协议`; `user@server:/path.git`表示SSH 传输协议。
- 关联远程仓库和本地仓库，执行`git bash`
```
git remote add origin https://github.com/tugenhua0707/testgit.git  //在本地仓库目录下执行
//OR本地dev分支与远程origin/dev分支的链接,设置dev和origin/dev的链接：
$ git branch --set-upstream dev origin/dev
```

- 克隆远程仓库到本地（无仓库），执行`git bash`
```
git clone git://github.com/schacon/grit.git  guong                 //在自定义文件夹下克隆并创建新仓库 guong 关联远程仓库
```

## Git分支
- 因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这和直接在`master`分支上工作效果是一样的，但过程更安全。
- 合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。

### HEAD
- 首先，在Git中用`HEAD`表示当前版本，上一个版本就是`HEAD^`,上上版本就是`HEAD^^`,倒数第100个就是`HEAD~100`.

### master
- 在git中，每一次提交都处于一条不断变化的时间线上，这条时间线就是一条主分支-`master`,git会创建一个`master`指针指向主分支`master`.
- 我们的HEAD会默认指向`master`指针。每一次提交，`master`指针都会随`master`主分支移动，主分支也越来越长。

### dev
- 当我们创建分支`dev`时,它会继承主分支`master`,并且git会创建一个`dev`指针。
- 将HEAD指`dev`,当再次提交，`dev`分支就会越来越长，`dev`指针会向前移动，而`master`指针不会移动。
```
git branch             //查看分支，*代表当前分支
git checkout -b dev    //创建dev分支（-b 表示创建并切换，等价于下面的两条语句）
git branch dev         //创建
git checkout dev       //切换
```

### merge
- 当我们在`dev`分支上完成工作，就将`dev`分支合并到`master`主分支，合并是“快进模式”，git会将`master`指针直接指向`dev`分支，效率极高。
```
git merge dev           //将当前dev分支合并到主分支，
git branch -d dev       //删除dev分支
```

## Git冲突
- `master`分支和`dev`分支各自都分别有新的提交时，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有冲突。可以用`mergez`或者`status`查看冲突.
- Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，我们修改如下后保存再提交.
- 用带参数的`$ git log --graph --pretty=oneline --abbrev-commit`也可以看到分支的合并情况,最后，删除分支.
- 当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
- 用git log --graph命令可以看到分支合并图。

## Git操作
- 基本常用操作(符号约定：[]：可选　　<>：必选)
```
git config [--global] user.name <name>　　　　设置用户名
git config [--global] user.email <email>　　　　　设置邮箱
git config [--global] core.editor <editor>　　　　设置编辑器
git config [--global] github.user <user>　　　　　设置github帐号名
git config [--global] github.token <token>　　　  设置github的token
git clone <url>　　　　　　　　　　　　　　　　　　　ssh/http(s)/git三种协议，ssh和https可推送
git init　　　　　　　　　　　　　　　　　　　　　　  初始化Git仓库
git add <file>　　　　　　　　　　　　　　　  将文件加入index file
git rm [--cached]　　　　　　　　　　　　　   删除，加--cached表示仅从index file中删除文件，即放弃跟踪
git mv <src> <dest>　　　　　　　　　　　　   移动/更名
git diff --cached/--staged　　　　　　　　　　当前索引与上次提交（有哪些需要commit）
git diff　　　　　　　　　　　　　　　　　     当前索引与工作目录（有哪些需要add）
git diff HEAD[^]　　　　　　　　　　　　　　  工作目录与上次提交（当前目录与上次提交有何改变）
git commit [-a] -m <msg>　　　　　　　　　 　提交
git commit --amend [-m <msg>]　　　　　　　  修复上次提交
git reset HEAD <file>　　　　　　　　　　　   同--mixed，default option
git reset --mixed HEAD　　　　　　　　　　    撤销 commit 和index file,只保留 working tree 的信息
git reset --hard HEAD[^]　　　　　　　　　　  将 working tree 和 index file 都撤销到以前状态
git reset --soft HEAD[^]　　　　　　　　　　  只撤销 commit,而保留 working tree 和 index file 的信息
　　　　　　　　　　　　　　　　　　　　　      回复到某个状态。以git reset --soft HEAD为例，commit回退到
　　　　　　　　　　　　　　　　　　　　      　HEAD（相当于无变化），若是HEAD^，则commit回退到HEAD^
git gc　　　　　　　　　　　　　　　　　　          用垃圾回收机制清除由于 reset 而造成的垃圾代码
git status　　　　　　　　　　　　　　　　　        显示当前工作目录状态
git log [-p]　　　　　　　　　　　　　　　　        显示提交历史（many useful options to be learned）
git branch [branch]　　　　　　　　　　　　        显示/新建分支
git branch -d/-D　　　　　　　　　　　　　　       删除分支（d表示“在分支合并后删除分支”，D表示无论如何都删除分支）
git show-branch
git checkout <branch>　　　　　　　　　　　        切换分支（分支未commit无法切换）
git merge <branch>　　　　　　　　　　　　         合并分支
git merge == git pull .
git show <branch | commit | tag | etc>　　　      显示对应对象的信息
git grep <rep> [object]　　　　　　　　　　　     （在指定对象（历史记录）中）搜索　　　　　　　　
git cat-file 　　　　　　　　　　　　　　　　       查看数据
git cat-file <-t | -s | -e | -p | (type)> <object>        type can be one of: blob, tree, commit, tag
git ls-files [--stage]　　　　　　　　　　　　　 show information about files in the index and the working tree（实际是查看索引文件）
git watchchanged <since>..<until>　　　　　　  显示两个commit（当然也可以是branch）的区别
git remote [-v]　　　　　　　　　　　　　　    　显示远程仓库，加-v选项可显示仓库地址
git remote add <repo_name> <url>　　　　　  　　添加远程仓库，repo_name为shortname，指代仓库地址
git remote rename <old_name> <new_name>  　　  更名
git remote rm <repo_name>　　　　　　　　　　   删除远程仓库
git remote show <repo_name>　　　　　　　　　   查看远程仓库信息
git remote fetch <repo_name>　　　　　　　　　  从远程仓库抓取数据（并不合并）
git pull <repo_name> <branch_name>　　　　　　 拉去数据并合并到当前分支
git push <repo_name> <branch_name>　　　　　   推送指定分支到指定仓库
git fetch <repo_name> <branch_name>[:<local_branch_name>]　　　　拉去数据，未合并
GIT_DIR:              如果指定了那么git init将会在GIT_DIR指定的目录下创建版本库
GIT_OBJECT_DIRECTORY: 用来指示对象存储目录的路径。即原来$GIT_DIR/objects下的文件会置于该变量指定的路径下
HEAD:                 表示最近一次的 commit。
MERGE_HEAD:           如果是 merge 产生的 commit,那么它表示除 HEAD 之外的另一个父母分支。
FETCH_HEAD:           使用 git-fetch 获得的 object 和 ref 的信息都存储在这里,这些信息是为日后 git-merge 准备的。
HEAD^:          表示 HEAD 父母的信息
HEAD^^:         表示 HEAD 父母的父母的信息
HEAD~4:         表示 HEAD 上溯四代的信息
HEAD^1:         表示 HEAD 的第一个父母的信息
HEAD^2:         表示 HEAD 的第二个父母的信息
COMMIT_EDITMSG: 最后一次 commit 时的提交信息。
```
