# Git clean

```git clean``` 命令用于删除工作目录中所有未跟踪的文件。这是一个非常有用的命令，因为手动查看工作目录中哪些文件没有被跟踪并且手动删除这些文件是十分繁琐并且没有必要的。和普通的 ```rm``` 命令一样，```git clean``` 是不可撤销的，所以在运行之前确保你真的想删除所有未跟踪的文件。

```git clean``` 命令通常与 [```git reset --hard```][3] 一起执行。[```git reset```][3] 仅影响跟踪的文件，因此需要单独的 ```git clean``` 命令来清理未跟踪的文件。结合起来，这两个命令可以将工作目录返回到特定提交的确切状态。

## Usage

执行一次 “dry run”。该命令将告诉你哪些文件将被删除，但是并不会真正删除这些文件。

``` bash
    git clean -n
```

删除当前文件夹下所有的未跟踪文件。```-f``` 只有当 ```clean.requireForce``` 配置被设置为 true 时才需要指定（该配置的默认值为 true）。执行该命令并不会将 [```.gitignore```][4] 中指定的文件夹或者文件删除。

``` bash
    git clean -f
```

只删除符合指定路径的未跟踪文件。

``` bash
    git clean -f <path>
```

删除当前文件夹中的所有未跟踪文件和未跟踪的文件夹。

``` bash
    git clean -df
```

删除当前文件夹中的所有为跟踪文件，同时也会将 [```.gitignore```][4] 中指定的文件删除。

``` bash
    git clean -xf
```

## Discussion

[```git reset --hard```][3] 和 ```git clean -f``` 命令是移除本地存储库中所有临时开发进度的最佳命令组合。运行它们将使你的工作目录匹配至最近的提交节点，并且将移除该节点之后所有的开发进度。

```git clean``` 命令对编译后清理工作目录也很有用。例如，它可以轻松地删除由编译器生成的临时文件。在打包项目之前，这有时是一个必要的步骤。如果是在这种情况下使用命令，可以指定 ```-x``` 选项，这样即使这些临时文件被 [```gitignore```][4]，也可以命令删除。

特别要注意的是，除了 [```git reset```][3] 之外，```git clean``` 是唯一有可能永久删除提交的 Git 命令之一，所以要小心使用。 事实上，很容易误操作导致丢失重要的文件，所以 Git 的作者要求默认情况下使用该命令时需要指定 ```-f``` 标志。这可以防止意外删除所需要的文件。

## Example

以下示例假设已经进行过一些提交，并且在当前的工作区域中做了一些临时开发。现在需要丢弃工作目录中的所有更改，并且需要删除所有已添加的新文件。

<!-- markdownlint-disable MD031 -->
``` base
# Edit some existing files
# Add some new files
# Realize you have no idea what you're doing

# Undo changes in tracked files
git reset --hard

# Remove untracked files
git clean -df
```
<!-- markdownlint-enable MD031 -->

运行这两个命令之后，工作目录和暂存区域将看起来与最近的提交完全一致，并且 [```git status```][5] 将报告一个干净的工作目录。

需要注意的是，与 [```git reset```][3] 中的第二个示例不同，新文件还没有添加到存储库中。因此，这些新添加的文件不会受到 [```git reset --hard```][3] 命令的影响，而只能通过使用 ```git clean``` 删除它们。

## More resources

- [Git overview article][1]
- [Git tutorials: Undoing Changes][2]
- [Git reset][3]
- [gitignore][4]
- [Git status][5]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/undoing-changes#git-clean
[3]: ./git-command-git-reset.md
[4]: ./git-file-gitignore.md
[5]: ./git-commamd-git-status.md
