# Git checkout

在 Git 中，`git checkout` 是一个功能非常丰富的命令，有很多用途，从命令本身的功能就可以分为三种：

- [签出文件][File level]

- [签出提交][Commit level]

- [签出分支][Branch level]

版本控制系统最主要的功能就是安全地保存整个项目的所有历史记录，以防止开发人员对项目的源代码造成无法恢复的破坏。在一个 Git 管理的项目中，`git checkout` 是一种简单稳定的签出特定历史版本的方法。

## File-level Operations

`git checkout` 命令可以接受文件路径作为参数。在这种情况下，`git checkout` 的操作仅针对此文件。执行该命令会将工作区中的文件回滚到该文件最后提交到版本历史记录中的最后一次快照版本。在工作区或者暂存区中对该文件的变更将被丢弃。

![`git checkout` 文件的示意图][m1]

### Usage

将工作区中的某个文件回滚到最后一次提交的版本。

``` bash
    git checkout <file>
```

将工作区中的某个文件回滚到某一次提交的版本。

``` bash
    git checkout <commit> <file>
```

### Discussion

签出老版本的文件会覆盖当前工作区中的文件，并且会清除暂存区中该文件的变更。如果签出版本的文件与最后一次提交的该文件内容不同，还可以再次提交该文件，方法和提交其它的变更的文件完全相同。

![`git checkout` 文件并且再次提交的示意图][m2]

### Example

可以使用 `git checkout` 签出老版本的文件。比如，你指向查看提交a1e8fb5时*hello.cs*文件的内容，你可以执行以下命令：

``` bash
    git checkout a1e8fb5 hello.cs
```

使用 [`git status`][8] 查看当前 Git 代码库的状态，会发现签出的老版本文件，一般是有变更的文件(Change to be committed)，你可以直接提交此时的该文件，即可以将该文本回滚到提交a1e8fb5时的版本。如果你不想回滚到老版本，你可以签出最新版本的该文件，命令如下：

``` bash
    git checkout HEAD hello.cs
```

## Commit-level Operations

![`git checkout` 提交的示意图][m3]

`git checkout` 命令可以接受 `commit ID` （提交的摘要值） 或者 `tag` 作为参数。签出提交，会使得整个工作区切换到该次提交对应的历史版本快照，但是并不会回滚或者丢失任何版本历史记录。可以使用这个方法查看任意一次提交后的项目状态。

### Usage

切换工作区中的所有文件到某个指定提交时的快照版本。如果在指定提交时，该文件还没有被 Git 追踪，则切换后的工作区中就不会有该文件。

``` bash
    git checkout <commit>
```

### Discussion

`git checkout` 分支是只读操作，不需要担心这种操作会破坏项目的历史记录。在进行签出操作时，项目的当前状态依旧保存在项目的历史记录中，并且不会被改变或者丢失。例如，假设我们使用 `master` 分支作为当前分支，在开发工作中，HEAD 作为当前提交的引用，一般是指向当前分支的顶提交(tip commit)的快照版本，但是当使用 `git checkout` 命令签出某一提交时，HEAD 将不再指向分支的顶提交快照版本，而是直接指向签出的提交快照版本。这个情况下， HEAD 被称为 "detached HEAD" （分离头），如下图示意：

![`git checkout` 提交的示意图][m4]

关键字 HEAD 在 Git 中引用当前的提交。在 `git checkout` 的实现上，实际是改变 HEAD 指向的提交。当签出某一个提交时，HEAD 就变为 "detached HEAD" （分离头）。

![`git checkout` 提交后分离头的示意图][m7]

可以使用 ```~``` 分支的相对引用签出提交版本，HEAD 的指向也会改变。

``` bash
    git checkout HEAD~2
```

![`git checkout` 提交的示意图][m10]

这其实是明确地提醒开发者，在签出提交后所进行的开发已经与原开发的历史记录分离。如果你在 "detached HEAD" （分离头）引用的提交版本的基础上继续进行开发，你其实是在一个不存在的分支上进行开发，一旦离开这个分支，就无法再切换回来。所有在这个分支上提交的提交版本都会丢失。

![`git checkout` 基于分离头开发会造成不存在的分支][m8]

开发工作应该始终在已经存在的分支上进行，而不能基于"detached HEAD" （分离头）进行，除非只是想在过去的历史上做一些实验，而且这些实验代码没有保留的价值。

### Example

这个例子假设你在 `master` 分支上进行一个疯狂实验的开发，但你不知道是否需要保留这些实验的代码。为了确认项目的情况，你希望查看下在开始实验之前项目代码的状态。首先，需要找到开始实验之前的提交的 `commit ID`。

``` bash
    git log --oneline
```

执行命令查看的项目历史如下所示：

``` bash
    b7119f2 Continue doing crazy things
    872fa7e Try something crazy
    a1e8fb5 Make some important changes to hello.cs
    435b61d Create hello.cs
    9773e52 Initial import
```

现在可以使用 `git checkout` 查看a1e8fb5提交时的内容：

``` bash
    git checkout a1e8fb5
```

执行以上命令会使当前工作区的文件切换回提交a1e8fb5时的状态。可以查看文件，编译项目，执行测试甚至可以修改文件，而不用担心丢失项目中已经保存的任何的历史记录。但是在这个状态下所做的任何修改都不会保存到项目的版本历史记录中。要继续开发，你只需要回到项目的顶提交即可(tip commit)：

``` bash
    git checkout master
```

一旦你回到了分支的顶提交(tip commit)，你可以使用 [`git revert`][6] 命令或者 [`git reset`][7] 命令撤销不再需要的版本历史。

![`git checkout` 提交的示例][m5]

## Branch-level Operations

`git checkout` 命令可以接受分支名作为参数。签出分支，即是切换分支，会把工作区中的文件全部更新为指定分支中顶提交(tip commit)版本中的文件，并且之后的提交会提交到切换后的分支。

### Usage

切换当前工作区到指定的分支。

``` bash
    git checkout <existing-branch>
```

`git checkout` 还可以创建出新的分支，同时切换到该分支。使用 `-b` 操作符可以让 Git 先创建出新分支，再切换到新创建的分支。如果提供 `<existing-branch>` 参数，则新分支就以 `<existing-branch>` 为基线创建，否则就以执行命令时工作区所处的分支为基线进行创建。`<existing-branch>` 也可以是远程分支。关于分支创建的更多信息，可以参考 [`git branch`][9]。

``` bash
    checkout -b <new-branch> <existing-branch>
```

### Discussion

在分支级别上的操作，`git checkout` 经常需要和 [`git branch`][9] 配合使用。当需要创建并且使用一个新的功能分支时，可以先使用 [`git branch`][9] 创建新分支，然后使用 `git checkout` 切换到新的分支上进行工作。也可以直接使用 `git checkout -b` 完成创建新分支并且切换的需求。

![`git checkout` 分支的示例][m6]

使用特定独立的分支进行功能的开发，是使用 Git 的工作流相对于使用 SVN 的工作流的转变。这使得使用 Git 很容易进行尝试性开发，而不用担心对公共代码的影响。

和对提交进行签出类似，对分支进行签出，Git 的内部实现，实际也是变更 HEAD 的指向。签出分支会丢失你当前分支上未提交的工作，所以 Git 会强制要求提交当前的所有变更或者清空变更后，才可以签出分支。

![`git checkout` 分支前后的 HEAD 的示意图][m9]

### Example

下面例子演示在日常的 Git 工作流出使用 `git checkout` 对分支进行处理。当你需要开发一个新功能时，使用以下命令创建一个新分支并且切换到新分支上：

``` bash
    git branch new-feature
    git checkout new-feature
```

之后，你可以提交一些变更：

``` bash
    # Edit some files
    git add <file>
    git commit -m "Started work on a new feature"
    # Repeat
```

这些变更会被提交到新的功能分支中，你可以根据需要添加任意数量的提交。当需要切换回公共开发分支时（假设是 master 分支），可以执行以下命令：

``` bash
    git checkout master
```

在这个分支上，你可以将功能分支合并进来，或者创建新的分支进行新功能的开发，亦或者进行版本发布。

## More resources

- [Git overview article][1]
- [Git tutorials: Viewing old commits][2]
- [Git tutorials: Undoing Changes][3]
- [Git tutorials: Using Branches][4]
- [Git tutorials: Reset, Checkout, and Revert][5]
- [Undo anything in Git][10]
- [Git branch][9]
- [Git revert][6]
- [Git reset][7]

<!-- Anchors -->
[File level]: #file-level-operations
[Commit level]: #commit-level-operations
[Branch level]: #branch-level-operations

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/viewing-old-commits
[3]: https://www.atlassian.com/git/tutorials/undoing-changes/git-checkout
[4]: https://www.atlassian.com/git/tutorials/using-branches/git-checkout
[5]: https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting
[6]: ./git-command-git-revert.md
[7]: ./git-command-git-reset.md
[8]: ./git-command-git-status.md
[9]: ./git-command-git-branch.md
[10]: ./git-undo-anything.md

<!-- Images -->
[m1]: ./media/git-command-git-checkout/git-checkout-file.png
[m2]: ./media/git-command-git-checkout/git-checkout-recommit-file.png
[m3]: ./media/git-command-git-checkout/git-checkout-tag.png
[m4]: ./media/git-command-git-checkout/git-checkout-commit.png
[m5]: ./media/git-command-git-checkout/git-checkout-commit-example.png
[m6]: ./media/git-command-git-checkout/git-checkout-branch.png
[m7]: ./media/git-command-git-checkout/git-checkout-commit-detached-HEAD.png
[m8]: ./media/git-command-git-checkout/git-checkout-commit-non-existent-branch.png
[m9]: ./media/git-command-git-checkout/git-checkout-branch-HEAD.png
[m10]: ./media/git-command-git-checkout/git-checkout-commit-reference.png