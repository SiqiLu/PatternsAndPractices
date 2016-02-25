#Git revert

![```git revert``` 示意图][m1]

```git revert``` 命令用于消除错误提交的影响。但是该命令并不是从历史版本记录中移除错误的提交或者撤销提交，而是通过引入一个新的提交来抵消错误提交对代码的影响。使用该命令可以在保证不丢失任何历史记录的情况下，消除错误提交的影响。特别是当错误的提交已经被推送到公共代码库中，或者因为其他原因已经不再是一个私有提交，使用其它会更改版本历史的方法进行撤销，往往会造成其他代码历史的混乱，这个方法则可以保证历史记录的稳定。

##Usage

生成一个新的变更集，在这个变更集中通过撤销所有变更文件中的内容到指定版本，在将这次撤销操作造成的变更集提交到当前分支以消除错误提交的影响。

```bash
    git revert <commit>
```

```git revert``` 和 [```git checkout```][5] 一样，会丢失当前工作区的变更，所以 Git 会强制你先将工作区的变更提交或者清空变更区，才可以使用此命令。

##Discussion

```git revert``` 可以帮助你自动撤销错误提交中所做的所有变更。但是该操作的粒度是提交级别的，无法只撤销提交中的某一个文件的变更。

特别要清晰理解的是，```git revert``` 并不会将版本历史进行回滚，也不会撤销任何提交，而是对错误提交中涉及到的所有的文件变更内容进行操作，这些操作刚好将错误提交涉及的文件内容修改全部撤销掉。再将这些文件内容的变更合并为一个变更集，然后提交到当前分支中。

```git revert``` 不会影响当前提交和错误提交之间的提交内容，但是如果错误提交之后还有提交修改了相同的文件，执行 ```git revert``` 之后可能需要解决冲突。

而在 Git 里，将代码库回滚到一个特定版本，需要使用 [```git reset```][4] 命令。

```git revert``` 和 [```git reset```][4] 的区别如下图所示：

![```git revert``` 和 [```git reset```][4] 的区别示意图][m2]

```git revert``` 相对于回滚历史记录有2个主要优点。第一，不会改变历史记录，使得这个命令是一个安全的操作，可以用于公共代码库和公共提交。第二，回滚历史会丢失当前提交到错误提交之间的所有提交，而 ```git revert``` 只针对错误提交。

##Example

下面例子演示如何使用 ```git revert```，先进行一次提交，并且认定这次提交时错误提交，然后立刻使用 ```git revert``` 消除错误提交的影响：

```bash
    # Edit some tracked files

    # Commit a snapshot
    git commit -m "Make some changes that will be undone"

    # Revert the commit we just created
    git revert HEAD
```

![```git revert``` 的示例][m3]

上图中的的用红色方框表示的错误提交在执行 ```git revert``` 之后依旧会保留在历史记录中。只是添加了一个新的提交抵消错误提交的影响。结果是途中第二个提交时和第四个提交时的代码是完全一致的，而且第三个提交的记录依旧保留在版本历史记录中。

下面例子演示针对之前的某次提交（非上一次）使用 ```git revert``` 的情况，```git revert``` 经常用于进行对功能误加进生产环境问题的 hotfix 。

```bash
    git checkout hotfix
    git revert HEAD~2
```

![```git revert``` 的示例][m4]

##More resources

- [Git overview article][1]
- [Git tutorials: Undoing Changes][2]
- [Git tutorials: Reset, Checkout, and Revert][3]
- [Git reset][4]
- [Git checkout][5]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/undoing-changes/git-revert
[3]: https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting
[4]: ./git-command-git-reset.md
[5]: ./git-command-git-checkout.md

<!-- Images -->
[m1]: ./media/git-command-git-revert/git-revert.png
[m2]: ./media/git-command-git-revert/git-revert-vs-git-reset.png
[m3]: ./media/git-command-git-revert/git-revert-example.png
[m4]: ./media/git-command-git-revert/git-revert-hotfix-example.png
