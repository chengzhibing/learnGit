git 学习步骤


1、//检查windows有没有安装git 
 git --version //显示当前的版本号证明安装成功，没有的话就找教程安装
2、//安装成功在菜单栏内找到Git文件夹下Git Bash打开命令行工具
3、//设置本机的名字和邮箱
  $ git config --global user.name "Your Name"
  $ git config --global user.email "email@example.com"
  *注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这   个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

4、//创建版本库
      什么是版本库呢？版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录   里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以   追踪历史，或者在将来某个时刻可以“还原”。

      1）所以，创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：
     $ mkdir learngit
     $ cd learngit
     $ pwd
       /Users/michael/learngit
     *pwd命令用于显示当前目录  
     *如果你使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）           不包含中文
     2）第二步，通过git init命令把这个目录变成Git可以管理的仓库：
      $ git init
        Initialized empty Git repository in /Users/michael/learngit/.git/
      *瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者       可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要       手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

       如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以看见。
5、//把文件添加到版本库
    1）现在我们编写一个readme.txt文件,内容随便输入
       *一定要放到learngit目录下（子目录也行），因为这是一个Git仓库，放到其他地方Git再厉害        也找不到这个文件
    2）把一个文件放到Git仓库只需要两步。
       第一步：用命令git add告诉Git，把文件添加到仓库：实际上就是把文件修改添加到暂存区；
               $ git add readme.txt
               *执行上面的命令，没有任何显示，这就对了
       第二步：用命令git commit告诉Git，把文件提交到仓库：实际上就是把暂存区的所有内容提交                 到当前分支
               $ git commit -m "wrote a readme file"
                 [master (root-commit) cb926e7] wrote a readme file
 		 1 file changed, 2 insertions(+)
 		 create mode 100644 readme.txt
               *简单解释一下git commit命令，-m后面输入的是本次提交的说明，可以输入任意内容                ，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录
               *git commit命令执行成功后会告诉你，1个文件被改动（我们新添加的readme.txt文件                 ），插入了几行内容（readme.txt你所插入的内容）
               *为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件		，所以你可以多次add不同的文件，比如：

		$ git add file1.txt
		$ git add file2.txt file3.txt
		$ git commit -m "add 3 files."
6、//文件状态，差异
   我们已经成功地添加并提交了一个readme.txt文件，现在，是时候继续工作了，于是，我们继续修改    readme.txt文件（内容随意更改）
    1）现在，运行git status命令看看结果
        $ git status
	# On branch master
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#    modified:   readme.txt
	#
	no changes added to commit (use "git add" and/or "git commit -a")
       *git status命令可以让我们时刻掌握仓库当前的状态，上面的命令告诉我们，readme.txt被修          改过了，但还没有准备提交的修改。
   2）虽然Git告诉我们readme.txt被修改了，但如果能看看具体修改了什么内容，自然是很好的。比如      你休假两周从国外回来，第一天上班时，已经记不清上次怎么修改的readme.txt，所以，需要用        git diff这个命令看看：
     	$ git diff readme.txt 
	diff --git a/readme.txt b/readme.txt
	index 46d49bf..9247db6 100644
	--- a/readme.txt
	+++ b/readme.txt
	@@ -1,2 +1,2 @@
	-Git is a version control system.
	+Git is a distributed version control system.
 	Git is free software.
7、//版本回退，
   1）git log命令显示从最近到最远的提交日志；如果嫌输出信息太多，看得眼花缭乱的，可以试试加          上--pretty=oneline参数：
   $ git log --pretty=oneline
     3628164fb26d48395383f8f31179f24e0882e1e0 append GPL
     ea34578d5496d7dd233c827ed32a8cd576c5ee85 add distributed
     cb926e7ea50ad11b8f9e909c05226233bf755030 wrote a readme file
     *3628164...882e1e0是commit id（版本号）
   2）git reset --hard HEAD  查看当前版本
      git reset --hard HEAD^ 上一个版本
      git reset --hard HEAD^^上两个版本
      git reset --hard HEAD~100上100个版本
      $ git reset --hard 3628164（这串数字为版本号）跳转到对应版本
      $ git reflog  Git提供了一个命令git reflog用来记录你的每一次命令：
	ea34578 HEAD@{0}: reset: moving to HEAD^
	3628164 HEAD@{1}: commit: append GPL
	ea34578 HEAD@{2}: commit: add distributed
	cb926e7 HEAD@{3}: commit (initial): wrote a readme file
      （可以查看到你想进入的版本号）
   3)$ cat readme.txt 查看文件内容
8、1）工作区（Working Directory）

      就是你在电脑里能看到的目录，比如我的learngit文件夹就是一个工作区：
   2）版本库（Repository）

      工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。
   3）一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：
   4）add 是把文件添加到暂存区，
      commit 是把暂存区文件添加到当前分支
9、管理修改
  1）Git比其他版本控制系统设计得优秀，因为Git跟踪并管理的是修改，而非文件
  2）如果修改（添加文件，删除文件，修改文件）后的文件没有执行add命令，而直接执行commit命令     ，那么修改后的内容是提交不到当前分支的（也就是版本库）；
  3）git diff HEAD -- readme.txt查看工作区和版本库里面最新版本的区别：
10、撤销修改
  1）git checkout -- readme.txt把readme.txt文件在工作区的修改全部撤销，两种情况：
     一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态     ；

     一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状     态。
  2）git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区：
   
  *场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout --    file。

  *场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一    步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。

  *场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考7、2），不过前提是没有推     送到远程库。
11、删除文件
     git rm test.txt
    *如果是误删，若要再恢复误删的文件，应该执行命令 
     git checkout -- test.txt
    *命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但     是要小心，你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。======也就是说    提交到版本库以后，我又在工作区修改了文件的内容；这个时候我删除了文件，那么执行恢复命令    的话，就只能恢复到版本库内最新的版本，在工作区修改的内容恢复不了；



12、远程仓库（可以自己找台电脑充当服务器，也可以进入gitub官网注册账号）
    默认已经注册
    1）由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：
       第1步：创建SSH Key。
              在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和              id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。
              如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

              $ ssh-keygen -t rsa -C "youremail@example.com"
              你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个              Key也不是用于军事目的，所以也无需设置密码。

              如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两              个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公              钥，可以放心地告诉任何人。
      第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：
             然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：           点“Add Key”，你就应该看到已经添加的Key：
   2）为什么GitHub需要SSH Key呢？因为GitHub需要识别出你推送的提交确实是你推送的，而不是别人      冒充的，而Git支持SSH协议，所以，GitHub只要知道了你的公钥，就可以确认只有你自己才能推       送。

       当然，GitHub允许你添加多个Key。假定你有若干电脑，你一会儿在公司提交，一会儿在家里提     交 ，只要把每台电脑的Key都添加到GitHub，就可以在每台电脑上往GitHub推送了。

        最后友情提示，在GitHub上免费托管的Git仓库，任何人都可以看到喔（但只有你自己才能改）     所以，不要把敏感信息放进去。

      如果你不想让别人看到Git库，有两个办法，一个是交点保护费，让GitHub把公开的仓库变成私有      的，这样别人就看不见了（不可读更不可写）。另一个办法是自己动手，搭一个Git服务器，因为      是你自己的Git服务器，所以别人也是看不见的。这个方法我们后面会讲到的，相当简单，公司内      部开发必备。

      确保你拥有一个GitHub账号后，我们就即将开始远程仓库的学习。
  