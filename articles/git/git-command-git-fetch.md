# Git fetch

使用 ```git fetch``` 命令可以从远程存储库导入提交到本地仓库的提交。提交会被存储在远程分支中，而不是直接导入本地分支。这样使得有机会在将远程存储库的提交合并到本地分支之前可以进行审查。

## Usage

从远程存储库中获取所有分支。同时下载所有需要的提交和文件。

``` bash
    git fetch <remote>
```

从远程存储库中获取指定的分支。同时下载所有需要的提交和文件。

``` bash
    git fetch <remote> <branch>
```

## Discussion

```git fetch``` 可以获取远程存储库的分支信息、提交信息。由于获取的内容被表示为远程分支，所以对本地开发工作完全没有影响。这使得 ```git fetch``` 是一个安全的方式获取远程存储库的提交，在与本地的存储库合并之前可以审查将要合并的内容。它与 ```svn update``` 类似，它可以让你看到中央代码存储库历史是如何发展的，但是并不强迫你实际地将这些变化合并到你的存储库中。

### Remote Branches

远程分支和本地分支十分类似，除了代表的是远程存储库中分支的提交。你可以像检查本地分支一样检查一个远程分支，但是这会让你处于一个分离的HEAD状态（就像检查一个旧的提交一样）。你可以把它们看作只读分支。要罗列远程分支，只需将 ```-r``` 标志传递给 [```git branch```][3] 命令即可。远程分支以它们所属的远程存储库的名称为前缀，以便您不要将它们与本地分支混淆。 例如，下一个代码片段显示从 [```origin```][4] 获取后可能会看到的分支：

<!-- markdownlint-disable MD031 -->
``` bash
    git branch -r
    # origin/master
    # origin/develop
    # origin/some-feature
```
<!-- markdownlint-enable MD031 -->

你可以用通常的 [```git checkout```][5] 和 [```git log```][6] 命令来检查这些分支。如果您批准远程分支包含的更改，则可以使用正常的 [```git merge```][7] 命令将远程分支上的提交其合并到本地分支中。因此，与SVN不同，将本地存储库与远程存储库同步实际上是一个两步过程：```git fetch```，然后 [```git merge```][7]。[```git pull```][8] 命令是这个过程的一个快捷方式。

## Example

本示例介绍了将本地存储库与中央存储库的主分支同步的典型工作流程。

使用该命令将显示下载的分支：

<!-- markdownlint-disable MD031 MD032 -->
``` bash
    $ git fetch origin
    a1e8fb5..45e66a4 master -> origin/master
    a1e8fb5..9e8ab1c develop -> origin/develop
    * [new branch] some-feature -> origin/some-feature
```
<!-- markdownlint-enable MD031 MD032 -->

如下图所示，这些新的远程分支的提交显示为正方形，原有的本地分支的提交显示为圆圈。正如你所看到的，```git fetch``` 可以让你访问另一个仓库的整个分支结构。

![```git fetch``` 获取 origin 远程分支后的示意图][m1]

要查看已经向上游 ```master``` 分支添加了什么提交，可以使用 origin/master 作为过滤器来运行 [```git log```][9]:

<!-- markdownlint-disable MD031 -->
``` bash
    git log --oneline master..origin/master
```
<!-- markdownlint-enable MD031 -->

使用一下命令将远程分支的提交合并到本地分支中：

<!-- markdownlint-disable MD031 -->
``` bash
    git checkout master
    git log origin/master
    git merge origin/master
```
<!-- markdownlint-enable MD031 -->

```origin/master``` 和 ```master``` 现在指向同一个提交节点，现在本地分支的进度与上游分支进行了同步。

## More resources

- [Git overview article][1]
- [Git tutorials: Collaborating Syncing][2]
- [Git branch][3]
- [Git remote][4]
- [Git checkout][5]
- [Git log][6]
- [Git merge][7]
- [Git pull][8]
- [Git log][9]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/syncing#git-fetch
[3]: ./git-command-git-branch.md
[4]: ./git-command-git-remote.md
[5]: ./git-command-git-checkout.md
[6]: ./git-command-git-log.md
[7]: ./git-command-git-merge.md
[8]: ./git-command-git-pull.md
[9]: ./git-command-git-log.md

<!-- Images -->
[m1]: ./media/git-command-git-fetch/git-command-git-fetch.png
