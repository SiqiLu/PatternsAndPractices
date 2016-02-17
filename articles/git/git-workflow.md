#Git workflow

![Git workflow][m0]

此文档会详细说明推荐使用的 git 工作流。该工作流包含以下步骤：

- [创建项目][Initialize and set up a project]

- [创建本地代码副本][Git clone]

- [使用 ```feature branch``` 进行开发][Feature branch]

- [使用 ```pull request``` 进行代码评审和合并][Pull request]




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

Git 的工作流的核心理念是所有的功能开发、BUG修补、hotfix、发布都应该在专门的分支（下文中统一称为功能分支--feature branch）上进行，而开发分支（dev 分支或者其它的指定开发分支）和发布分支（master 分支或者其它的指定发布分支）只用来合并经过评审的稳定的分支（下文中统一称为 公共分支）。

开发人员在独立的功能分支上开发，而公共分支只合并稳定的代码。这样便于开发人员专注于特定功能的工作，而不会互相干扰。这也意味着公共分支永远不会包含不稳定的代码，非常有利于进行持续集成。

团队使用 pull request 进行代码合并，每一次 pull request 都需要经过团队的 code review 才能合并进公共分支，以确保公共分支代码的稳定性和风格一致性。同时也有助于促进团队对功能开发和代码质量的沟通。

###How It Works

团队使用一个统一的中央代码仓库，一般可以选择使用 [GitHub][9]、[GitHub Enterprise][10]、[Team Foundation Server][11]、[Bitbucket][12]、[GitLab][13] 搭建 git 服务器，并且托管中央代码仓库。而该代码仓库作为整个团队公认的代码仓库，也成为官方代码库或者公共代码库（下文中统一称为 公共代码库）。

>**Warning:**

> 公共代码库指：托管在 git 服务器上的中央代码仓库。

> 公共分支指：团队约定的开发分支和发布分支的统称。

> 私有代码库指：维护在开发人员本地的代码仓库副本，与 公共代码库 相对应。

> 功能分支：指为开发独立功能而创建的独立代码分支，与 公共分支 相对应。

> 可以将功能分支托管到公共代码库中，公共分支也可以在私有代码库中存在副本。

> 注意区分概念。

在工作中，如果需要开发新功能或者有新的代码提交，不能直接在私有代码库的公共分支上进行开发或者变更提交，即不能在本地的master、dev或者其他公共分支上提交。而是应该由开发人员创建一个新的功能分支进行开发。新分支的创建往往对应着开发人员开始解决某一任务项，功能分支应该具有描述性的名字并且分支名中只能包含 ASCII 字符， 功能分支的命名应该包含2部分，并且按照 ```<feature branch type>/<feature branch name>``` 的格式命名。比较推荐的分支名可以是 feature/animated-menu-items 或者 bugfix/issue-#1061，可以透过分支名清晰地获知分支的目的、对应的工作和相关的资源。

功能分支在 git 功能上与公共分支没有任何区别。在功能分支上开发依旧是修改代码、暂存(stage)变更、提交变更集。相对应的命令是 [```git add```][14], [```git commit```][15]。

功能分支可以只保留在本地，也可以推送到公共代码库。推送到公共代码库可以团队中其他的开发人员也可以一起开发该功能分支，并且可以对功能分支进行备份。

>**Warning:**

> 即使功能分支被推送到公共代码库上，该分支依旧不是 公共分支 。

> 注意区分概念。

###Example

以下示例演示如何使用功能分支进行新功能的开发、同样适用于修改BUG、hotfix、进行发布前准备。

1.  Kate 创建新分支：

    ![Kate 创建新分支][m7] 

    在Kate开发新功能的代码之前，她首先需要创建一个新的独立分支，她应该使用如下命令创建分支，其中功能分支名为feature/GDM-issue-001-hello-world，表明该分支是针对GDM项目的001任务的功能开发：

    ```bash
        git checkout -b feature/GDM-issue-001-hello-world dev
    ```

    或者（其中 GitDemo 是项目的公共开发分支）：

    ```bash
        git checkout -b feature/GDM-issue-001-hello-world GitDemo
    ```

    实际操作情况应该和下图类似：
    ![创建功能分支的图示][m8]

    通过以上命令可以将当前 git 工作区切换到 feature/GDM-issue-001-hello-world 分支上，而 -b 操作符表示当需要的分支不存在时则基于 GitDemo 分支创建新分支。在这个分支上可以添加新代码、修改缺陷、暂存变更、提交变更，在这个独立的分支上可以提交任意多的提交，但是需要注意所有的代码变动和提交必需是聚焦在该分支对应的新功能上，不能随意修改继承来的老代码，否则会因为对原有的代码库冲击过大，而合并的时候非常困难。

    ```bash
        git status
        git add <some-file>
        git commit -m "<commit message>"
    ```
    实际操作情况应该和下图类似：
    ![在功能分支中提交代码][m9]
    
    本次提交的代码：
    ![在功能分支中第一次提交的代码][m10]
    
2.  将功能分支推送到公共代码库中：

    ![Kate 暂离][m11]

    Kate 由于开会或者吃午饭需要暂时离开工作，在她离开之前，最好将手头正在开发的功能分支代码推送到公共代码库中，防止该代码分支丢失。如果Kate是和其他同事一起开发此功能，她就需要经常将该分支推送到公共代码库以和其他同事协作。

    ```bash
        git push -u origin feature/GDM-issue-001-hello-world
    ```
    
    实际操作情况应该和下图类似：
    ![将功能分支推送到公共代码库][m12]
    
    >**Tip:**

    > 可以使用 ```git gc``` 命令对代码仓库进行垃圾回收，可以提升代码仓库的性能。

##Pull Requests

除了隔离功能开发，使用功能分支并且通过 [```pull request```][16] 发起代码合并请求可以在功能代码合并进公共分支之前，提供合适的代码评审和沟通的方式和时机。一旦有人完成一个功能的开发，团队不会立即将代码合并。相反，开发人员在完成功能的开发后，会将对应的功能分支推送到公共代码库上，并且发起一个 ```pull request``` 通知团队的其他成员进行代码评审，并且在评审后将整个分支进行提交整理再合并到团队的公共分支中。

一旦拉请求被接受，发布功能的实际行动是大致相同的集中式工作流程。首先，你需要确保你的本地主机与上游主同步。然后，合并特性分支成主推更新的主回中央存储库。

在合并了一定量的功能分支后，就可以从公共分支上进行版本发布。公共开发分支可以用于开发环境持续集成，公共发布分支用于版本发布和作为 hotfix 的基线代码。

```pull request``` 的发起和合并一般可以使用成熟的 git 项目管理工具。比如 GitHub 和 Bitbucket。使用方法可以参考 [GitHub pull request documentation][17]、[Bitbucket Server pull request documentation][18]。

###Example



<!-- Anchors -->
[Initialize and set up a project]: #initialize-and-set-up-a-project
[Set up a new repository]: #set-up-a-new-repository
[Set up a new branch]: #set-up-a-new-branch
[Git clone]: #git-clone
[Feature branch]: #feature-branch
[Pull request]: #pull-request

<!-- Links -->
[1]: ./git-command-git-init..md
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

<!-- Images -->
[m0]: ./media/git-workflow/git-workflow.svg
[m1]: ./media/git-workflow/git-init.png
[m2]: ./media/git-workflow/git-init-commit.png
[m3]: ./media/git-workflow/git-push-repository.png
[m4]: ./media/git-workflow/git-create-branch.png
[m5]: ./media/git-workflow/git-clone.png
[m6]: ./media/git-workflow/git-feature-branch.svg
[m7]: ./media/git-workflow/example-git-create-feature-branch.svg
[m8]: ./media/git-workflow/example-git-create-feature-branch.png
[m9]: ./media/git-workflow/example-feature-branch-first-commit.png
[m10]: ./media/git-workflow/example-feature-branch-first-commit-codes.png
[m11]: ./media/git-workflow/example-kate-goes-to-lunch.svg
[m12]: ./media/git-workflow/example-feature-branch-git-push.png