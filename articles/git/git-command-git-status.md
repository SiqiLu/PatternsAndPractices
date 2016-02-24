#Git status

![查看 Git 代码库的示意图][m1]

```git status``` 命令可以输出工作区和暂存区的当前状态。可以很清晰地展示出哪些变更的文件已经被暂存，哪些变更的文件还未暂存，哪些文件是新添加的还没有被 Git 追踪等等。该命令不会告诉你任何关于版本历史记录的信息，如果需要这方面的信息，可以使用 [```git log```][3] 命令。

##Usage

列出已暂存的变更文件文件(Changes to be committed)、未暂存的变更文件(Changes not staged for commit)、新添加未追踪的文件(Untracked files)。

```bash
    git status
```

##Discussion

[```git status```] 是一个相对简单的命令。它展示了使用 [```git add```][4] 或者 [```git commit```][5] 命令会影响的文件。展示的内容中还包含对文件的相关注释。一般的包含3中类型的文件的状态输出会如下所示：

```bash
# On branch master
# Changes to be committed:
# (use "git reset HEAD <file>..." to unstage)
#
#modified: hello.cs
#
# Changes not staged for commit:
# (use "git add <file>..." to update what will be committed)
# (use "git checkout -- <file>..." to discard changes in working directory)
#
#modified: main.cs
#
# Untracked files:
# (use "git add <file>..." to include in what will be committed)
#
#goodbye.cs
```

##Example

在提交变更之前，最佳实践是先使用 ```git status``` 检查当前 Git 暂存区和工作区的状态，这样可以避免误提交不需要的文件。以下示例展示常见的做法：

```
# Edit hello.cs
git status
# hello.cs is listed under "Changes not staged for commit"
git add hello.cs
git status
# hello.cs is listed under "Changes to be committed"
git commit
git status
# nothing to commit (working directory clean)
```

在示例中，第一次执行 ```git status``` 会输出哪些文件还没有被添加进暂存区。第二次执行会输出执行 [```git add```][4] 的结果，即哪些文件被添加进暂存区。最后一次执行 ```git status``` 会告诉你提交后当前的暂存区是空的，以确认提交的结果。一些命令（比如：```git merge```）会要求当前的暂存区和工作区是空的才可以执行。

##More resources

- [Git overview article][1]
- [Git tutorials: Inspecting a repository][2]
- [Git log][3]
- [Git file: gitignore][6]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-status
[3]: ./git-command-git-log.md
[4]: ./git-command-git-add.md
[5]: ./git-command-git-commit.md
[6]: ./git-file-gitignore.md

<!-- Images -->
[m1]: ./media/git-command-git-status/inspecting-repository.png