#### 目录

[Git基本概念](#git-concept)

[常见命令](#common-command)

[版本回退](#version-back)

[撤销文件的修改](#undo-file-change)

[分支](#branch)

[解决冲突](#resolved-conflict)

[子模块](#submodule)

[生成 SSH 公钥](#generate-publick-key)

#### <a name="git-concept"></a>Git基本概念

- 工作区(Working Directory)

> 在电脑里面能够看到的目录

- 版本库（Repository）

> 工作区又一个隐藏文件夹`.git`, 叫做Git的版本库。<br>
> Git的版本库存放很多东西， 其中比价重要的就是stage（或者index) 的暂存区， 还有Git为我们自动创建的第一个分支`master`， 以及指向`master`的指针`HEAD`。

![](https://cdn.liaoxuefeng.com/cdn/files/attachments/001384907702917346729e9afbf4127b6dfbae9207af016000/0)

- 远程仓库区(Remote)

> 代码托管的服务器


#### <a name="common-command"></a>常见命令

1. `git clone <remote-url>` 克隆某个远端仓库
2. `git add <file path>` 把工作区中修改的文件添加到暂存区
3. `git commit -m 'xx'` 把暂存区中的内容提交到当前分支
4. `git pull` 拉取远端代码，并自动合并
5. `git push origin master` 当前分支(默认是`master`分支)代码推送到远端仓库

#### <a name="version-back"></a>版本回退

- `git reset --hard HEAD^` 把当前分支指向上一个版本，
- `git reset --hard HEAD~100`, 把当前分支回退往上100个版本， 
- `git reset --hard xxxx`, 把当前分支指到指定版本

#### <a name="undo-file-change"></a>撤销文件的修改
1. 文件没有添加到暂存区(没有使用`git add `)
	- `git checkout -- <file path>` 把文件在工作区的修改全部撤销，这里有两种情况：
		- 一种是自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
		- 一种是已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

2. 文件已经添加到暂存区(使用`git add `， 尚未使用`git commit`)
	- `git reset HEAD <file>` 把暂存区的修改撤销掉（`unstage`），重新放回工作区
	- `git checkout -- <file path>` 撤销工作区中文件的修改

3. 暂存区内容已经提交到当前分支(使用`git commit`)
	- `git reset HEAD^` 回退当前提交到工作区 
	- `git checkout -- <file path>` 撤销工作区中文件的修改 

#### <a name="branch"></a>分支

- 查看分支：`git branch`
- 创建分支：`git branch <name>`
- 切换分支：`git checkout <name>`
- 创建+切换分支：`git checkout -b <name>`
- 合并某分支到当前分支：`git merge <name>`
- 删除分支：`git branch -d <name>`

#### <a name="resolved-conflict"></a>解决冲突
`Git` 用`<<<<<<<`，`=======`，`>>>>>>>`标记出冲突的内容， 手动解决之后，先`git add `, 再`git commit`即可。

#### <a name="submodule"></a>子模块

克隆带子模块的项目
> git clone xxx

默认会包含子模块目录，但是其中没有任何文件。<br>
你必须运行两个命令：<br>
`git submodule init` 用来初始化本地配置文件，而 `git submodule update` 则从该项目中抓取所有数据并检出父项目中列出的合适的提交。

> git clone --recursive xxx

自动初始化并更新仓库中的每一个子模块

#### <a name="generate-publick-key"></a>生成git ssh 公钥

> 1. SSH 公钥默认储存在账户的主目录下的 ~/.ssh 目录

> 2. 有 .pub 后缀的文件就是公钥，另一个文件则是密钥

> 3. 假如没有这些文件，或者干脆连 .ssh 目录都没有，可以用 `ssh-keygen` 来创建

#### 参考资料
[git-book](https://git-scm.com/book/en/v2)

[git 教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000)

[生成 SSH 公钥](https://git-scm.com/book/zh/v1/服务器上的-Git-生成-SSH-公钥)