# GIT 的使用

| Function | Action                                | Syntax                                           |
| -------- | ------------------------------------- | ------------------------------------------------ |
|          | 推送分支                              | git push origin main                             |
|          | 推送其他分支                          | git push origin <name>                           |
|          | Check the full output of remote URL   | git remote show origin                           |
| 分支管理 | 查看分支                              | git branch                                       |
|          | check the current branch              | git branch --show-current                        |
|          | See all remote branch names           | git branch -r                                    |
|          | See all local and remote branch names | git branch -a                                    |
|          | 创建分支                              | git branch <name>                                |
|          | 切换分支                              | git checkout <name> 或者 git switch <name>       |
|          | 创建+切换分支                         | git checkout -b <name> 或者 git switch -c <name> |
|          | 合并某分支到当前分支                  | git merge <name>                                 |
|          | 删除分支                              | git branch -d <name>                             |
|          |                                       |                                                  |



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



## 基础步骤 Basic steps to initilising a Git repository

定位到所在文件夹

1. 将本地仓库初始化，命令：```git init``` This command will write a .git directory.
2. `git status` 查看文件状态
3. `git add `文件列表 追踪文件
4. `git commit -m 提交信息` 向仓库提交代码例如`git commit -m "initial comit"`
5. `git log` 查看提交记录
6. 将你需要的项目从github或者服务器上克隆下来，命令：`git clone url`

### 撤销 Undo

- 用暂存区中的文件覆盖工作目录中的文件：`git checkout -- 文件名` 不加 `-- 文件名`则覆盖全部文件
- 将文件从暂存区中删除：`git rm --cached 文件名`
- 将git仓库中指定的更新记录恢复出来，并且覆盖暂存区和工作目录：` git reset --hard commitID`

### 删除文件

1. 在文件管理器中删除文件或者使用`rm <file>`
2. 可使用`git status`查看文件状态
3. 使用`git rm <file>`移除文件，并且`git commit -m "message"`提交修改

#### 恢复版本库中误删文件

`git checkout -- <file>`

#### 不追踪文件/文件夹

[忽略文件 - GitHub 文档](https://docs.github.com/zh/get-started/getting-started-with-git/ignoring-files)

- 如果是新文件：

  创建.gitignore文件，加入文件/文件夹路径

- 如果是之前已经commit的文件，需要先做一步

  ```bash
  git rm --cached <file>
  ```

##### .gitignore 文件模版

1. 不追踪所有临时文件

```bash
# Ignore all files in a directory named "temp"
temp/

# Ignore all files with a specific extension, for example .tmp
*.tmp

# Ignore files in a specific directory with a particular extension
directory_name/*.tmp

# Ignore all files with tilde (~) at the end (often used by text editors)
*~

# Ignore files with a dollar sign ($) at the end (sometimes used for temporary files)
*$

# Ignore swap files created by Vim editor
*.swp

# Ignore .DS_Store files (macOS)
.DS_Store

# Ignore Thumbs.db files (Windows)
Thumbs.db

# Ignore desktop.ini files (Windows)
desktop.ini
```

## Commit Message

1. 小于50个字符 A short singe-line summary (less than 50 characters)

2. 可选添加空白行或者完整描述 Blank line and more complete description

3. 保证一行小于72个字符 Keep each line to less than 72 characters

4. 用现在时态而不是过去时态 Present tense rather than past tense

   'Fix for a bug' / 'Fixes a bug' not 'Fixed a bug'

   '[css, js]'

   'bugfix:'

   '#38405-'

5. If the commit has not been pushed, you can amend the commit message by:

   ```bash
   git commit --amend --only -m 'xxxxxxx'
   ```

   

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
`git log --grep="Init"`

Git status

`git status`

当你文件夹中新建了新文件时，使用git status查看untracked files或者uncommited files.

#### Find the detail of last commit

```bash
git show
```



### 远程仓库

C:\Users\\<username>\.ssh目录下查看是否存在`id_rsa`和`id_rsa.pub`这两个文件，如果没有，在terminal中输入`ssh-keygen -t rsa -C "youremail@example.com"`生成

你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容：

#### 添加远程仓库 Add a local repository to Github

1. 在GitHub上创建一个远程仓库<github repo name>

2. `git init` first at the local directory

3. 在本地的仓库<github repo name>下运行

   `git remote add origin https://github.com/<github username>/<github repo name>.git`

4. Verifing the new remote URL

   `git remote -v`

`git branch -M main`

`git push -u origin main`

从现在起，只要本地作了提交，就可以通过命令：`git push origin main`

#### 从远程仓库克隆

1. 登陆GitHub，创建一个新的仓库Web_Mapping：

   Initialize this repository with a README，这样GitHub会自动为我们创建一个README.md文件。创建完毕后，可以看到README.md文件：
   `git clone git@github.com:BayiLi081/Web_Mapping.git`
   
#### 与远程仓库同步

##### 查看现有branch

```bash
git branch -a
```

运行结果为

```
* main                                                           remotes/origin/main 
```
将目前的branch设置为追踪远程仓库origin中的main branch

```
git branch --set-upstream-to=origin/main
```

运行```git pull```与远程同步



这条语句将删除您在本地的陈旧分支。当分支在远程存储库中被删除时，陈旧分支存在，但仍然存在于您的本地副本中。

```
git fetch --prune origin
```



## 分支管理

1. 创建dev分支，然后切换到dev分支 (`git checkout`命令加上`-b`表示创建并切换)

   `git switch -c dev` or `git checkout -b dev`

2. 使用`git branch`命令查看当前分支:

   当前分支前会标一个`*`

3. 对当前分支修改后提交代码为（以修改文件为readme.md为例）：

   `git add readme.md`

   `git commit -m "branch test"`

4. 切换为main

   `git switch main` or `git checkout main`

5. 把dev分支的工作成果合并到main分支上

   `git merge dev`

6. 删除dev分支:

   `git branch -d dev`

#### 清理commit历史 Clean commit history (危险操作)

1. 在本地仓库中删除 .git 文件夹

2. initiate the repo

   ```
   git init
   ```

3. 重新链接远程github仓库

   ```
   git remote add origin git@github.com:user/repo
   ```

4. If the new created branch name is main, continue; if 新创建的branch是master，重命名为main (和云端保持一致)

   ```
   git branch -m main
   ```

5. 重新commit

   ```
   git add -A
   git commit -m "commit message"
   ```

6. 强制更新github仓库即可

   ```
   git push -f origin main
   ```

## Issues and their solutions


#### Ignore local modifications

1. First fetch all changes:

    ```
    git fetch --all
    ```

2. Then reset the main:

    ```
    git reset --hard origin/main
    ```

3. Pull/update:

    ```
    git pull
    ```

### Merges files

1. Rebase all the changes

   ```
   git pull --rebase
   ```

2. Use `git mergetool` to compare the difference between branches

   ```
   git mergetool --tool=vimdiff
   ```

   

## References

1. [详解N个git合代码经典操作！ (qq.com)](https://mp.weixin.qq.com/s?__biz=MzUwOTg0MjczNw==&mid=2247517067&idx=1&sn=3c65521304f75976f10d9d09be774179&chksm=f90ec7d5ce794ec3386d8eaf3f4c0ff77dabc2c501104371d5a2c7af451429c4d2629797e0e2#rd)
