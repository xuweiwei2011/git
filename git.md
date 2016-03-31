
**gitlab地址：http://192.168.0.2**
> 项目地址：<br>
>www 
>git@192.168.0.2:root/www.git<br>
>cms2<br>
>git@192.168.0.2:root/cms2.git<br>
>其他项目地址参考gitlab<br>


**说明**
>此处只整理了部分常用命令,后续工作中遇到了其他问题再更新，另外命令详细用法及一些高级命令可使用--help命令获取<br>
>例如查看git branch 详细用法<br>
>`git branch --help` <br>
>以下带’*‘的部分为常用命令


**初始配置**
>* `git config --global user.name "XXX" `   #设置用户名<br>
>* `git config --global user.email "XXX@XXX.XX"`  #设置Email<br>


**账号注册设置SSH keys参考 GIT账号注册说明.docx**


**创建repository**
>方法一<br>
>`git init `     #初始化GIT仓库<br>
>方法二<br>
>* `git clone  仓库地址  `   #直接克隆现有git仓库<br>
>例如：克隆www库<br>
> `git clone git@192.168.0.2:root/www.git`<br>


**查看、新建、切换分支**<br>
**查看分支：**
> *   ` git branch ` #查看本地分支，当前分支使用“*”标记；<br>
>*   `git  branch -a` #查看本地和远程分支；<br>
>`git branch -v` #查看本地分支并显示最后一次提交信息；<br>
         

**新建切换分支**
>`git branch NAME `                                                          #创建NAME分支<br>
>`git branch \<NEW_BRANCH>\<START POINT>`             #基于提交\<start-point>创建新分支<br>
>`git checkout -b NAME    `                                              #创建并切换都NAME分支 相当于git branch NAME+git checkout NAME<br>
>`git checkout -b \<NEW_BRANCH> \<START POINT>`   #基于提交START POINT 分支为起点 创建并切换至本地NEW_BRANCH分支 <br>
>*   `git checkout -b  NAME   origin/NAME  `                       #新建本地分支NAME将远程分支关联到本地NAME 分支上，并切换到dev分支上<br>
>例如： `git checkout -b dev origin/dev   `                 #新建本地dev分支和代码库中的dev分支映射。远程分支名用 git branch -a查看<br>
>`git  checkout NAME  `                                                    #切换到NAME分支<br>

**删除分支**
>* `  git branch -d NAME  `      #删除NAME分支<br>
>* `  git branch -D NAME    `    #强制删除NAME分支<br>

**重命名分支**
>`git branch -m <oldbranch><newbranch>  `                #重命名分支<br>
>`git branch -M <oldbranch><newbranch>   `               #强制重命名分支<br>
   

**查看状态**
>`git status `    #查看状态<br>
>*      `git status -s`  #显示精简信息<br>
> `git diff` <br>
>*   `git diff    `               #对比工作区和暂存区<br>
>`git diff FILENAME`  #对比指定文件差异<br>
>`git diff --staged`    #对比暂存区和本地库<br>
>`git diff HEAD `        #对比工作区和本地库<br>

>* `git log     `                               #显示提交记录<br>
>`git log --oneline  `                  #简约模式显示；<br>
         
**提交操作**
>*   `git add .  /git add --all/ git add -A  ``           #添加所有文件到暂存区<br>
>*  `git add FILENAME      `                                #直接添加特定文件 到暂存区<br>

>*   ` git commit -m "MESSAGE"  `                      #提交到本地版本库<br>
> *    `git commit -am "MESSAGE"    `                  #直接从工作区提交到本地版本库 相当于git add + git commit  2条命令<br>

**同步命令**
>* `git pull `  #从远程获取最新版本并merge到本地<br>
>*` git fetch` #从远程获取最新版本到本地，不会自动merge<br>
>* ` git fetch origin` # 抓取远程仓库更新<br>


**推送命令：**
>`git push`   #推送所有分支到远端代码库。<br>
>`git push -u origin BRANCHNAME` # 客户端首次推送分支至远程代码库(如无远程主分支则创建，用于初始化远程仓库)<br>
>`git push origin BRANCHNAME `# 将当前分支推到远程代码库对应的BRANCHNAME分支<br>
    

**撤销误操作**
>`git reset  FILENAME  `                 # 从暂存区撤销到工作区，类似于git add 的逆操作<br>
>`git checkout FILENAME  `            #撤销工作区修改      <br>
>`git checkout HEAD FILENAME `   # 直接从本地库中还原工作区文件<br>

**合并**
>* `git merge  \<BRANCH NAME> `#合并某分支到当前分支<br>


**暂存工作区**
>*   `git stash ` #暂存当前工作区<br>
>*  ` git stash list ` #查看暂存区内容<br>
>*  `git stash pop` #恢复暂存区内容，并删除暂存区内容<br>
>`git stash apply`  #恢复暂存区的内容 但是不删除暂存的内容<br>
>`git stash drop `   #删除暂存区内容<br>


**案列一：克隆代码库test1至本地，并推送README.md文件至远程库master分支**

 **初始设置（永久，设置一次即可）**<br>
>`git config --global user.name "Administrator" ` <br>
>`git config --global user.email "xuweiwei@geihui.cn"`   <br>

**克隆远程库**
> `git clone git@192.168.0.2:root/test1.git<br>`
>` cd test1    `                                               #进入test1目录<br>
>` git add README.md    `                           #添加README.md文件到暂存区<br>
>`git commit -m "add README"  `             #提交commit 到本地库<br>
>`git push -u origin master  `                      #推送至远程仓库 （第一推送 加-u选项，以后推送直接git push即可）<br>

**案列二 ：冲突解决 ，使用暂存命令**<br>
>`git stash ` #暂存 <br>
>`git  pull `  #拉取代码去<br>
>`git stash pop` #还原暂存内容git自动合并<br>

**案列三： 合并分支 ，将本地分支goods 分支和远程goods_tmp分支合并**

>`git fetch origin`                                                      #拉取远程最新代码<br>
>`git checkout -b goods_tmp origin/goods_tmp `  #创建本地goods_tmp分支并关联远程goods_tmp分支<br>
>`git checkout goods `                                             #却换到本地goods分支<br>
>`git merge --no-ff  -m "merge with no-ff"  goods_tmp  `            #使用普通模式合并goods_tmp分支，--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并看不出来曾经做过合并<br>
>`git push origin goods   `                                      #推送至远程goods分支<br>