# Git pull

使用 ```git fetch``` 命令可以从远程存储库将远程分支上的提交直接合并到本地仓库的分支中。

## Usage

获取当前分支的指定远程副本，并立即将其合并到本地副本中。这跟使用 ```git fetch <remote>```, ```git merge origin/<current-branch>``` 命令组合的结果是一样的。

``` bash
    git pull <remote>
```

和上面的命令一样，但不是使用git merge来将远程分支与本地分支集成在一起，而是使用git rebase。

``` bash
    git pull --rebase <remote>
```

## Discussion

你可以把 ```git pull``` 当成 Git 的 ```svn update``` 版本。这是将本地存储库与上游更改同步的简单方法。下图解释了 ```git pull``` 过程的每一步。

![```git pull``` 过程][m1]

最开始，本地存储库的分支上代码的提交进度和远程存储库上的分支的进展是一致的，但是经过一段时间的开发，你通过使用 [```git fetch```][3]显示自从你上次检查它之后，master的版本已经进步了。然后[```git merge```][4] 立即将远程分支上的提交合并到本地分支。

## Example

以下示例演示了将远程中央存储库的 ```master``` 分支合并到本地的 ```master```分支。

``` bash
    git checkout master
    git pull origin master
```

## More resources

- [Git overview article][1]
- [Git tutorials: Collaborating Syncing][2]
- [Git fetch][3]
- [Git merge][4]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/syncing#git-pull
[3]: ./git-command-git-fetch.md
[4]: ./git-command-git-merge.md

<!-- Images -->
[m1]: ./media/git-command-git-pull/git-command-git-pull.png
