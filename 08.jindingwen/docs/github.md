### "快答"系统协同开发github使用:

1. fork主仓库'kuaida/kda'到自己的github仓库'jindwer/kda'(这里默认会是master分支)
2. 在本地电脑的一个文件夹中将自己的仓库'jindwer/kda'克隆下来
```
> git clone https://github.com/jindwer/kda.git
```
之后会在当前文件夹建立'kda'文件夹
3. 进入'kda'文件夹，查看分支情况
```
> git branch -av
```
```
master                    hash值
remotes/origin/HEAD       -> origin/master
remotes/origin/master     hash值
```
4. 添加主仓库'kuaida'为本地的一个远程分支'updateteam'，并依据此远程分支创建一个本地分支'update'
```
/* 添加远程 */
> git remote add updateteam https://github.com/kuaida/kda.git
```
```
/* 拉取远程内容 */
> git fetch updateteam
```
```
/* 创建本地分支 */
> git checkout -b update updateteam
```
```
> git branch -av
  master                    aed4ab6
 * update                    d0b881c
  remotes/origin/HEAD       -> origin/master
  remotes/origin/master     e81a5b0
  remotes/updateteam/master d0b881c
```
5. 根据'origin/master'远程分支创建中间本地分支'dev'
```
> git checkout -b dev origin/master
```
```
> git branch -av
  * dev                       aed4ab6
  master                    aed4ab6
  update                    d0b881c
  remotes/origin/HEAD       -> origin/master
  remotes/origin/dev        aed4ab6
  remotes/origin/master     e81a5b0
  remotes/updateteam/master d0b881c
```
6. 切换到master分支开发，完成开发工作，之后追踪新内容，最后将新内容放入到暂存区域
```
> git checkout master
do somethings
> git add .
> git stash save name
```
7. 切换到'update'分支，拉取updateteam的数据，并更新update本地分支
```
> git checkout update
> git fetch updateteam
> git pull
```
8. 切换到'dev'分支，并合并update分支
```
> git checkout dev
> git merge update
```
9. 在'dev'分支释放暂存区中的内容，并追踪新内容，然后提交，最后推送到自己的远程仓库的'dev'分支
```
/* 可能需要手动解决冲突，一般是删除自己的相关冲突代码来解决 */
> git stash pop stash@{0}
> git add .
> git commit -a -m "message"
> git push -u origin dev
```
10. 在自己的github仓库中的'dev'分支上'create pull request'给主仓库的管理者，等待管理者的审查，合并自身的工作到主仓库
11. 切换到'master'本地分支，合并本地分支'dev'
12. 之后的开发流程循环6~12步骤
