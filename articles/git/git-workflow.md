#Git workflow

![Git workflow][m0]

此文档会详细说明推荐使用的 git 工作流。该工作流包含以下步骤：

- [创建项目][Initialize and set up a project]

- [创建本地代码副本][Git clone]

- [使用 ```feature branch``` 进行开发][Feature branch]

- [使用 ```pull request``` 进行代码评审和合并][Pull request]

- [使用 ```feature branch``` 进行开发、缺陷修复、发布和Hotfix][Workflow]


##Initialize and set up a project

- [创建全新的中央代码库][Set up a new repository]

- [在已有的代码库中创建全新的项目分支][Set up a new branch]

###Set up a new repository

在使用 git 作为代码版本控制的项目中，一般建立项目指创建新的中央代码库 repository 并且提交初始化 commit 。

1.  使用 [```git init```][1] 命令创建 repository 。代码库目录中会有一个 .git 子目录。

    ```bash
        mkdir <project directory>
        cd <project directory>
        git init
    ```

    >**Tip:**

    > 也可以使用以下命令：
    ```bash
        git init <project directory>
        cd <project directory>
    ```

2.  初始化项目，为项目添加基本的 [gitignore][2] 文件和 [README.md][3] 文件。

    ```bash
        wget -Uri <gitignore file Uri from github gitignore repositor> -OutFile .gitignore   
        echo "#<project name>" >> README.md 
        git add .gitignore README.md
        git commit -m "init commit"
    ```
    >**Warning:**

    > 如果是在 Windows 的 PowerShell 中执行以上命令，```echo``` 命令输出的文本可能不是UTF-8编码，需要修改文件编码。
    
    <!-- -->
    
    >**Note:**

    > 你可以在 [github 的 gitignore 项目][4] 中找到所有常用的 gitignore 文件。
    
3.  使用 [```git remote```][5] 和 [```git push```][6] 命令，并且使用 -u 操作符，将初始化后的 repository 推送到中央代码库。

    ```bash
        git remote add origin <remote repository uri>
        git push -u origin master
    ```

例如：

1.  创建 repository：

    ![创建 repository][m1]

2.  初始化项目：

    ![初始化项目][m2]
    
3.  将新建立的项目推送到中央代码库：

    ![推送新创建的代码库][m3]
    
###Set up a new branch

如果项目是将所有的项目共享在相同的 repository 中，则创建新项目是指在 respository 中创建新的分支(branch)。例如：jinyinmao.com.cn 的项目即是如此。

1.  使用 [```git branch```][7] 命令从项目的初始分支（一般为master分支）创建新分支，根据项目的情况，可能需要创建多个分支（开发分支、发布分支）。

    ```bash
        cd <project directory>
        git branch <new branch name> <init branch name>
        git checkout <new branch name>
    ```

    >**Tip:**

    > 也可以使用以下命令：
    ```bash
        cd <project directory>
        git checkout <init branch name>
        git checkout -b <new branch name>
    ```

2.  使用 [```git remote```][5] 和 [```git push```][6] 命令，并且使用 -u 操作符，将初始化后的 Repository 推送到中央代码库。

    ```bash
        git remote add origin <remote Repository uri>
        git push -u origin <new branch name>
    ```
    
    >**Note:**

    > 一般这个时候 remote 已经经过正确配置了，可以忽略 ```git remote add```，只执行如下命令即可：
    ```bash
        git push -u origin <new branch name>
    ```

    例如：

    ![通过创建 branch 建立新项目][m4]

##Git clone

在开发工作开始之前，需要将中央代码库克隆到本地。使用 [```git clone```][8] 命令创建本地代码副本。

```bash
    git clone <remote repository uri> <directory>  
```

>**Tip:**

> 使用以下命令创建本地代码副本，代码的目录名将使用项目的名称：
```bash
    git clone <remote repository uri>
```

例如：

![使用 ```git clone``` 创建本地代码副本][m5]

##Feature branch

![Git feature branch][m6]

Git 的工作流的核心理念是所有的功能开发(feature)、缺陷修补(bugfix)、发布准备(release)、生产补丁(hotfix)都应该在专门的分支（下文中统一称为功能分支--feature branch）上进行，而开发分支（dev 分支或者其它的指定开发分支）和发布分支（master 分支或者其它的指定发布分支）只用来合并经过评审的稳定的分支（下文中统一称为 公共分支）。

开发人员在独立的功能分支上开发，而公共分支只合并稳定的代码。这样便于开发人员专注于特定功能的工作，而不会互相干扰。这也意味着公共分支永远不会包含不稳定的代码，非常有利于进行持续集成。

团队使用 pull request 进行代码合并，每一次 pull request 都需要经过团队的 code review 才能合并进公共分支，以确保公共分支代码的稳定性和风格一致性。同时也有助于促进团队对功能开发和代码质量的沟通。

###How It Works

团队使用一个统一的中央代码仓库，一般可以选择使用 [GitHub][9]、[GitHub Enterprise][10]、[Team Foundation Server][11]、[Bitbucket][12]、[GitLab][13] 搭建 git 服务器，并且托管中央代码仓库。而该代码仓库作为整个团队公认的代码仓库，也成为官方代码库或者中央代码库（下文中统一称为 中央代码库）。

>**Warning:**

> 中央代码库指：托管在 git 服务器上的中央代码仓库。

> 公共分支指：团队约定的开发分支和发布分支的统称。

> 私有代码库指：维护在开发人员本地的代码仓库副本，与 中央代码库 相对应。

> 功能分支：指为开发独立功能而创建的独立代码分支，与 公共分支 相对应。

> 可以将功能分支托管到中央代码库中，公共分支也可以在私有代码库中存在副本。

> 注意区分概念。

在工作中，如果需要开发新功能或者有新的代码提交，不能直接在私有代码库的公共分支上进行开发或者变更提交，即不能在本地的master、dev或者其他公共分支上提交。而是应该由开发人员创建一个新的功能分支进行开发。新分支的创建往往对应着开发人员开始解决某一任务项，功能分支应该具有描述性的名字并且分支名中只能包含 ASCII 字符， 功能分支的命名应该包含2部分，并且按照 ```<feature branch type>/<project name>/<feature branch name>``` 的格式命名（如果项目不是多项目共享 repository 的模式，则不需要在分支名称中包含 project name）。比较推荐的分支名可以是 feature/GieDemo/animated-menu-items 或者 bugfix/issue-#1061，可以透过分支名清晰地获知分支的目的、对应的工作和相关的资源。

>**Note:**

> 功能分支有4中类型，分别是：

> 功能开发 - ```feature```;

> 缺陷修复 - ```bugfix```;

> 发布准备 - ```release```;

> 生产补丁 - ```hotfix```.



功能分支在 git 功能上与公共分支没有任何区别。在功能分支上开发依旧是修改代码、暂存(stage)变更、提交变更集。相对应的命令是 [```git add```][14], [```git commit```][15]。

功能分支可以只保留在本地，也可以推送到中央代码库。推送到中央代码库可以团队中其他的开发人员也可以一起开发该功能分支，并且可以对功能分支进行备份。

>**Warning:**

> 即使功能分支被推送到中央代码库上，该分支依旧不是 公共分支 。

> 注意区分概念。

###Example

以下示例演示如何使用功能分支进行新功能的开发、同样适用于修改BUG、hotfix、进行发布前准备。

1.  Mary 创建新分支：

    ![Mary 创建新分支][m7] 

    在Mary开发新功能的代码之前，她首先需要创建一个新的独立分支，她应该使用如下命令创建分支，其中功能分支名为feature/GitDemo/GDM-issue-001-hello-world，表明该分支是针对GitDemo项目的GDM-issue-001任务的功能开发：

    ```bash
        git checkout -b feature/GitDemo/GDM-issue-001-hello-world dev
    ```

    或者（其中 GitDemo 是项目的公共开发分支）：

    ```bash
        git checkout -b feature/GitDemo/GDM-issue-001-hello-world GitDemo
    ```

    实际操作情况应该和下图类似：
    ![创建功能分支的图示][m8]

    通过以上命令可以将当前 git 工作区切换到 feature/GitDemo/GDM-issue-001-hello-world 分支上，而 -b 操作符表示当需要的分支不存在时则基于 GitDemo 分支创建新分支。在这个分支上可以添加新代码、修改缺陷、暂存变更、提交变更，在这个独立的分支上可以提交任意多的提交，但是需要注意所有的代码变动和提交必需是聚焦在该分支对应的新功能上，不能随意修改继承来的老代码，否则会因为对原有的代码库冲击过大，而合并的时候非常困难。

    ```bash
        git status
        git add <some-file>
        git commit -m "<commit message>"
    ```
    实际操作情况应该和下图类似：
    ![在功能分支中提交代码][m9]
    
    本次提交的代码：
    ![在功能分支中第一次提交的代码][m10]
    
2.  将功能分支推送到中央代码库中：

    ![Mary 暂离][m11]

    Mary 由于开会或者吃午饭需要暂时离开工作，在她离开之前，最好将手头正在开发的功能分支代码推送到中央代码库中，防止该代码分支丢失。如果Mary是和其他同事一起开发此功能，她就需要经常将该分支推送到中央代码库以和其他同事协作。

    ```bash
        git push -u origin feature/GitDemo/GDM-issue-001-hello-world
    ```
    
    实际操作情况应该和下图类似：
    ![将功能分支推送到中央代码库][m12]
    
    >**Tip:**

    > 可以使用 ```git gc``` 命令对代码仓库进行垃圾回收，可以提升代码仓库的性能。

##Pull Request

除了隔离功能开发，使用功能分支并且通过 [```pull request```][16] 发起代码合并请求可以在功能代码合并进公共分支之前，提供合适的代码评审和沟通的方式和时机。一旦有人完成一个功能的开发，团队不会立即将代码合并。相反，开发人员在完成功能的开发后，会将对应的功能分支推送到中央代码库上，并且发起一个 ```pull request``` 通知团队的其他成员进行代码评审，并且在评审后将整个分支进行提交整理再合并到团队的公共分支中。

一旦拉请求被接受，发布功能的实际行动是大致相同的集中式工作流程。首先，你需要确保你的本地主机与上游主同步。然后，合并特性分支成主推更新的主回中央存储库。

在合并了一定量的功能分支后，就可以从公共分支上进行版本发布。公共开发分支可以用于开发环境持续集成，公共发布分支用于版本发布和作为 hotfix 的基线代码。

```pull request``` 的发起和合并一般可以使用成熟的 git 项目管理工具。比如 GitHub 和 Bitbucket。使用方法可以参考 [GitHub pull request documentation][17]、[Bitbucket Server pull request documentation][18]。

###Example

1.  Mary 完成功能分支上的开发工作：

    ![Mary 完成功能开发][m13] 
    
2.  Mary 尝试合并(merge)公共分支的代码以确认功能分支上开发的代码与公共分支上的代码没有冲突，一般只需要检查是否和公共开发分支上的代码是否有冲突：

    合并前的分支情况：
    ![功能分支合并公共分支前的示意图][m14]
    
    >**Note:**
    
    > 上图中的Master代指公共分支。该分支根据情况，可以是 master 分支、dev 分支或者其它的公共分支。在前面的示例中，该分支可以是 GitDemo 分支或者 GitDemo-Release 分支。
    
    ```bash
        git merge GitDemo
    ```
    ![在功能分支上合并开发分支][m15]
    
    如果合并的过程中没有发现冲突，则不需要额外的操作。如果遇到冲突，则需要在功能分支上处理冲突，并且提交处理完冲突的版本。这种方式可以把冲突隔离到相对独立的功能分支中，使得公共分支上不会有冲突的代码。
    
    合并后的分支情况：
    ![功能分支合并公共分支后的示意图][m16]
    
    >**Note:**
    
    > 上图中的Master代指公共分支。该分支根据情况，可以是 master 分支、dev 分支或者其它的公共分支。在前面的示例中，该分支可以是 GitDemo 分支或者 GitDemo-Release 分支。

3.  Mary将合并后的分支推送到中央代码库：

    ![Mary 推送合并后的功能分支][m17]

4.  Mary 使用GUI工具创建 ```pull request```:

    ![创建 ```pull request```][m18]
    
    >**Note:**
    
    > 上图中的界面是Bitbucket的界面。
    
5.  团队的项目管理者 John 收到
 Mary 的 ```pull request``` 通知，并且组织代码评审：
        
     ![收到 ```pull request``` 通知][m19]
     
     ![收到 ```pull request``` 通知][m20]
     
     ![处理 ```pull request```][m21]
     
     代码评审的基本流程为：
     1. 查看功能分支中的代码功能、风格、单元测试是否符合交付标准。如果不通过，则拒绝合并 ```pull request```，开发人员继续该功能分支的代码修改，之后发起新的 ```pull request```；如果通过，进入下一步。
     
     2. 再次合并(merge)公共分支，确保在发起 ```pull request``` 到代码评审完成的期间，功能分支依旧和公共分支的代码没有冲突。如果有冲突，则拒绝合并 ```pull request```，开发人员继续在该功能分支上处理冲突，之后发起新的 ```pull request```；如果通过，进入下一步。
     
     3. 接受并且关闭 ```pull request```，将功能分支的代码合并进公共分支，最后将合并后的公共分支推送到中央代码库。
     
     ```bash
        git checkout GitDemo
        git merge feature/GitDemo/GDM-issue-001-hello-world 
        git push origin GitDemo
     ```
    实际操作情况应该和下图类似：
    ![接受 ```pull request```][m22]

##Workflow

团队可以使用 git 配合公共开发分支、公共发布分支和功能分支（功能）进行日常研发工作。
但是分别在进行功能开发(feature)、缺陷修补(bugfix)、发布准备(release)、生产补丁(hotfix)四种场景下，工作的流程特别是分支的处理上还是会有略微差别。以下会详细说明。

###Feature branches

- 父分支: 公共开发分支，develop
- 目标分支: 公共开发分支，develop
- 命名规则: ```feature/<branch name>``` 或者 ```feature/<project name>/<branch name>```

![git-feature-branches][m23]

每一个新功能的开发，都应该创建一个独立的分支，分支名称应该符合规则 ```feature/<branch name>``` 或者 ```feature/<project name>/<branch name>``` 并且推送到中央代码库进行备份以及团队协作。用于功能开发的分支应该使用公共开发分支作为它的父分支，即分支创建的时候，应该以dev或者团队指定的公共开发分支作为代码基线。当一个用于功能开发的功能分支经过评审后应该合并进公共开发分支。

>**Note:**

> Master代指公共发布分支，Develop代指公共开发分支。

###Bugfix branches

- 父分支: 公共开发分支，develop
- 目标分支: 公共开发分支，develop
- 命名规则: ```bugfix/<branch name>``` 或者 ```bugfix/<project name>/<branch name>```

每一个缺陷的修复也同样应该在独立的功能分支中进行，除创建的分支名称规则不同，应该为 ```bugfix/<branch name>```之外 ，其余和用于功能开发的分支使用方法一致。

特别是用于缺陷修复的分支应该只包含很少量的代码变更，方法测试人员进行针对性的回归测试。而如果某个缺陷需要大量修改代码来修复，则可以直接将该缺陷的修复看作是一个功能点的重新开发，使用 ```Feature branches``` 进行。

###Release branches

- 父分支: 公共开发分支，develop
- 目标分支: 公共发布分支，master 和 公共开发分支，develop
- 命名规则: ```release/<branch name>``` 或者 ```release/<project name>/<branch name>```

![git-release-branches][m24]

一旦开发完成足够的功能，并且代码均经过评审和开发阶段自测，则可以准备进行版本发布。在进行发布准备之前，一般已经将现有的 ```Feature branches``` 和 ```Bugfix branches``` 进行了合并。在这个分支中，团队主要完成release notes的编写、部署文档的编写、编译脚本的编写、还要为该版本创建一个合适的版本号。完成这些工作之后，可以将该分支推送到中央代码库中，并且使用持续集成工具（编译服务器）进行发布包的创建。

使用三级版本号，即 x.y.z 版本号，每次进行发布，新开 ```Release branch``` 则递增第二级版本号，即 1.3.9 到 1.4.1。而在一次发布准备中往往需要进行多次编译尝试和打包，可以每次编译和打包递增第三级版本号，即 1.4.5 到 1.4.6。只有经过较大业务变更，才递增第一级版本号，即 1.4.6 到 2.0.1。

成功打包发布到测试环境后，需要将发布准备分支合并到公共发布分支和公共开发分支。在准备发布的过程中，将停止对其他功能分支的 ```pull request``` 处理，防止发布后的代码合并进公共分支会出现冲突的情况。

由于发布准备实际需要很多的工作，使用独立分支进行发布准备，可以为一些特定于发布的工作定义良好的阶段，从而可以显式地进行发布准备工作。

1.  创建新分支；

    ```bash
        git checkout GitDemo-Release
        git pull origin GitDemo-Release
        git checkout GitDemo
        git pull origin GitDemo
        git merge GitDemo-Release
        git checkout -b release/GitDemo/GDM-issue-010-version-1.4 GitDemo
        git push -u origin release/GitDemo/GDM-issue-010-version-1.4
    ```

2.  进行发布准备工作；

    ```bash
        git add <some-file>
        git commit -m "commit message"
        git push -u origin release/GitDemo/GDM-issue-010-version-1.4
    ```  

3.  使用 [```git tag```][19] 为代码库添加版本；

    ```bash
        git checkout release/GitDemo/GDM-issue-010-version-1.4
        git pull origin GitDemo
        git tag <project name>@<version> -m "Version <project name>@<version>"
        git push origin <project name>@<version> release/GitDemo/GDM-issue-010-version-1.4
    ```
4.  将分支推送到编译服务器上的 git 仓库，尝试编译并且打出版本包；

5.  如果版本号能够成功使用，则创建 ```pull request``` 并且完成评审工作；

6. 合并分支，并且将合并后的分支推送到中央代码库。

    ```bash
        git checkout GitDemo-Release
        git pull origin GitDemo-Release
        git merge release/GitDemo/GDM-issue-010-version-1.4
        git push origin GitDemo-Release
        git checkout GitDemo
        git pull origin GitDemo
        git merge release/GitDemo/GDM-issue-010-version-1.4
        git push origin GitDemo
    ```
    
###Hotfix branches

- 父分支: 公共发布分支中的某一版本
- 目标分支: 公共发布分支，master 和 公共开发分支，develop
- 命名规则: ```hotfix/<branch name>``` 或者 ```hotfix/<project name>/<branch name>```

>**Note:**

> Hotfix分支的合并方法比较复杂，可能需要在公共分支上解决冲突，而且有可能导致后续的很多功能分支出现代码冲突。

![git-release-branches][m25]

```Hotfix branches```  是用于对生产环境进行补丁工作的分支。这也是唯一一种从公共发布分支创建的分支类型。并且为了尽快发布，针对这个补丁的功能开发、缺陷修复、发布准备不再细分分支，而是统一在该 ```Hotfix branches``` 中进行。但是依旧要通过 ```pull request``` 的方式合并进公共分支。特别要注意的是，hotfix 过程中会进行发布，需要更新代码的版本号。

1.  从公共发布分支中检出特定版本的代码（比如是针对1.4.1版本的hotfix）：

    ```bash
        git checkout -b hotfix/GitDemo/GDM-issue-010-version-1.4.1 <project name>@<version>
    ```

2.  完成 hotfix 的开发工作；

3.  使用 [```git tag```][19] 为代码库更新版本；
    ```bash
        git tag -a <project name>@<new version>-hotfix
        git push origin <project name>@<new version>-hotfix hotfix/GitDemo/GDM-issue-010-version-1.4.1  
    ```

4.  将分支推送到编译服务器上的 git 仓库，尝试编译并且打出版本包；

5.  如果版本号能够成功使用，则创建 ```pull request``` 并且完成评审工作；

6. 合并分支，并且将合并后的分支推送到中央代码库。

    ```bash
        git checkout GitDemo-Release
        git pull origin GitDemo-Release
        git merge hotfix/GitDemo/GDM-issue-010-version-1.4.1
        git push origin GitDemo-Release
        git checkout GitDemo
        git pull origin GitDemo
        git merge hotfix/GitDemo/GDM-issue-010-version-1.4.1
        git push origin GitDemo
    ```
    
##More resources

- [Git overview article][20]
- [Git tutorials][21]
- [Git branch][7]
- [Git pull request][16]
- [Bitbucket pull request documentation][18]
 
<!-- Anchors -->
[Initialize and set up a project]: #initialize-and-set-up-a-project
[Set up a new repository]: #set-up-a-new-repository
[Set up a new branch]: #set-up-a-new-branch
[Git clone]: #git-clone
[Feature branch]: #feature-branch
[Pull request]: #pull-request
[Workflow]: #workflow

<!-- Links -->
[1]: ./git-command-git-init.md
[2]: ./git-file-gitignore.md
[3]: ./git-file-readme.md
[4]: https://github.com/github/gitignore
[5]: ./git-command-git-remote.md
[6]: ./git-command-git-push.md
[7]: ./git-command-git-branch.md
[8]: ./git-command-git-clone.md
[9]: https://github.com/
[10]: https://enterprise.github.com/home
[11]: https://www.visualstudio.com/en-us/products/tfs-overview-vs.aspx
[12]: https://bitbucket.org/
[13]: https://about.gitlab.com/
[14]: ./git-command-git-add.md
[15]: ./git-command-git-commit.md
[16]: ./git-pull-request.md
[17]: https://help.github.com/articles/using-pull-requests/
[18]: https://confluence.atlassian.com/bitbucketserver/using-pull-requests-in-bitbucket-server-776639997.html
[19]: ./git-command-git-tag.md
[20]: ./git-articles-overview.md
[21]: https://www.atlassian.com/git/tutorials

<!-- Images -->
[m0]: ./media/git-workflow/git-workflow.png
[m1]: ./media/git-workflow/git-init.png
[m2]: ./media/git-workflow/git-init-commit.png
[m3]: ./media/git-workflow/git-push-repository.png
[m4]: ./media/git-workflow/git-create-branch.png
[m5]: ./media/git-workflow/git-clone.png
[m6]: ./media/git-workflow/git-feature-branch.png
[m7]: ./media/git-workflow/example-git-create-feature-branch.png
[m8]: ./media/git-workflow/example-git-create-feature-branch-2.png
[m9]: ./media/git-workflow/example-feature-branch-first-commit.png
[m10]: ./media/git-workflow/example-feature-branch-first-commit-codes.png
[m11]: ./media/git-workflow/example-go-to-lunch.png
[m12]: ./media/git-workflow/example-feature-branch-git-push.png
[m13]: ./media/git-workflow/example-finish-feature.png
[m14]: ./media/git-workflow/example-before-feature-merge-master.png
[m15]: ./media/git-workflow/example-feature-merge-master.png
[m16]: ./media/git-workflow/example-after-feature-merge-master.png
[m17]: ./media/git-workflow/example-push-feature-branch.png
[m18]: ./media/git-workflow/example-create-pull-request.png
[m19]: ./media/git-workflow/example-receive-pull-request.png
[m20]: ./media/git-workflow/example-access-pull-request.png
[m21]: ./media/git-workflow/example-comment-pull-request.png
[m22]: ./media/git-workflow/example-accept-pull-request.png
[m23]: ./media/git-workflow/git-workflow-feature-branches.png
[m24]: ./media/git-workflow/git-workflow-release-branches.png
[m25]: ./media/git-workflow/git-workflow-hotfix-branches.png