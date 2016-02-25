#Git commit

![```git commit``` 示意图][m1]

```git commit``` 命令用于将保存在暂存区的变更作为一个变更集原子性地提交到代码库的版本记录中。已经提交的变更集可以认为是一个被 Git 承诺持久记录的版本记录，除非被明确要求进行回滚，否则该变更集将持续保持稳定。和 ```git add``` 类似，```git commit``` 是 Git 最重要的命令之一。

##Usage

使用 ```git commit``` 提交暂存的变更集。Git 会打开文本编辑器，要求你输入本次提交的描述信息。当完成提交信息的编辑，保存文件并且关闭编辑器就可以完成一次变更集的提交。

```bash
    git commit
```

除了使用文本编辑器输入提交信息以外，还可以直接在执行提交命令的同时完成提交信息的编辑工作。可以使用 ```-m``` 操作符，然后传入想要提交的信息作为参数：

```bash
    git commit -m "<message>"
```

可以一次性提交工作区中所有有变更的文件，只会包含已经被 Git 追踪的文件中（已追踪的文件是指已经被提交到 Git 版本记录中的文件）。

```bash
    git commit -a
```

##Discussion

变更集只会背提交到*本地的代码库*中。这和 SVN 有很大不同，在 SVN 中变更集是直接提交到中央公共代码库中。相比之下，在 Git 的工作流程中，首先所有的操作都发生在本地的代码库中，只有当你确认所有的操作都正确的情况下，才需要你将本地代码库和远程的中央公共代码库进行同步。正如暂存区是工作区和代码库版本历史记录之间的缓存区，每个开发者的本地代码库是他们的变更集和中央公共代码库之间的缓存区。

使用 Git 往往会改变开发者的工作流程。使用 Git 意味着开发者不再是将自己的代码直接提交到中央公共代码库中，而是将变更集先提交到本地代码库中，再同步到中央公共代码库中。这个模式比 SVN 模式有很多优点：

1.  可以更容易地将功能切分为变更集进行原子提交；

2.  更好地对相关的变更集进行组织；

3.  可以在提交到公共代码库之前，先在本地代码库进行充分的检查工作；

4.  开发者可以在独立的环境中开发，甚至是在离线的情况下，也可以对变更集进行提交和版本控制，直到合适的时间点，再将所有变更提交统一同步到公共代码库中。

###Snapshots, Not Differences

Git 和 SVN 除了功能上的区别外，他们的底层实现也遵循了完全不同的设计理念。SVN 跟踪文件的差异，而 Git 的版本控制基于对文件的快照。例如，SVN 提交会比较当前文件与原始文件的差异，并且通过保存差异实现对文件的版本控制；而 Git 会记录每次提交发生变更的文件的整个内容，并且通过保存文件的快照实现对文件的版本控制。

>**Tip:**

> Git 在存储文件快照的实现上也使用了保存文件差异的方法。

![SVN 与 Git 文件版本控制机制示意图][m2]

因为 Git 获取特定版本的文件不再需要通过基线版本文件和大量的差异文件进行重建，而是可以直接从快照中读取。

Git 基于快照的实现对它版本控制模型影响深远，从它的分支切换到历史回滚，从差异对比到冲突合并的各个方面都受此影响巨大。

##Example

下面的例子假设你已经创建了一个名为 ```hello.cs``` 的文件，并且在该文件中添加了一些内容，并准备将其提交到该项目的历史记录中。首先，你需要使用 Git 将该文件添加到暂存区中，之后将该次变更集提交。

```bash
    git add hello.cs
    git commit
```

执行以上命令后，Git 会打开文本编辑器（可以通过 [```git config```]进行配置）要求在一个文件中编辑一段提交信息，同时该文件中还会有一些被注释掉的提示信息可供参考:

```
# Please enter the commit message for your changes. Lines starting
# with '#' will be ignored, and an empty message aborts the commit.
# On branch master
# Changes to be committed:
# (use "git reset HEAD <file>..." to unstage)
#
#modified: hello.cs
```

Git 并不会强制要求提交信息遵循特定的格式，但是一般会在第一行用50个字以内的文字简述该次提交的目的，然后空一行，再编辑详细的变更信息。

```
修改 hello.cs 中输出的消息

- 修改 SayHello() 方法输出包含用户姓名的消息
- 修改 SayGoodbye() 方法输出更加友好的消息
```

在提交信息中如果使用英文，推荐使用一般现在时。

##More resources

- [Git overview article][1]
- [Git tutorials: Saving changes][2]
- [Git commit --amend][3]
- [Git status][4]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/saving-changes/git-commit
[3]: ./git-commit-amend.md
[4]: ./git-command-git-status.md

<!-- Images -->
[m1]: ./media/git-command-git-commit/git-commit.png
[m2]: ./media/git-command-git-commit/git-svn-history-records.png