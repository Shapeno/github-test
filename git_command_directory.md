# git 个人的命令汇总

韩鹏

## 本地仓库管理命令

| 命令                                                         | 意义                                      |
| ------------------------------------------------------------ | ----------------------------------------- |
| `$ git config --global user.name "Peng Han"`                 | 初始设置，设置用户名                      |
| `$ git config --global user.email frozenr@163.com`           | 初始设置，设置邮箱                        |
| `$ git config --list`                                        | 查询配置信息                              |
| `$ git init`                                                 | 初始化仓库                                |
| `$ git clone`                                                | 克隆现有的仓库                            |
| `$ git status` , 可添加`-s` 后缀查看简览                     | 查询仓库的当前状态                        |
| `$ git add filename`                                         | 开始跟踪新文件，或者提交到暂存区          |
| `$ git commit -m "prompt message"`                           | 提交跟新，并撰写提示信息（提交前需要add） |
| `$ git commit -a`                                            | 不适用暂存区，一步提交                    |
| `$ git rm filename`                                          | 在仓库中删除文件（之后需要commit）        |
| `$ git rm --cached filename`                                 | 在暂存区中删除文件                        |
| `$ git log`, 可添加`-2` 后缀查看近两次操作；或者`--since=2.weeks` 等限制条件 | 查看提交历史                              |

状态简览：

1. ??: 新添加的未跟踪文件
2. A: 新添加到暂存区的文件
3. M: 修改过的文件
4. 右侧的M: 文件被修改了但是还没有放入暂存区
5. 左侧的M: 文件被修改了并被放入暂存区

## 远程仓库管理

1. 首先注册一个gitlab账号（gitlab是没有桌面级GUI的）。

2. 在 git bash 中检验是否安装ssh：`$ ssh` 。（一般都是有的）结果如下所示。

![ssh_exist](.\ssh_exist.png)

3. 在 git bash 中使用`ssh-keygen -t rsa`生成密钥，之后要输入三个 `enter` 。对于windows 10 而言，密钥生成在user/.ssh目录下。将公钥上传至gitlab即可完成电脑的认证。

| 命令                                                    | 意义                                                         |
| ------------------------------------------------------- | ------------------------------------------------------------ |
| `$ git remote add <short-name> <url>`                   | 添加远程仓库                                                 |
| `$ git clone <url>`                                     | 克隆远程仓库                                                 |
| `$ git remote`                                          | 查询远程仓库的缩写名称                                       |
| `$ git fetch [remote name]`                             | 获取克隆或抓取后的新推送的所有工作（不会合并）               |
| `$ git pull`                                            | 获取服务器上的数据，并自动尝试合并到当前的分支（只更新文件名，而不是文件内容） |
| `$ git push [remote-name] [branch-name]`                | 将本地的文件推送到服务器上（必须首先获得写入权限，或之前没有人推送过；如果有人推送了，就需要先fetch并合并后才能上传） |
| `$ git remote rename [old-short-name] [new-short-name]` | 远程仓库的重命名                                             |
| `$ git remote rm`                                       | 移除远程仓库                                                 |
| `$ git tag`                                             | 列出标签                                                     |
| `$ git tag -a v1.0 -m 'description'`                    | 附注标签，如去掉`-a`和`-m`，则为轻量标签                     |
| `$ git push origin [tagname]`                           | push命令显式推送标签                                         |

## 分支操作

git的分支类似于数据结构“树”。每一次提交（除了第一次）都有一个父对象，并用一个指针指向他。

git的默认分支是“master”，但它并不特殊。

| 命令                                           | 意义                                                         |
| ---------------------------------------------- | ------------------------------------------------------------ |
| `$ git branch`                                 | 查看分支情况（`-v` 可以查看每个分支的最后一次提交）          |
| `$ git branch [branch-name]`                   | 创建一个新的分支（不会切换到新的分支）                       |
| `$ git branch --oneline --decorate`            | 查看分支当前所指对象的日志                                   |
| `$ git log --oneline --decorate --graph --all` | 以非常神奇的方式显示所有分支的日志                           |
| `$ git checkout [branch-name]`                 | 切换分支到 [pointer-name]（`-b`可以新建+切换）               |
| `$ git merge [branch-name]`                    | 将当前分支合并到目标分支                                     |
| `$ git branch -d [branch-name]`                | 删除分支（注意，没有合并的分支没法删除）                     |
| `$ git branch --merged`                        | 查看已经合并的分支（之后就可以删了），同理`no-merged` 可以查看没有合并的 |
| `$ git remote add`                             | 添加一个远程仓库                                             |



注意，使用`checkout`指令会完成两件事情，一是使head指针指向目标，而是将目录恢复成目标指针所指向的快照内容。当然，你完全可以在使用一次`checkout`来返回。另外，如果当前的工作目录和暂存区里存在没有提交的修改，`checkout`指令可能会被阻止。

## 小技巧

git bash 中复制粘贴：https://blog.csdn.net/nishiwodebocai21/article/details/72510341

别名：`$ git config --global alias.last 'log -1 HEAD'`，之后输入`$ git last`就可以查看最后一次提交了。

## 学习中的疑问

1. fetch指令
2. 分支操作在远程仓库中的应用
3. 如何上传一个工程文件
4. ignore文件
5. tag怎么附在commit后面（我只知道怎么附在push后面）（用的少）
6. merge 好像就没有成功过（gitlab Merge Request）
7. 远程仓库

## 请各位做的事情

思考自己手头正在做的事情和已经完成的事情，他们应当建立成工程，还是工程的分支呢？

无论是建立成工程，还是工程的分支，请各位一定要把自己的程序上传上去，并且附有一定的注释。