# Git reset

相对于 [```git revert```][3]，```git reset``` 是一种危险的撤销方法，因为该方法会永久地移除回滚掉的历史，在使用这个命名时要特别小心，并且永远不要回滚公共的版本历史。除了可以回滚到指定的历史版本之外，```git reset``` 还可以撤销保存在暂存区中的变更。

## Usage

从暂存区中移出指定文件，但是该文件的变更不会被撤销，该文件依旧会在工作区保持变更状态。即文件状态从 "Changes to committed" 转变为 "Changes not staged for commit"。

``` bash
    git reset <file>
```

从暂存区中移出所有的文件，但是文件的变更不会被撤销，文件依旧会在工作区保持变更状态。即文件状态从 "Changes to committed" 转变为 "Changes not staged for commit"。

``` bash
    git reset
```

从暂存区中移出所有的文件，并且同时清除工作区中文件的变更，也可以说是用最后一次提交的版本覆盖当前工作目录中的所有文件。

``` bash
    git reset --hard
```

可以使用以下命令让当前分支回滚到指定的历史版本，并且清空暂存区，但是会保留工作区的文件为最后修改的状态。所有在 ```<commit>``` 之后的变更都会被保留在工作区中。这使得开发人员可以重新构建项目历史，设计更加清晰，原子性的提交。

``` bash
    git reset <commit>
```

当然，除了让当前分支的版本历史回滚之外，也可以选择不仅仅清空暂存区，也丢弃工作区中所有文件在 ```<commit>``` 之后的变更。这样操作就像是让 ```<commit>``` 之后的所有变更都没有发生过一样。而且该次回滚很可能无法挽回。

## Discussion

```git reset``` 主要是对历史版本的回滚操作，如果没有 ```--hard``` 操作符，```git reset``` 只会回滚历史版本，但是会保留所有的变更到工作区中，即文件会变成 "Changes not staged for commit" 状态。可以使用该命令重新整理代码库的提交。当你确定某次提交之后的代码没有任何意义，也可以使用 ```--hard``` 彻底丢弃提交后的所有历史和变更。

[```git revert```][4] 是用来安全地处理公共提交的撤销操作，而 ```git reset``` 则是用来设计为撤销私有的提交。具体区别可以参考 [```git revert```][4]。

```git reset``` 是撤销私有提交和私有变更的最常用方法。当你在自己私有的功能分支上突然发现：“哦，XXX，我在做什么？我应该重新开始。”是可以立即使用的方法。除了回滚历史版本，你主要可以使用 ```git reset``` 修改 Git 暂存区或者工作区文件的状态。```git reset``` 在处理提交的时候有三种模式：

- ```--soft``` 只会回滚到指定的历史版本，暂存区和工作区的文件不会被改变。

- ```--mixed``` 回滚到指定的历史版本，并且会清空暂存区，工作区的文件不会被改变。

- ```--hard``` 会回滚到历史版本，暂存区和工作区的变更都会被清空。

![```git reset``` 三种模式示意图][m4]

最常用的2种形式是：

1. 清空暂存区，直接执行 ```git reset``` 其实就是使用缺省参数，效果和下面这个命令相同。

    ``` bash
        git reset --mixed HEAD
    ```
1. 撤销所有未提交到版本库中的变更，包括保存到暂存区中的。

    ``` bash
        git reset --hard HEAD
    ```

如果不想改变版本历史，也不想改变暂存区，只清除暂存区外工作区内的文件的变更，可以在 Git 项目的根目录中执行 ```git checkout .```。

```git reset``` 在处理文件时，没有模式的区分，无论使用 ```--soft```、```--mixed``` 还是 ```--hard```。效果是相同的，只是会把指定版本的该文件移动到暂存区，而工作区的文件不会有变化，参考下图（已确认下图的表示是正确的）。

![```git reset``` 文件的示意图][m5]

### Don’t Reset Public History

千万不要使用 ```git reset``` 回滚任何公共提交。当一个提交被推送到公共分支上或者推送到公共代码库上，则该提交就有可能被其他开发人员使用，并且基于该分支继续开发。如果此时，该公共提交被从版本历史记录中移除，会造成基于该提交继续开发的代码库产生严重的混乱。在公共代码进行同步的过程中，如果有公共提交被移除，就会像代码库的一部分历史凭空消失。下图将示意这个混乱的情况：

![```git reset``` 公共提交的示意图][m1]

参考上图，在回滚后的分支上继续开发，会造成代码库历史的分化，而 Git 的合并操作和同步操作将无法确定需要针对哪一条版本历史进行。所以 ```git reset``` 只能用于本地私有的代码库和私有提交。如果需要修复公共提交的问题，推荐使用 [```git revert```][4] 命令。

## Example

### Unstaging a File

```git reset``` 使用的最合适场景是将文件移出暂存区。下面的例子假设你有2个文件 hello.cs 和 main.cs，并且都分别做了修改。

``` bash
# Edit both hello.cs and main.cs

# Stage everything in the current directory
git add .

# Realize that the changes in hello.cs and main.cs
# should be committed in different snapshots

# Unstage main.cs
git reset main.cs

# Commit only hello.cs
git commit -m "Make some changes to hello.cs"

# Commit main.cs in a separate snapshot
git add main.cs
git commit -m "Edit main.cs"
```

在这个例子中，使用 ```git reset``` 命令将 main.cs 文件移出暂存区，然后只提交 hello.cs 文件的变更，再提交 main.cs 文件的变更，让提交更加细致。

实际案例还可以参考下图：

![```git reset``` 从暂存区移出文件的示例][m5]

### Removing Local Commits

下面的例子假设开发者做了一部分实验性质的代码开发，然后决定彻底放弃这部分代码。然后以下例子就是可以采用的回滚操作：

``` bash
# Create a new file called `foo.cs` and add some code to it

# Commit it to the project history
git add foo.cs
git commit -m "Start developing a crazy feature"

# Edit `foo.cs` again and change some other tracked files, too

# Commit another snapshot
git commit -a -m "Continue my crazy feature"

# Decide to scrap the feature and remove the associated commits
git reset --hard HEAD~2
```

以下命令从 hotfix 分支的顶提交(tip commit) 回滚2个提交。

``` bash
    git checkout hotfix
    git reset HEAD~2
```

![```git reset``` 2个提交的示意图][m3]

## More resources

- [Git overview article][1]
- [Git tutorials: Undoing Changes][2]
- [Git tutorials: Reset, Checkout, and Revert][3]
- [Git revert][4]
- [Git checkout][5]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/undoing-changes#git-reset
[3]: https://www.atlassian.com/git/tutorials/resetting-checking-out-and-reverting
[4]: ./git-command-git-revert.md
[5]: ./git-command-git-checkout.md

<!-- Images -->
[m1]: ./media/git-command-git-reset/git-reset-public-commit.png
[m2]: ./media/git-command-git-reset/git-reset-file-example.png
[m3]: ./media/git-command-git-reset/git-reset-two-commit-example.png
[m4]: ./media/git-command-git-reset/git-reset-flags.png
[m5]: ./media/git-command-git-reset/git-reset-file.png
