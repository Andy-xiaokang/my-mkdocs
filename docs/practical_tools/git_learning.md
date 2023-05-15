# Github 入门与实践笔记
## chapter4 通过实际操作学习Git
### 4.1基本操作
* `git init`——**初始化仓库**
  要使用Git 进行版本管理，必须先初始化仓库。Git 是使用git init命令进行初始化的。请实际建立一个目录并初始化仓库。
  > $ mkdir git-tutorial
   \$ cd git-tutorial
   \$ git init

   如果初始化成功，执行了git init命令的目录下就会生成.git 目录。这.git目录里存储着管理当前目录内容所需的仓库数据。在Git 中，我们将这个目录的内容称为“附属于该仓库的工作树”。文件的编辑等操作在工作树中进行，然后记录到仓库中，以此管理文件的历史快照。如果想将文件恢复到原先的状态，可以从仓库中调取之前的快照，在工作树中打开。
* `git status`——**查看仓库的状态**
* `git add`——**向暂存区中添加文件**
* `git commit`——**保存仓库的历史记录**
  `git commit`命令可以将当前暂存区中的文件实际保存到仓库的历史记录中。通过这些记录，我们就可以在工作树中复原文件。
  记述一行提交信息
  > $ git commit -m "First commit"
    -m 参数后的"First commit"称作提交信息，是对这个提交的概述。
    git commit -am "message"一次性完成add 和commit
* `git log`——**查看提交日志**
  只要在`git log`命令后加上目录名，便会只显示该目录下的日志。如果加的是文件名，就会只显示与该文件相关的日志。
  > $ git log README.md

* `git diff`——**查看更改前后的差别**
  不妨养成这样一个好习惯：在执行`git commit`命令之前先执行`git diff HEAD`命令，查看本次提交与上次提交之间有什么差别，等确认完毕后再进行提交。这里的HEAD 是指向当前分支中最新一次提交的指针。

### 4.2 分支的操作
* `git branch`——**显示分支一览表**
* `git checkout -b`——**创建、切换分支**
  >实际上，连续执行下面两条命令也能收到同样效果。
    > $ git branch feature-A
    > \$ git checkout feature-A
* `git merge`——**合并分支**
    >然后合并feature-A 分支。为了在历史记录中明确记录下本次分支合并，我们需要创建合并提交。因此，在合并时加上--no-ff参数。
    \$ git checkout master
    $ git merge --no-ff feature-A
* `git log --graph`——**以图表形式查看分支**
  git log --graph命令可以用图表形式输出提交日志，非常直观，请大家务必记住.

### 4.3 更改提交的操作
* `git reset`——**回溯历史版本**
  要让仓库的HEAD、暂存区、当前工作树回溯到指定状态，需要用到`git rest --hard`命令。只要提供目标时间点的哈希值A，就可以完全恢复至该时间点的状态。
  > $ git reset --hard fd0cbf0d4a25f747230694d95cac1be72d33441d HEAD is now at fd0cbf0 Add index
  我们已经成功回溯到特性分支（feature-A）创建之前的状态。由于所有文件都回溯到了指定哈希值对应的时间点上，README.md 文件的内容也恢复到了当时的状态。
* `git reflog`——**查看当前仓库的操作日志**。在日志中找出回溯历史之前的 哈希值，通过git reset --hard命令恢复到回溯历史前的状态。

### 4.4 推送至远程仓库
* `git remote add`——**添加远程仓库**
  远程仓库顾名思义，是与我们本地仓库相对独立的另一个仓库。让我们先在GitHub 上创建一个仓库，并将其设置为本地仓库的远程仓库。为防止与其他仓库混淆，仓库名请与本地仓库保持一致
  在GitHub 上创建的仓库路径为“git@github.com:用户名/git-tutorial.git”。现在我们用git remote add命令将它设置成本地仓库的远程仓库A
  > $ git remote add origin git@github.com:github-book/git-tutorial.git
  >按照上述格式执行git remote add命令之后，Git 会自动将git@github.com:github-book/git-tutorial.git远程仓库的名称设置为origin（标识符）。
* `git push`——**推送至远程仓库**
  * > $ git push -u origin master
  像这样执行git push命令，当前分支的内容就会被推送给远程仓库origin 的master 分支。-u参数可以在推送的同时，将origin 仓库的master 分支设置为本地仓库当前分支的upstream（上游）。添加了这个参数，将来运行git pull命令从远程仓库获取内容时，本地仓库的这个分支就可以直接从origin 的master 分支获取内容，省去了另外添加参数的麻烦。
  * >推送至master 以外的分支
     除了master 分支之外，远程仓库也可以创建其他分支。举个例子，我们在本地仓库中创建feature-D 分支，并将它以同名形式push 至远程仓库。
     \$ git checkout -b feature-D
     $ git push -u origin feature-D
     现在，在远程仓库的GitHub 页面就可以查看到feature-D 分支了。

### 4.5 从远程仓库获取
* `git clone`——**获取远程仓库**
  * 获取远程仓库
    > $ git clone git@github.com:github-book/git-tutorial.git
      执行git clone命令后我们会默认处于master 分支下，同时系统会自动将origin 设置成该远程仓库的标识符。也就是说，当前本地仓库的master 分支与GitHub 端远程仓库（origin）的master 分支在内容上是完全相同的。
  * 获取远程的feature-D 分支
    > $ git checkout -b feature-D origin/feature-D
    > -b 参数的后面是本地仓库中新建分支的名称。为了便于理解，我们仍将其命名为feature-D，让它与远程仓库的对应分支保持同名。新建分支名称后面是获取来源的分支名称。例子中指定了origin/feature-D，就是说以名为origin 的仓库（这里指GitHub 端的仓库）的feature-D 分支为来源，在本地仓库中创建feature-D 分支。
  * 向本地的feature-D 分支提交更改
    > $ git commit -am "Add feature-D"
  * 推送feature-D 分支
    > $ git push
    从远程仓库获取feature-D 分支，在本地仓库中提交更改，再将feature-D 分支推送回远程仓库，通过这一系列操作，就可以与其他开发者相互合作，共同培育feature-D 分支，实现某些功能。
* `git pull`——**获取最新的远程仓库分支**
  > $ git pull origin feature-D
  GitHub 端远程仓库中的feature-D 分支是最新状态，所以本地仓库中的feature-D 分支就得到了更新。今后只需要像平常一样在本地进行提交再push 给远程仓库，就可以与其他开发者同时在同一个分支中进行作业，不断给feature-D 增加新功能。

## Chapter6 尝试Pull Request
### 6.1 Pull Request 的概要
* 什么是 Pull Request
  首先我们来理解什么是Pull Request。Pull Request 是自己修改源代码后，请求对方仓库采纳该修改时采取的一种行为。

### 6.2 发送Pull Request 前的准备
* Fork（Github网页上）
* clone
  > \$ git clone git@github.com:hirocastest/first-pr.git
  > $ cd first-pr

  first-pr 目录下会生成Git 仓库。这个仓库与我们GitHub 账户下first-pr 仓库状态相同。现在只要在这个仓库中修改源代码进行push，GitHub 账户中的仓库就会被修改。
* branch 创建特性分支
  > git checkout -b work 
* 提交修改
  > \$ git add index.html
  >   $ git commit -m "Add my impression"
* 创建远程分支
  要从GitHub 发送Pull Request，GitHub 端的仓库中必须有一个包含了修改后代码的分支。我们现在就来创建本地work 分支的相应远程分支。
  > $ git push origin work

### 6.3 发送Pull Request
* 登录GitHub 并切换至work 分支。点击分支名左侧的绿色按钮，会跳转至查看分支间差别的页面（图6.4）。请在这里通过差别查看刚刚进行的更改是否正确。这里显示的东西就是我们本次Pull Request 中包含的提交。确认想要发送的Pull Request 的内容差别无误后，请点击Create PullRequest。确认没有问题后，点击Send pull request 按钮。这样一来，Pull Request 的目标仓库中就会新建Pull Request 和Issue，同时该仓库的管理者会接到通知。
  
### 6.5 仓库的维护
Fork 或clone 来的仓库，一旦放置不管就会离最新的源代码越来越远。如果不以最新的源代码为基础进行开发，劳神费力地编写代码也很可能是白费力气。下面就让我们学习如何让仓库保持最新状态。通常来说clone 来的仓库实际上与原仓库并没有任何关系。所以我们需要将原仓库设置为远程仓库，从该仓库获取（fetch）数据与本地仓库进行合并（merge），让本地仓库的源代码保持最新状态。
* 仓库的 Fork 与 clone
  将octocat/Spoon-Knife 作为原仓库，在GitHub 上进行Fork，然后clone。
  > \$ git clone git@github.com:hirocastest/Spoon-Knife.git
  > $ cd Spoon-Knife
* 给原仓库设置名称
  我们给原仓库设置upstream 的名称，将其作为远程仓库。
  > $ git remote add upstream git://github.com/octocat/Spoon-Knife.git
  > 今后，我们的这个仓库将以upstream 作为原仓库的标识符。这个环境下只需要设定一次。
* 获取最新数据
  > $ git fetch upstream
  >From git://github.com/octocat/Spoon-Knife
  > \* [new branch] master -> upstream/master
  >\$ git merge upstream/master
  > Already up-to-date.

   我们通过 `git fetch` 命令获取最新的数据，将upstream/master 分支与当前分支（master）合并。这样一来，当前分支（master）就获得了最新的源代码。各位在创建特性分支，编辑源代码之前，建议先将仓库更新到这一状态。一般情况下master 分支都会获取最新代码，很少需要Fork 的开发者亲自进行修正。

## Chapter 7 接收pull request
### 7.2 采纳pull request前的准备
**在本地开发环境中反映 Pull Request的内容**
下面我们来讲解收到Pull Request 后在本地开发环境中进行实际检查的流程。在本示例中，Pull Request 接收方的用户名为ituring，发送方的用户名为“PR 发送者”。
* 将接收方的本地仓库更新至最新状态
  首先，将Pull Request 接收方的仓库clone 到本地开发环境中，如果已经clone 过，那么请进行pull 等操作更新至最新状态。
  >\$ git clone git@github.com:ituring/first-pr.git
  > $ cd first-pr
* 获取发送方的远程仓库
  将Pull Request 发送方的仓库设置为本地仓库的远程仓库，获取发送方仓库的数据
  >\$ git remote add PR发送者 git@github.com:PR发送者/first-pr.git
  >$ git fetch PR发送者
 
  现在我们获取了Pull Request 发送方仓库以及分支的数据
* 创建用于检查的分支
  前面我们只获取了远程仓库的数据，这些数据尚未反映在任何一个分支中。因此我们需要创建一个分支，用来模拟采纳Pull Request 后的状态。由于这是我们第一个Pull Request，分支名就叫pr1。
  > $ git checkout -b pr1
* 合并
  下面要将已经fetch 完毕的“PR 发送者/work”的修改内容与pr1分支进行合并。
  > $ git merge PR发送者/work
  >这样一来，pr1 分支中就加入了“PR 发送者/work”分支的修改内容。
* 删除分支 
  检查结束后pr1 分支就没用了，可以直接删除。我们切换至pr1 之外的分支，运行下面的代码。
  > $ git branch -D pr1
### 7.3 采纳pull request
* 完成上述内容后，如果Pull Request 的内容没有问题，大可打开浏览器找出相应的Pull Request 页面，点击Merge pull request 按钮，随后Pull Request 的内容会自动合并至仓库

### 9.5 模拟体验GitHub flow
* 添加新功能，创建新的分支
  * 如果尚未clone 仓库
    > \$ git clone git@github.com:ituring/fizzbuzz.git
    > $ cd fizzbuzz

  * 如果之前clone 过仓库
    >\$ git checkout master
    $ git pull
* 创建特性分支
  > \$ git checkout -b 7-case-output-github
  $ git push -u origin 7-case-output-github

* 实现新功能(在特性分支中作出修改)
  >\$ git commit -am "Add output GitHub"
  > $ git push
* 创建 Pull Request

本笔记摘要参考的GitHub入门与实践
另外附加some reference website
[Git-book](https://git-scm.com/book/en/v2)
[Git](https://git-scm.com)
[learn git branching](https://learngitbranching.js.org/?locale=zh_CN)
[Github 快速入门](https://docs.github.com/zh/get-started/quickstart)