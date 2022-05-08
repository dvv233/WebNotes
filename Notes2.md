## Git与GitHub
1. 添加SSH关联授权  
    >ssh-keygen

    > 使用 ' cat ~/.ssh/id_rsa.pub'将文件中的公钥内容复制出来。

    > 使用 SSH 的好处:
    - 执行git push免密推送。
    - 提高数据传输速度。

2. 使用'cd XXX'进入到仓库目录XXX中
3. 配置个人信息 【这些也可在github或gitee页面中修改】
- <font color="skyblue">git config -l  </font> 查看个人配置信息
- <font color="skyblue">git congig --global user.email "xxx"</font>
- <font color="skyblue">git config --global user.name "xxx"</font>
4. 常用的git基本命令：
- 执行 <font color="red">git status</font> 查看整个仓库的状态
- 使用 <font color="red">git add [文件名]</font>命令跟踪此新建文件，即把新增文件添加到暂存区，以备提交。对多个文件或目录进行了增删改，可以使用 <font color="red">git add . </font> 命令全部添加到暂存区。【 git add 命令是将这些修改添加到暂存区，暂存区记录的只是修改。】
- 执行 <font color="skyblue">git reset -- [文件名] </font>或者 <font color="skyblue">git rm --cached [文件名]</font> 命令撤销暂存区的修改。<font color="skyblue">git reset --</font> 即可把暂存区的全部修改撤销。
- 使用<font color="skyblue">git diff</font>可以用来查看工作区被跟踪的文件的修改详情。
--执行 <font color="red">git commit -m '写提交备注'。</font> 命令把暂存区的修改提交到版本区，生成一个新的版本。【不同系统可能对于''和" "有要求】
- 使用<font color="skyblue">git log</font>它用来查看版本区的提交历史记录。
- 执行 <font color="red">git push</font>后面不需要任何选项和参数，此命令会把本地仓库 master 分支上的新增提交推送到远程仓库的同名分支上。
- - 使用命令 <font color="skyblue">git branch -avv</font>它用来查看全部分支信息。
    > ![branchInfo](/images/branch_info.png)

    > 上图有三行信息，依次说明:
第一行，开头的星号表示当前所在分支，绿色的 master 是分支名，之所以是绿色，也是因为它是当前所在分支。后面第二项是版本号，第三项中括号里面蓝色的字，表示此分支跟踪的远程分支的名字，当然啦，这也是克隆远程仓库到本地时的默认设置 -- 创建 master 分支并自动跟踪远程同名分支；冒号后面黑色文字表示本地分支领先其跟踪的远程分支一个提交。最后一项是提交时填写的备注信息。
第二行，是 Git 指针信息，它指向远程仓库的 master 分支，这行信息暂不重要。
第三行，远程分支信息，详见第一行的解释。
- git reset命令
    -  <font color="skyblue">git reset --soft HEAD^ </font>撤销最近的一次提交，将修改还原到暂存区。HEAD^ 表示撤销一次提交，HEAD^^ 表示撤销两次提交，撤销 n 次可以简写为 HEAD~n。
    - <font color="skyblue">git reset --hard [版本号]</font>回到分支的每一次版本或者 <font color="skyblue">git reset --hard HEAD@{n} </font>回到当前分支最近n次提交版本变化前
- 使用<font color="skyblue">git push -f </font>强制推送。如果不是基于远程仓库 origin/master 分支的最新提交版本，而是撤回了一个版本后提交。这样本地和远程提交版本上就有了冲突，又叫做提交时间线分叉。这种情况下也是可以将本地 master 分支推送到远程仓库的，使用git push -f 强制推送【增加一个-f 选项】
- <font color="skyblue">git reflog </font>命令，它会记录本地仓库所有分支的每一次版本变化。reflog 记录只存在于本地仓库中，本地仓库删除后，记录消失。
5. 设置命令别名
    > 设置别名的命令是 <font color="skyblue">git config --global alias.[别名] [原命令] </font>，如果原命令中有选项，(就是带有-m -f这样的选项)需要加引号。别名是自定义的，可以随意命名，设置后，原命令和别名具有同等作用。

    > 【注：】如果要修改别名将其运用到新的命令中，增加选项 <font color="skyblue">--replace-all</font>。
例如 之前运用命令$ git config --global alias.br branch将br设置为branch的别名，现在需要将br设置为'branch -avv'的别名，执行命令 $ git config --global alias.br 'branch -avv' --replace-all
6. Git 分支
- <font color="skyblue">git fetch</font>它的作用是将远程仓库的分支**信息**拉取到本地仓库，注意，仅仅是更新了本地的远程分支信息
- <font color="skyblue">git pull </font>命令来拉取远程分支到本地，pull 是拉取远程仓库的**数据**到本地，需要联网，而由于前面执行过 git fetch 命令，所以也可以执行 <font color="skyblue">git rebase origin/master </font>命令来实现 “使本地 master 分支基于远程仓库的 master 分支”，rebase 命令在后面还会经常用。这样在github页面上修改的数据内容可以更新到本地。
- 执行 <font color="skyblue">git branch [分支名] </font>可以创建新的分支
- 执行 <font color="skyblue">git checkout [分支名] </font>切换分支 
- <font color="skyblue">git checkout -b [分支名] </font>创建分支并切换到新分支
    > 新建分支并无跟踪任何远程分支，所以没有 master 分支中的中括号和括号内的蓝色远程分支名。使用<font color="skyblue">git branch -u [主机名/远程分支名] [本地分支名] </font>将本地分支与远程分支关联，或者说使本地分支跟踪远程分支。如果是设置当前所在分支跟踪远程分支，最后一个参数本地分支名可以省略不写。同样执行 <font color="skyblue">git branch --unset-upstream [分支名] </font>即可撤销该分支对远程分支的跟踪，同样地，如果撤销当前所在的分支的跟踪，分支名可以省略不写。
- 执行 <font color="skyblue">git push [主机名] [本地分支名]:[远程分支名] </font>，将本地分支推送到远程仓库的分支中。通常冒号前后的分支名是相同的，如果是相同的，可以省略 :[远程分支名]，如果远程分支不存在，会自动创建。如果要在推送时就自动跟踪远程分支，加个<font color="skyblue">-u</font> 选项
- 使用<font color="skyblue">git push [主机名] :[远程分支名] :[远程分支名] :[远程分支名]</font>或者 <font color="skyblue">git push [主机名] --delete [远程分支名] </font>删除远程分支。使用 <font color="skyblue">git branch -D [分支名] </font>删除本地分支。
- 本地分支改名 <font color="skyblue">git branch -m [原分支名] [新分支名]</font>

