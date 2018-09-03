### Git ###

#### Git安装后初始化配置 ####

1. 设置全局用户名、用户密码

   ```
   $ git config --global user.name '[your name]'
   $ git config --global user.email [your email address]
   ```

2. 设置特定项目的用户名与邮件，在该项目目录下执行：

   ```
   $ git config user.name '[your name]'
   $ git config user.email [your email address]   
   ```

3. 设置默认文本编辑器（未配置，Git将使用操作系统默认文本编辑器，通常为Vim）

   ```
   $ git config --global core.editor [editor name]
   ```

#### Git功能查询操作 ####

1. 版本号查询

   ```
   $ git --version
   ```

2. 查看配置信息

   + 列出所有Git当时可找到的配置 （重复变量名为不同文件中的同一配置）

     ```
     $ git config --list
     ```

   + 查看Git某一项配置

      ```
      $ git config <key>
      
      Eg:$ git config user.name
      ```

3. Git帮助，查询命令手册

   + 查询Git拥有的命令列表，以及每个命令的简介

     ```
     $ git --help
     ```

   + 查询某个命令的具体介绍

     ```
     $ git help <verb>
     $ git <verb> --help
     $ man git-<verb>
     ```


4.查看远程仓库，列出指定的每一个远程服务器的简写

```
git remote
```

7、查看当前分支列表

```
$ git branch
```



#### Git仓库的创建、获取 ####

##### 1. 在现有项目或目录下导入所有文件到Git中 #####

1. 初始化仓库

   ```
   $ git init
   ```

2. 跟踪指定文件

   ```
   $ git add [file]
   ```

3. 提交到本地仓库

   ```
   $ git commit -m 'commit message'
   ```


##### 2.从服务器clone一个现有的Git仓库 #####

    Git clone 命令将拉取默之配置下远程Git的每一个文件的每一个版本；此时每个文件都属于已跟踪未修改状态

1. 默认使用远程仓库名称：

   ```
   $ git clone [url]
   ```

2. 自定义本地仓库名：

   ```
   $ git clone [url] [new name]
   ```



#### Git文件状态变化查看 ####

1. 查看文件当前状态

   ```
   $ git status
   ```

   查看紧凑版状态输出

   ```
   $ git status -s/--short
   ```

2. 查看文件具体修改

   + 查看尚未暂存的改动

     ```
     $ git diff
     ```

   + 查看已暂存的改动

     ```
     $ git diff --cached
     $ git diff --staged //版本>1.6.1
     ```

3. 查看提交历史

   ```
   $ git log <verb>
   ```

   参数 `<verb>`（可叠加使用）：

   + `无参`

     按提交时间列出所有更新

   + `-p`

     显示每次提交的内容差异

   + `-[number]`

     最近number次提交

   + `—stat`

     显示每次就提交的简略统计信息

   + `--pretty=[verb]`

     指定格式展示提交信息

   + `--since`

   + `--until`



#### 文件的状态、Git仓库的更新 ####

1、工作目录中文件状态：

* 已跟踪（tracked/staged)：被纳入版本控制的文件，在上一次快照中有记录，未来状态：未修改/已修改/已暂存

* 未跟踪 (untracked)：除了已跟踪的文件外，均属于未跟踪文件，既不存在上次快照中，也不存在于暂存区

* 已修改（modified):自上次暂存/提交后（或者初次clone某个仓库后），对文件作出修改、编辑，Git会将该文件标记为已修改文件


2、添加内容至下一次提交（不是将文件放入项目）

```
$ git add [file]/*      //单个文件/所有文件
```

      file：文件或者目录的路径，若为目录路径，将递归跟踪该路径下所有文件

+ 跟踪新文件（未跟踪）

       状态变化：untracked==>tracked、staged

+ 暂存已修改的文件（已跟踪）

		状态变化：tracked==>modified==>staged

+ 将合并时有冲突的文件标记为已解决状态

        **状态变化：**



![lifecycle](https://git-scm.com/book/en/v2/images/lifecycle.png)

[Figure 1.文件状态变化][figure]  



[figure]: https://git-scm.com/book/zh/v2/Git-%E5%9F%BA%E7%A1%80-%E8%AE%B0%E5%BD%95%E6%AF%8F%E6%AC%A1%E6%9B%B4%E6%96%B0%E5%88%B0%E4%BB%93%E5%BA%93	"点击查看图片来源"



3. 提交更新

*建议：每次提交前运行 `$git status` 查看工作区是否有需要提交的修改还未暂存，未暂存内容将只保留在本地磁盘，不被纳入本次提交*

+ 将提交信息与命令放在同一行（常用）

  ```
  $ git commit -m "commit message"
  ```

+ 打开编译器编辑提交信息

  ```
  $ git commit
  ```

> tip:提交记录的是放在暂存区的快照，而不是文件本身；任何未暂存的修改不会受到影响



4. 跳过使用暂存区直接提交,所有已跟踪的文件都会被暂存起来一起提交

5. ```
   $ git commit -a -m "commit message"
   ```



#### 撤销操作 ####

1、重新提交，将取代上一次的提交结果

```
$ git commit --amend
```

2、取消暂存某个文件

```
$ git reset HEAD <file name>
```

3、撤销对文件的修改，还原为上次提交/初始化时的状态（该操作不可修复！！！）

```
git checkout -- <file>
```



#### Git分支 ####

1、创建新分支

```
$ git branch [branch-name]
```

2、切换分支

```
$ git checkout [brabch-name]
```

3、新建分支的同时切换到该分支

```
$ git checkout -b [branch-name]
```

4、合并分支（假设当前在`develop`分支，合并到`master`分支）

```
$ git checkout master
$ git merge develop
```

5、删除分支

```
$ git branch -d [branch-name]
```

6、查看合并冲突

```
$ git status

```

7、查看当前分支列表

```
$ git branch
```



#### 远程仓库 ####

1、添加远程仓库（默认分支名`origin`，默认分支`master`）

```
git remote add <shortname> <url> 
```

2、从远程仓库抓取（所有分支）数据，需手动合并

```
$ git fetch [remote-name/shortname]
```

3、从远程仓库拉取已跟踪远程分支并自动合并到当前分支

```
$ git pull
```

4、推送到远程仓库

```
$ git push [remote-name] [branch-name]
```

注：若当前远程分支有他人推送记录，必须先将最新变动拉取到本地合并

5、修改远程仓库名称

```
$ git remote rename [oldname] [newname]
```

6、移除远程仓库

```
$ git remote rm [remote-name]
```

7、查看当前仓库

```
$ git remote
```

8、删除origin远程分支

```
$ git push origin --delete [branch-name]
```



#### 忽略文件 .gitignore ####

      不希望加入Git管理，也不希望总是出现在未跟踪文件列表的文件，例如一些临时文件，日志，依赖包等

方法：创建`.gitignore`文件，列出需要忽略的文件模式

eg: 

```
$ cat .gitignore    //创建.gitignore文件
*.[oa]				//忽略所有以.o或.a结尾的文件
*~					//忽略所有以波浪符(~)结尾的文件
```

最好在项目开始就创建`.gitignore`文件，避免以后提交无用文件

`.gitignore`文件格式如下：

+ 所有空行或者以 `＃` 开头的行都会被 Git 忽略。
+ 可以使用标准的 glob 模式匹配。
+ 匹配模式可以以（`/`）开头防止递归。
+ 匹配模式可以以（`/`）结尾指定目录。
+ 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（`!`）取反。



#### 移除文件 ####

步骤:

1. 从工作目录中删除该文件（保证此后不会出现在未跟踪文件列表）

2. 从暂存区（已跟踪文件清单）中移除

3. 提交

    

删除情景：

1. 工作区无变化，从仓库删除，本地不保留：删除暂存区文件并提交

   ```
   $ rm [file]
   $ git rm [file]
   $ git commit -m "delete file"
   ```

1. 工作区已修改，但是未暂存，从仓库删除，本地不保留：`-f` 强制删除暂存区同时删除工作区(*防止普通删除操作将未暂存的文件删除*)

   ```
   $ rm [file]
   $ git rm -f [file]
   $ git commit -m "delete file"
   ```

2. 从仓库删除，本地保留：删除暂存区变动，保留工作区文件（*适用于将文件添加到`.gitignore`*）

   ```
   $ rm [file]
   $ git rm --cached [file]
   $ git commit -m "delete file"
   ```



##### 移动文件（更改文件名） #####

```
$ git mv file_old file_new
```

以上代码相当于执行：

```
$ git mv file_old file_new
$ git rm file_old
$ git add file_new
```

使用其他工具批量改名时要记得删除老的文件名，再添加新的文件名

```
$ rm [file]
$ git rm [file]
$ git commit -m "delete file"
```



####  ####

#### Git名词解释####

1. modified：已修改，在工作目录（Working Directory）对文件进行了修改，但还没有保存到工作目录中；
2. Staged：已暂存，对已修改的文件的当前版本做了标记，保存快照以供下次提交；
3. Commited:已提交，文件已经保存在本地仓库；
4. Working Directory：工作目录，项目某个版本独立提取出来，放在磁盘以供使用修改的文件；
5. git directory(Respository)：Git仓库目录，Git用来保存项目元数据和对象数据哭的地方，为Git核心；



