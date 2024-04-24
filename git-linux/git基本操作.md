![image](img1.png) 
### 本地提交与修改
- `git add <file1 file2> ...` 将指定文件加入index，表明要跟踪他们
- `git status` 查看工作区状态，如果工作区index所指向的文件与仓库中的相比有变化，会给出具体提示。
- `git diff` 查看工作区详细的变化
- `git commit <file> [-a] [-m "xxx"]` 提交index中指定文件到本地仓库，-a表示提交index中所有文件，-m添加提交注释
- `git rm <file>` 将文件从工作区和index区删除
- `git reset` `git restore <file>` 回退版本并忽略修改。对某个文件修改后如果想要撤销，则应先reset，然后restore。
- `git mv` 等价于`mv`
- `git checkout --<file>` 将file加入index后，如果想撤销修改，也可以使用此命令
### 日志

`git log` 查看提交日志
`git blam <file>` 按行查看指定文件的修改历史
`git log --graph` 以树型方式显示各分支提交历史
### 分支管理
- `git branch` 列出所有分支
- `git branch <branchname>` 创建分支
- `git branch -d <branchname>` 删除分支
- `git switch -c <branchname> | git checkout [-b] <branchname>` 切换分支，-b, -c选项，如果分支不存在，则创建新分支并切换

### 合并操作
##### 分支合并
两个分支，如果对某个文件的 **同一个地方** 都进行了修改，然后各自提交，之后如果要合并两个分支(如temp->mster，temp合并到master分支)， git会不知道选择哪个修改，便会发生合并冲突，此时，需要手动编辑冲突文件，解决冲突。之后 `git add .` 、 `git merge -- continue` 继续合并即可。

- `git merge temp` 将 `temp` 分支合并到当前分支

### 远程管理
- `git push <remote> <branch>` 将当前分支推到远程仓库的指定分支
- `git pull <remote> <branch>` 将远程仓库的指定分支拉到本地
- `git fetch <remote>` 成功抓取后需要合并，才可以到工作区：`git merge [<remote>/]<branch>` 表示将\[远程仓库\<remote>的]\<branch>分支合并当本地当前分支
   - `--allow-unrelated-histories` 在合并阶段，加入这个选项和将无关历史合并到一起
- `git clone -b <branchname> <git address>` 通过选项-b可以指定远程仓库的指定分支
- `git remote show [origin]` 查看远程仓库列表或某个远程仓库的详细信息
### 仓库配置 
- `git config -e [--global] [--system]` 打开配置文件并编辑，默认是当前仓库的配置文件，即`Dir/.git/config`，只影响当前仓库；`--global` 选项则打开用户级配置文件，即`username/.gitconfg`，影响当前用户的所有仓库；`--system`选项打开系统及配置文件，即`/etc/gitconfg`，影响当前系统上的所有git仓库
- `git config -l | --list` 列出当前仓库配置，从上到下依次列出系统级、用户级、仓库级的配置文件，其中，仓库级配置会覆盖用户级和系统及配置，用户级配置会覆盖系统及配置，总之，影响范围越小的配置优先级越高


- `git config --system core.editor "vim"` 配置默认编辑器
##### 添加远程仓库
`git remote add <name> <addr>` \<name> 是你给这个仓库气的名称，取决于你，\<addr>是远程仓库的地址。

##### 凭据管理
- 对于 `public repo` `push` 操作需要密码
- 对于 `private repo` `clone`, `pull`, `push` 操作均需要密码
自动化操作免登录：使用git的 `credential.helper` 配置。
- `store` 将用户名和口令以明文方式储存在 `~/git-credentials`当中
- `cache` 将用户名和口令暂时存在内存中，15分钟后消失
- 使用凭据管理工具： `windows credential manager`, `git-gredential-manager`等等。
在Windows中，身份验证由 `windows credential manager` 管理。
在其他平台，可以下载凭据管理器，比如 `git-credential-manager` 等。

github 已移除口令（密码）验证方式，转而使用 token 方式，在使用 `store` 或 `cache` 时，如果给的是用户口令（密码），将失败。

- 对于`store`配置格式： `https://<username>:<tokens>@github.com`
### gitignore不起作用问题修复
- 原因：当文件已被跟踪后，如果想要ignore，git将依然不会忽视，除非清楚缓存：
``` shell
git rm [-r] cached <file>
# -r 用于删除目录
```
### gitignore 配置
- `!file.xxx`  `!` 表示文件被排除在规则之外

### 加速访问GitHub
- 镜像代理
    - eg. “git clone [https://mirror.ghproxy.com/https://github.com/Fenlyin/MihoyoBBSTools.git”](https://mirror.ghproxy.com/https://github.com/Fenlyin/MihoyoBBSTools.git%E2%80%9D)
- 常用的镜像网站：
    1. [https://mirror.ghproxy.com/](https://mirror.ghproxy.com/)
    2. [https://gitclone.com/](https://gitclone.com/)
    3. [https://cnpmjs.org/](https://cnpmjs.org/)
    4. [https://shrill-pond-3e81.hunsh.workers.dev/](https://shrill-pond-3e81.hunsh.workers.dev/)
    5. [https://fastgit.org/](https://fastgit.org/)

