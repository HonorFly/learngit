# git分布式版本控制系统 #
## 1.安装 ##
    1. git官网下载安装程序
    2. 配置  
       git config --global user.name 
       git config --global user.email
## 2.初始化 ##
    git init  初始化
    git add 添加文件
    git commit -m "提交说明" 文件提交
    git diff  比较文件的改变
    git status  仓库的状态
## 3.版本回退 ##
    git log 查看提交历史
    git log --pretty=oneline 查看提交历史精简
    git reflog  查看命令历史（便于回退版本）
    git reset --hard HEAD^ 回退上一版本 HEAD^^ 回退两个版本  HEAD~100 回退100个版本
    git reset --hard commit_id(例：384180) 数字指定回退到的版本号，数字是commit_id
## 4.工作区和暂存区 ##
    git diff 是工作区（work dict）和暂存区（stage）的比较
    git diff --cashed 是暂存区（stage)和仓库分支(master)的比较
    git diff HEAD -- 文件名 可以查看工作区和仓库分支（版本库）里面最新版本的区别
    git add 是把要提交的所有修改放到暂存区 
    git commit 是把暂存区的修改提交到仓库分支
## 5.git commit后面没有写说明的情况 ##
    直接写git commit 进行提交，没有写提交说明和-m，git bash进入vim模式，处理方法：
    首先，输入i，进入insert输入模式，此时输入说明；（相当于给一次不就得说明机会）；
    然后，输入完后，按esc，下方的insert消失；
    最后，输入:wq,回车。
## 6.git log太长，无法退出的情况 ##
    按q即可（最好英文状态下，如果是中文按完q按回车键）
## 7.撤销修改 ##
    三种情况：
      1、修改的只是工作区某个文件的内容，想直接丢弃工作区的修改，用命令git checkout -- file；
      2、不但修改了工作区某个文件的内容，还添加到暂存区，想丢弃修改，分两步，第一步用命令git reset HEAD file,此时回到场景1，第二步就是按照第一步的命令git checkout -- file；(git reset --hard HEAD 或者 git checkout HEAD -- file,这两种方法也可以实现add后的撤销）；
      3、已经git commit就是提交到版本库了，想撤销本次提交，参考上面的“版本回退”，回退到指定版本。

      工作区的修改分为两种情况：一种是修改后没被放到暂存区，此时用git checkout -- file 就可以回到和版本库一样的状态；另一种是已经添加到暂存区后，又做了修改，此时git checkout -- file这个命令就回到添加到暂存区后的状态，这时候就要采用第二种情况的方法进行撤销。

      git status 查看状态，可以根据下面的提示判断文件是否已在暂存区，当下面出现（use “git reset HEAD <file>..." to unstage）这句话说明修改添加到暂存区，还没有提交；当出现（use "git add <file>..." to update whaat will be committed) (use "git checkout -- <file>..." to discard changes in working directory)时，说明暂存区是干净的，工作区有修改。
## 8.删除文件 ##
      通常情况下，没用的文件直接在文本管理器将文件删除，也可以用rm命令删除文件（rm file）；
      删除文件后，工作区和版本库不一致，git status查看那个文件删除；

      此时，有两种选择情况：
        1.删错了，版本库还有，直接将误删的文件恢复到最新版本；git checkout -- file 这种情况本质就是版本库的替换工作区的，无论工作区是修改还是删除，都可以一键还原，但只能恢复到版本库的最新文件，不会恢复最近一次提交后修改的内容。
        2.确实从版本库中删除该文件。用命令git rm删掉，并且git commit提交。文件从版本库被删除。

      rm删除文件和从文件管理器删除文件是一样的,只是将工作区的文件删除,版本库的文件未删除,git rm file是删除版本库的文件。两者是不同的。如果是只删除工作区的文件可以用git checkout -- file，如果是git rm file删除文件，此时将版本库，暂存区和工作区的都删除，此时没有使用git commit命令提交到版本库时，可以使用版本回退或者git checkout HEAD file 或者 git checkout HEAD -- file；如果使用git rm file删除文件，并用git commit提交到版本库时，只能用版本回退恢复。