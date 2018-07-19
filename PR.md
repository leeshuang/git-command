### Git ###

#### GitHub Pull Request ####

1.`Fork git-command`  到自己的GitHub目录

    访问：https://github.com/leeshuang/git-command，点击fork，即可在自己的GitHub目录发现git-command项目。

2.`Clone` 代码到本地

    git clone https://github.com/leeshuang/git-command.git

 
3.设置代码的 `UpStream` 原始目录，此处应使用项目原 `git` 地址

    cd git-command 
    git remote add upstream https://github.com/leeshuang/git-command.git

4.在本地获取最新的 `UpStream` 版本

    cd git-command
    git fetch upstream
    git checkout master
    git rebase upstream/master

5.本地项目创建新分支 `develop` 并提交修改

    git add .
    git commit -m 'some messages'
    git push origin develop
 