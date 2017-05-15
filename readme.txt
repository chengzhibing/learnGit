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
  13、你已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远      程同步，这样，GitHub上的仓库既可以作为备份，又可以让其他人通过该仓库来协作，真是一举        多得
    1）首先，登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：
    2）在Repository name填入learngit，其他保持默认设置，点击“Create repository”按钮，就成       功地创建了一个新的Git仓库：
    3）目前，在GitHub上的这个learngit仓库还是空的，GitHub告诉我们，可以从这个仓库克隆出新的       仓库，也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。

       现在，我们根据GitHub的提示，在本地的learngit仓库下运行命令：

       $ git remote add origin git@github.com:michaelliao/learngit.git
    *要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；

     关联后，使用命令git push -u origin master第一次推送master分支的所有内容；

     此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；

   *****你需要修改远程地址，
     可以键入：git remote set-url origin xxxx，来修改远程地址，
     你也可以先删除origin然后再添加：
          git remote rm origin
          git remote add origin https://github.com/coder-pig/SimpleTea.git
    还可以直接修改.git文件夹里的config文件，直接替换
          url=""

    另外，这个origin不是什么固定的东西，这个只是我们后面那个仓库地址的一个别名！！！
   你可以写成其他的东西，比如我的项目既托管在Github又托管在Git@OSC，我可这样设置：
      git remote add github https://github.com/coder-pig/SimpleTea.git
      git remote add osc git@git.oschina.net:coder-pig/SimpleTea.git
   这一点要弄清楚！！！
14、现在，假设我们从零开发，那么最好的方式是先创建远程库，然后，从远程库克隆。

    1）首先，登陆GitHub，创建一个新的仓库，名字叫gitskills：
    我们勾选Initialize this repository with a README，这样GitHub会自动为我们创建一个         README.md文件。创建完毕后，可以看到README.md文件：
    2）现在，远程库已经准备好了，下一步是用命令git clone克隆一个本地库：
    $ git clone git@github.com:michaelliao/gitskills.git（写远程库的地址）
     （或者是git clone https://github.com/chengzhibing/gitMap.git）;
      Cloning into 'gitskills'...
      remote: Counting objects: 3, done.
      remote: Total 3 (delta 0), reused 0 (delta 0)
      Receiving objects: 100% (3/3), done.

      $ cd gitskills
      $ ls
      README.md
15、1）分支就是科幻电影里面的平行宇宙，当你正在电脑前努力学习Git的时候，另一个你正在另一个      平行宇宙里努力学习SVN。
    2)如果两个平行宇宙互不干扰，那对现在的你也没啥影响。不过，在某个时间点，两个平行宇宙合      并了，结果，你既学会了Git又学会了SVN！
    3)分支在实际中有什么用呢？假设你准备开发一个新功能，但是需要两周才能完成，第一周你写了    50%的代码，如果立刻提交，由于代码还没写完，不完整的代码库会导致别人不能干活了。如果等代    码全部写完再一次提交，又存在丢失每天进度的巨大风险。

    4）现在有了分支，就不用怕了。你创建了一个属于你自己的分支，别人看不到，还继续在原来的分    支上正常工作，而你在自己的分支上干活，想提交就提交，直到开发完毕后，再一次性合并到原来      的分支上，这样，既安全，又不影响别人工作。
    5）在版本回退里，你已经知道，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分     支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不     是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支。
    6）一开始的时候，master分支是一条线，Git用master指向最新的提交，再用HEAD指向master，就     能确定当前分支，以及当前分支的提交点：
    7）每次提交，master分支都会向前移动一步，这样，随着你不断提交，master分支的线也越来越长
    8）当我们创建新的分支，例如dev时，Git新建了一个指针叫dev，指向master相同的提交，再把       HEAD指向dev，就表示当前分支在dev上：不过，从现在开始，对工作区的修改和提交就是针对dev分     支了，比如新提交一次后，dev指针往前移动一步，而master指针不变：
   9）假如我们在dev上的工作完成了，就可以把dev合并到master上。Git怎么合并呢？最简单的方法，    就是直接把master指向dev的当前提交，就完成了合并：
   10)合并完分支后，甚至可以删除dev分支。删除dev分支就是把dev指针给删掉，删掉后，我们就剩下    了一条master分支：
   ***********下面开始实战。
   1）首先，我们创建dev分支，然后切换到dev分支：

    $ git checkout -b dev
    Switched to a new branch 'dev'
    **git checkout命令加上-b参数表示创建并切换，相当于以下两条命令：

    $ git branch dev
    $ git checkout dev
    Switched to branch 'dev'
   2）然后，用git branch命令查看当前分支：

    $ git branch
      * dev
      master
   
    **git branch命令会列出所有分支，当前分支前面会标一个*号。

   3）然后，我们就可以在dev分支上正常提交，比如对readme.txt做个修改，加上一行：

    Creating a new branch is quick.
    然后提交：

    $ git add readme.txt 
    $ git commit -m "branch test"
      [dev fec145a] branch test
      1 file changed, 1 insertion(+)
   4）现在，dev分支的工作完成，我们就可以切换回master分支：

    $ git checkout master
    Switched to branch 'master'
    切换回master分支后，再查看一个readme.txt文件，刚才添加的内容不见了！因为那个提交是在dev    分支上，而master分支此刻的提交点并没有变：

   

    5）现在，我们把dev分支的工作成果合并到master分支上：
    
    $ git merge dev
    Updating d17efd8..fec145a
    Fast-forward
    readme.txt |    1 +
    1 file changed, 1 insertion(+)
    **git merge命令用于合并指定分支到当前分支。合并后，再查看readme.txt的内容，就可以看到，     和dev分支的最新提交是完全一样的。

    **注意到上面的Fast-forward信息，Git告诉我们，这次合并是“快进模式”，也就是直接把master     指向dev的当前提交，所以合并速度非常快。

    **当然，也不是每次合并都能Fast-forward，我们后面会讲其他方式的合并。

    6）合并完成后，就可以放心地删除dev分支了：

    $ git branch -d dev
      Deleted branch dev (was fec145a).
      删除后，查看branch，就只剩下master分支了：

    $ git branch
     * master
    因为创建、合并和删除分支非常快，所以Git鼓励你使用分支完成某个任务，合并后再删掉分支，这    和直接在master分支上工作效果是一样的，但过程更安全。
    7）Git鼓励大量使用分支：

    查看分支：git branch

    创建分支：git branch <name>

    切换分支：git checkout <name>

    创建+切换分支：git checkout -b <name>

    合并某分支到当前分支：git merge <name>

    删除分支：git branch -d <name>
16、解决冲突
   1）准备新的feature1分支，继续我们的新分支开发：
    $ git checkout -b feature1
      Switched to a new branch 'feature1'
    修改readme.txt最后一行，改为：

    Creating a new branch is quick AND simple.
    2）在feature1分支上提交：

    $ git add readme.txt 
    $ git commit -m "AND simple"
    [feature1 75a857c] AND simple
    1 file changed, 1 insertion(+), 1 deletion(-)
    3）切换到master分支：

    $ git checkout master
     Switched to branch 'master'
     Your branch is ahead of 'origin/master' by 1 commit.
     **Git还会自动提示我们当前master分支比远程的master分支要超前1个提交。

    5）在master分支上把readme.txt文件的最后一行改为：

    Creating a new branch is quick & simple.
    6）提交：

    $ git add readme.txt 
    $ git commit -m "& simple"
    [master 400b400] & simple
    1 file changed, 1 insertion(+), 1 deletion(-)
    现在，master分支和feature1分支各自都分别有新的提交
    这种情况下，Git无法执行“快速合并”，只能试图把各自的修改合并起来，但这种合并就可能会有     冲突，我们试试看：

    7）$ git merge feature1
         Auto-merging readme.txt
         CONFLICT (content): Merge conflict in readme.txt
         Automatic merge failed; fix conflicts and then commit the result.
         果然冲突了！Git告诉我们，readme.txt文件存在冲突，必须手动解决冲突后再提交。
         git status也可以告诉我们冲突的文件：

         $ git status
	 # On branch master
	 # Your branch is ahead of 'origin/master' by 2 commits.
	 #
         # Unmerged paths:
	 #   (use "git add/rm <file>..." as appropriate to mark resolution)
	 #
	 #       both modified:      readme.txt
	 #
	 no changes added to commit (use "git add" and/or "git commit -a")
	 我们可以直接查看readme.txt的内容：

         Git is a distributed version control system.
         Git is free software distributed under the GPL.
	 Git has a mutable index called stage.
	 Git tracks changes of files.
	 <<<<<<< HEAD
	 Creating a new branch is quick & simple.
	 =======
	 Creating a new branch is quick AND simple.
	 >>>>>>> feature1
    8）**Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，我们修改如下后保存：

	 Creating a new branch is quick and simple.
    9）再提交：

	 $ git add readme.txt 
	 $ git commit -m "conflict fixed"
	 [master 59bc1cb] conflict fixed
     10）用带参数的git log也可以看到分支的合并情况：

	 $ git log --graph --pretty=oneline --abbrev-commit
	 *   59bc1cb conflict fixed
	 |\
 	 | * 75a857c AND simple
	 * | 400b400 & simple
	 |/
	 * fec145a branch test
     11）最后，删除feature1分支：

         $ git branch -d feature1
	 Deleted branch feature1 (was 75a857c).
         工作完成。
     **当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。

     用git log --graph命令可以看到分支合并图。
17、分支管理策略
    通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分     支信息。

    如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上    就可以看出分支信息。

    下面我们实战一下--no-ff方式的git merge：
    1）首先，仍然创建并切换dev分支：

     $ git checkout -b dev
     Switched to a new branch 'dev'
    2）修改readme.txt文件，并提交一个新的commit：

     $ git add readme.txt 
     $ git commit -m "add merge"
     [dev 6224937] add merge
     1 file changed, 1 insertion(+)
    3）现在，我们切换回master：

      $ git checkout master
      Switched to branch 'master'
    4）准备合并dev分支，请注意--no-ff参数，表示禁用Fast forward：

     $ git merge --no-ff -m "merge with no-ff" dev
      Merge made by the 'recursive' strategy.
      readme.txt |    1 +
     1 file changed, 1 insertion(+)
     因为本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去。
    5）合并后，我们用git log看看分支历史：

    $ git log --graph --pretty=oneline --abbrev-commit
    *   7825a50 merge with no-ff
    |\
    | * 6224937 add merge
    |/
    *   59bc1cb conflict fixed
    ...
   6）在实际开发中，我们应该按照几个基本原则进行分支管理：

      首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；

      那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本      发布时，再把dev分支合并到master上，在master分支发布1.0版本；

      你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上          合并就可以了。
      **合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做       过合并，而fast forward合并就看不出来曾经做过合并。
18、Bug分支
    1）软件开发中，bug就像家常便饭一样。有了bug就需要修复，在Git中，由于分支是如此的强大，      所以，每个bug都可以通过一个新的临时分支来修复，修复后，合并分支，然后将临时分支删除。

     2）当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复         它，但是，等等，当前正在dev上进行的工作还没有提交：

        $ git status
	# On branch dev
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#       new file:   hello.py
	#
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#       modified:   readme.txt
	#
	并不是你不想提交，而是工作只进行到一半，还没法提交，预计完成还需1天时间。但是，必须	        在两个小时内修复该bug，怎么办？

      3）幸好，Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继        续工作：

	$ git stash
	Saved working directory and index state WIP on dev: 6224937 add merge
	HEAD is now at 6224937 add merge
        现在，用git status查看工作区，就是干净的（除非有没有被Git管理的文件），因此可以放心         地创建分支来修复bug。
      4）首先确定要在哪个分支上修复bug，假定需要在master分支上修复，就从master创建临时分支：

        $ git checkout master
        Switched to branch 'master'
        Your branch is ahead of 'origin/master' by 6 commits.
        $ git checkout -b issue-101
        Switched to a new branch 'issue-101'
      5）现在修复bug，需要把“Git is free software ...”改为“Git is a free software ...”，然后提交：

        $ git add readme.txt 
	$ git commit -m "fix bug 101"
	[issue-101 cc17032] fix bug 101
 	1 file changed, 1 insertion(+), 1 deletion(-)
      6）修复完成后，切换到master分支，并完成合并，最后删除issue-101分支：

        $ git checkout master
        Switched to branch 'master'
	Your branch is ahead of 'origin/master' by 2 commits.
	$ git merge --no-ff -m "merged bug fix 101" issue-101
        Merge made by the 'recursive' strategy.
        readme.txt |    2 +-
        1 file changed, 1 insertion(+), 1 deletion(-)
        $ git branch -d issue-101
        Deleted branch issue-101 (was cc17032).
      7）太棒了，原计划两个小时的bug修复只花了5分钟！现在，是时候接着回到dev分支干活了！

        $ git checkout dev
        Switched to branch 'dev'
        $ git status
        # On branch dev
        nothing to commit (working directory clean)
        工作区是干净的，刚才的工作现场存到哪去了？用git stash list命令看看：

        $ git stash list
        stash@{0}: WIP on dev: 6224937 add merge
      8）工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：
        一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；

	另一种方式是用git stash pop，恢复的同时把stash内容也删了：
        $ git stash pop
	# On branch dev
	# Changes to be committed:
	#   (use "git reset HEAD <file>..." to unstage)
	#
	#       new file:   hello.py
	#
	# Changes not staged for commit:
	#   (use "git add <file>..." to update what will be committed)
	#   (use "git checkout -- <file>..." to discard changes in working directory)
	#
	#       modified:   readme.txt
	#
	Dropped refs/stash@{0} (f624f8e5f082f2df2bed8a4e09c12fd2943bdd40)
        再用git stash list查看，就看不到任何stash内容了：

	$ git stash list
	你可以多次stash，恢复的时候，先用git stash list查看，然后恢复指定的stash，用命令：

	$ git stash apply stash@{0}
        **修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

	当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，	        回到工作现场。
19、软件开发中，总有无穷无尽的新的功能要不断添加进来。

添加一个新功能时，你肯定不希望因为一些实验性质的代码，把主分支搞乱了，所以，每添加一个新功能，最好新建一个feature分支，在上面开发，完成后，合并，最后，删除该feature分支。

现在，你终于接到了一个新任务：开发代号为Vulcan的新功能，该功能计划用于下一代星际飞船。

于是准备开发：
   1）$ git checkout -b feature-vulcan
   Switched to a new branch 'feature-vulcan'
   2）5分钟后，开发完毕：
      $ git add vulcan.py
      $ git status
      # On branch feature-vulcan
      # Changes to be committed:
      #   (use "git reset HEAD <file>..." to unstage)
      #
      #       new file:   vulcan.py
      #
	$ git commit -m "add feature vulcan"
	[feature-vulcan 756d4af] add feature vulcan
 	1 file changed, 2 insertions(+)
 	create mode 100644 vulcan.py 
   3）切回dev，准备合并：

     $ git checkout dev
   4）一切顺利的话，feature分支和bug分支是类似的，合并，然后删除。

但是，

就在此时，接到上级命令，因经费不足，新功能必须取消！

虽然白干了，但是这个分支还是必须就地销毁：

5）$ git branch -d feature-vulcan
error: The branch 'feature-vulcan' is not fully merged.
If you are sure you want to delete it, run 'git branch -D feature-vulcan'.
销毁失败。Git友情提醒，feature-vulcan分支还没有被合并，如果删除，将丢失掉修改，如果要强行删除，需要使用命令git branch -D feature-vulcan。

现在我们强行删除：

6）$ git branch -D feature-vulcan
Deleted branch feature-vulcan (was 756d4af).
终于删除成功！
**开发一个新feature，最好新建一个分支；

如果要丢弃一个没有被合并过的分支，可以通过git branch -D <name>强行删除。
19、========多人协作

当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。

1）要查看远程库的信息，用git remote：

$ git remote
origin
2）或者，用git remote -v显示更详细的信息：

$ git remote -v
origin  git@github.com:michaelliao/learngit.git (fetch)
origin  git@github.com:michaelliao/learngit.git (push)
上面显示了可以抓取和推送的origin的地址。如果没有推送权限，就看不到push的地址。
======推送分支

推送分支，就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：

$ git push origin master
如果要推送其他分支，比如dev，就改成：

$ git push origin dev
但是，并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？

master分支是主分支，因此要时刻与远程同步；

dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；

bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；

feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

总之，就是在Git中，分支完全可以在本地自己藏着玩，是否推送，视你的心情而定！

======抓取分支
多人协作时，大家都会往master和dev分支上推送各自的修改。
1）现在，模拟一个你的小伙伴，可以在另一台电脑（注意要把SSH Key添加到GitHub）或者同一台电脑的另一个目录下克隆：
$ git clone git@github.com:michaelliao/learngit.git
Cloning into 'learngit'...
remote: Counting objects: 46, done.
remote: Compressing objects: 100% (26/26), done.
remote: Total 46 (delta 16), reused 45 (delta 15)
Receiving objects: 100% (46/46), 15.69 KiB | 6 KiB/s, done.
Resolving deltas: 100% (16/16), done.
2）当你的小伙伴从远程库clone时，默认情况下，你的小伙伴只能看到本地的master分支。不信可以用git branch命令看看：

$ git branch
* master
3）现在，你的小伙伴要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是他用这个命令创建本地dev分支：

$ git checkout -b dev origin/dev
4）现在，他就可以在dev上继续修改，然后，时不时地把dev分支push到远程：

$ git commit -m "add /usr/bin/env"
[dev 291bea8] add /usr/bin/env
 1 file changed, 1 insertion(+)
$ git push origin dev
Counting objects: 5, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 349 bytes, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:michaelliao/learngit.git
   fc38031..291bea8  dev -> dev
5）你的小伙伴已经向origin/dev分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送：
$ git add hello.py 
$ git commit -m "add coding: utf-8"
[dev bd6ae48] add coding: utf-8
 1 file changed, 1 insertion(+)
$ git push origin dev
To git@github.com:michaelliao/learngit.git
 ! [rejected]        dev -> dev (non-fast-forward)
error: failed to push some refs to 'git@github.com:michaelliao/learngit.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
6）推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送：

$ git pull
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0)
Unpacking objects: 100% (3/3), done.
From github.com:michaelliao/learngit
   fc38031..291bea8  dev        -> origin/dev
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details

    git pull <remote> <branch>

If you wish to set tracking information for this branch you can do so with:

    git branch --set-upstream dev origin/<branch>
git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，
7）根据提示，设置dev和origin/dev的链接：

$ git branch --set-upstream dev origin/dev
Branch dev set up to track remote branch dev from origin.
8）再pull：

$ git pull
Auto-merging hello.py
CONFLICT (content): Merge conflict in hello.py
Automatic merge failed; fix conflicts and then commit the result.
这回git pull成功，但是合并有冲突，需要手动解决，解决的方法和分支管理中的解决冲突完全一样。
9）解决后，提交，
10）再push：

$ git commit -m "merge & fix hello.py"
[dev adca45d] merge & fix hello.py
$ git push origin dev
Counting objects: 10, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (6/6), 747 bytes, done.
Total 6 (delta 0), reused 0 (delta 0)
To git@github.com:michaelliao/learngit.git
   291bea8..adca45d  dev -> dev

****因此，多人协作的工作模式通常是这样：

1）首先，可以试图用git push origin branch-name推送自己的修改；

2）如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

3）如果合并有冲突，则解决冲突，并在本地提交；

4）没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！

5）如果git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令git branch --set-upstream branch-name origin/branch-name。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。
****查看远程库信息，使用git remote -v；

本地新建的分支如果不推送到远程，对其他人就是不可见的；

从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；

在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；

建立本地分支和远程分支的关联，使用git branch --set-upstream branch-name origin/branch-name；

从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。
20、Git的标签虽然是版本库的快照，但其实它就是指向某个commit的指针（跟分支很像对不对？但是分支可以移动，标签不能移动），所以，创建和删除标签都是瞬间完成的。

Git有commit，为什么还要引入tag？

“请把上周一的那个版本打包发布，commit号是6a5819e...”

“一串乱七八糟的数字不好找！”

如果换一个办法：

“请把上周一的那个版本打包发布，版本号是v1.2”

“好的，按照tag v1.2查找commit就行！”

所以，tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起。


====创建标签
1）在Git中打标签非常简单，首先，切换到需要打标签的分支上：

$ git branch
* dev
  master
$ git checkout master
Switched to branch 'master'
2）然后，敲命令git tag <name>就可以打一个新标签：

$ git tag v1.0
可以用命令git tag查看所有标签：

$ git tag
v1.0
3）默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，比如，现在已经是周五了，但应该在周一打的标签没有打，怎么办？

方法是找到历史提交的commit id，然后打上就可以了：

$ git log --pretty=oneline --abbrev-commit
6a5819e merged bug fix 101
cc17032 fix bug 101
7825a50 merge with no-ff
6224937 add merge
59bc1cb conflict fixed
400b400 & simple
75a857c AND simple
fec145a branch test
d17efd8 remove test.txt
...
比方说要对add merge这次提交打标签，它对应的commit id是6224937，敲入命令：

$ git tag v0.9 6224937
再用命令git tag查看标签：

$ git tag
v0.9
v1.0
注意，标签不是按时间顺序列出，而是按字母排序的。可以用git show <tagname>查看标签信息：

$ git show v0.9
commit 622493706ab447b6bb37e4e2a2f276a20fed2ab4
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Thu Aug 22 11:22:08 2013 +0800

    add merge
...
可以看到，v0.9确实打在add merge这次提交上。

还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：

$ git tag -a v0.1 -m "version 0.1 released" 3628164
用命令git show <tagname>可以看到说明文字：

$ git show v0.1
tag v0.1
Tagger: Michael Liao <askxuefeng@gmail.com>
Date:   Mon Aug 26 07:28:11 2013 +0800

version 0.1 released

commit 3628164fb26d48395383f8f31179f24e0882e1e0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Tue Aug 20 15:11:49 2013 +0800

    append GPL
还可以通过-s用私钥签名一个标签：

$ git tag -s v0.2 -m "signed version 0.2 released" fec145a
签名采用PGP签名，因此，必须首先安装gpg（GnuPG），如果没有找到gpg，或者没有gpg密钥对，就会报错：

gpg: signing failed: secret key not available
error: gpg failed to sign the data
error: unable to sign the tag
如果报错，请参考GnuPG帮助文档配置Key。

用命令git show <tagname>可以看到PGP签名信息：

$ git show v0.2
tag v0.2
Tagger: Michael Liao <askxuefeng@gmail.com>
Date:   Mon Aug 26 07:28:33 2013 +0800

signed version 0.2 released
-----BEGIN PGP SIGNATURE-----
Version: GnuPG v1.4.12 (Darwin)

iQEcBAABAgAGBQJSGpMhAAoJEPUxHyDAhBpT4QQIAKeHfR3bo...
-----END PGP SIGNATURE-----

commit fec145accd63cdc9ed95a2f557ea0658a2a6537f
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Thu Aug 22 10:37:30 2013 +0800

    branch test
用PGP签名的标签是不可伪造的，因为可以验证PGP签名。验证签名的方法比较复杂，这里就不介绍了。

====命令git tag <name>用于新建一个标签，默认为HEAD，也可以指定一个commit id；

git tag -a <tagname> -m "blablabla..."可以指定标签信息；

git tag -s <tagname> -m "blablabla..."可以用PGP签名标签；

命令git tag可以查看所有标签。
======操作标签
1）如果标签打错了，也可以删除：

$ git tag -d v0.1
Deleted tag 'v0.1' (was e078af9)
2）因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

如果要推送某个标签到远程，使用命令git push origin <tagname>：

$ git push origin v1.0
Total 0 (delta 0), reused 0 (delta 0)
To git@github.com:michaelliao/learngit.git
 * [new tag]         v1.0 -> v1.0
或者，一次性推送全部尚未推送到远程的本地标签：

$ git push origin --tags
Counting objects: 1, done.
Writing objects: 100% (1/1), 554 bytes, done.
Total 1 (delta 0), reused 0 (delta 0)
To git@github.com:michaelliao/learngit.git
 * [new tag]         v0.2 -> v0.2
 * [new tag]         v0.9 -> v0.9
3）如果标签已经推送到远程，要删除远程标签就麻烦一点，先从本地删除：
$ git tag -d v0.9
Deleted tag 'v0.9' (was 6224937)
然后，从远程删除。删除命令也是push，但是格式如下：

$ git push origin :refs/tags/v0.9
To git@github.com:michaelliao/learngit.git
 - [deleted]         v0.9
要看看是否真的从远程库删除了标签，可以登陆GitHub查看。
====
命令git push origin <tagname>可以推送一个本地标签；

命令git push origin --tags可以推送全部未推送过的本地标签；

命令git tag -d <tagname>可以删除一个本地标签；

命令git push origin :refs/tags/<tagname>可以删除一个远程标签。


21、使用gitHub

如何参与一个开源项目呢？比如人气极高的bootstrap项目，这是一个非常强大的CSS框架，你可以访问它的项目主页https://github.com/twbs/bootstrap，点“Fork”就在自己的账号下克隆了一个bootstrap仓库，然后，从自己的账号下clone：

git clone git@github.com:michaelliao/bootstrap.git
一定要从自己的账号下clone仓库，这样你才能推送修改。如果从bootstrap的作者的仓库地址git@github.com:twbs/bootstrap.git克隆，因为没有权限，你将不能推送修改

如果你想修复bootstrap的一个bug，或者新增一个功能，立刻就可以开始干活，干完后，往自己的仓库推送。

如果你希望bootstrap的官方库能接受你的修改，你就可以在GitHub上发起一个pull request。当然，对方是否接受你的pull request就不一定了。

=-===在GitHub上，可以任意Fork开源仓库；

自己拥有Fork后的仓库的读写权限；

可以推送pull request给官方仓库来贡献代码。

22、自定义Git


在安装Git一节中，我们已经配置了user.name和user.email，实际上，Git还有很多可配置项。

1）比如，让Git显示颜色，会让命令输出看起来更醒目：

$ git config --global color.ui true
这样，Git会适当地显示不同的颜色，比如git status命令：