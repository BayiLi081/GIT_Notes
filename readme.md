# GIT 的使用

- Git的结构: Repository (仓库) + Staging index (暂存区) + Working (工作目录)
  1. Working --git add files--> Staging index
  2. Staging index --git add files--> Repository
  3. Repository --checkout--> working



## 配置 GIT Basic Git Configuration

- 系统 System

/etc/gitconfig

Program Files\Git\etc\gitconfig

```git config --system```

- 用户 User

~/.gitconfig

$Home\\.gitconfig

```git config --global```

- 项目 Project

my_project/.git/config

```git config```



```git config --global user.name "Bayi Li"```

```git config --global user.email "barryli081@gmail.com"```

```git config --list```

或者 or

```git config user.name	```

```git config --global core.editor "notepad"```

```git config --global color.ui true```

### Git Auto-Completion (Mac and Linux Only)

https://www.linkedin.com/learning/git-essential-training-the-basics/git-auto-completion?autoAdvance=true&autoSkip=true&autoplay=true&resume=false&u=0

### Git Help

```git help```

```git help log```



## 基础步骤 Basic steps to start a project

定位到所在文件夹

1. 将本地仓库初始化，命令：```git init``` This command will write a .git directory.
2. `git status` 查看文件状态
3. `git add `文件列表 追踪文件
4. `git commit -m 提交信息` 向仓库提交代码
5. `git log` 查看提交记录
6. 将你需要的项目从github或者服务器上克隆下来，命令：`git clone url`

### 撤销 Undo

- 用暂存区中的文件覆盖工作目录中的文件：`git checkout -- 文件名` 不加 `-- 文件名`则覆盖全部文件
- 将文件从暂存区中删除：`git rm --cached 文件名`
- 将git仓库中指定的更新记录恢复出来，并且覆盖暂存区和工作目录：` git reset --hard commitID`

## Commit Message

1. 小于50个字符 A short singe-line summary (less than 50 characters)

2. 可选添加空白行或者完整描述 Blank line and more complete description

3. 保证一行小于72个字符 Keep each line to less than 72 characters

4. 用现在时态而不是过去时态 Present tense rather than past tense

   'Fix for a bug' / 'Fixes a bug' not 'Fixed a bug'

   '[css, js]'

   'bugfix:'

   '#38405-'

### View Commit Log

```git log```

```git help log```

显示近五条 show the most recent 5 commit log

```git log -n 5```

根据时间显示 show commit log with certain time

```git log --since=2019-01-01```

```git log --until=2019-01-01```

```git log --author="Kevin"```

```git log --until=2020-09-10 -n 2``` will output the log for the last two commits that happened before September 10, 2020.

```git log --since=2019-03-01 --until=2019-03-31 --author="Karen" --grep="refactor"``` will output the log for all of Karen's commits labeled "refactor" during March 2019.

用正则表达式全局搜索commit log
```git log --grep="Init"```







