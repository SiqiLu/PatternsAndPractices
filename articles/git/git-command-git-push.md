# Git push

```git push``` 命令可以将本地存储库上的提交推送到远程存储库的分支上。该命令与 [```git fetch```][3]相对，[```git fetch```][3] 是将远程存储库上的提交导入到本地分支，```git push``` 是将本地存储库上的提交推送到远程存储库。 这有可能会覆盖更改，所以您需要小心如何使用它。 这些问题在下面讨论。

## Usage

将指定的分支连同所有必需的提交和内部对象一起推送到 ```<remote>```。 这会在目标存储库中创建一个和本地分支同名的新分支。为了防止覆盖提交，Git 在目标资源库中无法非快进合并时不会允许 ```git push```。

<!-- markdownlint-disable MD031 -->
``` bash
    git push <remote> <branch>
```
<!-- markdownlint-enable MD031 -->

与上述命令相同，但强制推送即使导致非快进合并。除非你确定你知道你在做什么，否则不要使用 ```--force``` 标志。

<!-- markdownlint-disable MD031 -->
``` bash
    git push <remote> --force
```
<!-- markdownlint-enable MD031 -->

将所有本地分支推送到指定的远程存储库。

<!-- markdownlint-disable MD031 -->
``` bash
    git push <remote> --all
```
<!-- markdownlint-enable MD031 -->

当您推送分支或使用 ```--all``` 选项时，不会自动推送标签。```--tags``` 标志将所有本地标签推送到远程存储库。

<!-- markdownlint-disable MD031 -->
``` bash
    git push <remote> --tags
```
<!-- markdownlint-enable MD031 -->

## Discussion

```git push``` 最常见的用例是将你的本地更改发布到中央存储库。积累了多个本地提交并准备与团队其他成员共享之后，您可以（可选）使用交互式重新整理来清理它们，然后将其推送到中央存储库。

![```git pull```][m1]

上图显示了当本地 ```master``` 分支的进度超过远程中央存储库的 ```master``` 分支的进度时，通过执行 ```git push origin master``` 来发布更改。请注意，```git push``` 与从远程存储库中运行 ```git merge master``` 是基本相同的。

### Force Pushing

Git会阻止您在导致非快进合并时的推送请求，从而保护中央存储库的历史记录不会被随意覆盖。所以，如果远程历史与您的历史有所不同，您需要拉远程分支并将其合并到本地，然后再次尝试推送。这与SVN在提交变更集之前通过svn update与中央库进行同步的方式类似。

```--force``` 标志表示推送是一次强制推送，并使远程存储库的分支与本地分支相匹配，从而删除自上次提交以来可能发生的任何上游更改。唯一需要强制推送的情况是，当你意识到你刚分享的提交不是很正确的时候，你用一个 [```git commit```][4]或者一个交互式 ```rebase``` 来修复它们。但是，在使用 ```--force``` 选项之前，您必须绝对确定您的队友没有任何提交。

### Only Push to Bare Repositories

你只能将本地提交推送到已经用 ```--bare``` 标志创建的仓库。因为使用推送可以修改远程存储库上的进度和历史，所以不要推送到其他开发人员的存储库。由于 ```bare``` 存储库没有工作目录，推送到 ```bare``` 存储库是相对安全的。

## Example

以下示例描述了将本地提交发布到中央存储库的标准方法之一。首先，通过获取中央存储库的副本并确保您的本地分支的进度是最新的。此时也是进行交互式 ```base``` 整理提交的好机会。然后，使用 ```git push``` 命令会将本地分支上的所有提交发送到远程中央存储库。

<!-- markdownlint-disable MD031 -->
``` bash
    git checkout master
    git fetch origin master
    git rebase -i origin/master
    # Squash commits, fix up commit messages etc.
    git push origin master
```
<!-- markdownlint-enable MD031 -->

因为我们已经确定本地的 ```master``` 分支的进度和远程存储库上的 ```master``` 分支的进度是同步的，所以这次推送应该导致一个 ```fast-forward```。

## More resources

- [Git overview article][1]
- [Git tutorials: Collaborating Syncing][2]
- [Git fetch][3]
- [Git commit][4]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/syncing#git-push
[3]: ./git-command-git-fetch.md
[4]: ./git-command-git-commit.md

<!-- Images -->
[m1]: ./media/git-command-git-push/git-command-git-push.png
