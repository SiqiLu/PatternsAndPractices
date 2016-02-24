#Git commit --amend

```git commit --amend``` 命令是修改最近一次提交的最简单的方法，该方法只能添加新的变更文件到最近的一次提交中或者修改最近一次提交的提交信息。该命令会将暂存区中的变更集和最近一个提交的变更集合并为一个变更集，并且允许你再次修改提交信息，从而达到修改最近一次提交的效果，该命名不会创建新的提交。

![```git commit --amend``` 示意图][m1]

Git 修改提交实际上并不是修改了最近一次提交，而是完全替换最近一次提交，如上图中有星号(```*```)标识的的提交。只能在本地私有代码库中使用该操作，如果修改已经存在于公共代码库中的提交，造成其它已经继承于该公共分支的代码产生混乱。

##Usage

合并暂存区的变更集和最近一次提交中的所有变更集，将产生的新变更集提交，并且完全覆盖最近一次的提交。当然该命令也可以用于仅仅修改最近一次提交的提交信息。

```bash
    git commit --amend
```

##Discussion   

在日常开发中，经常会有不完善的提交。很容易在提交中遗漏部分有变更的文件，也可能忘记格式化提交信息。使用 ```git commit --amend``` 命令是修复这些问题的很方便的方法。

###不要修改公共的提交

>**Important:**

> 公共代码库中存在的提交，或者继承于公共代码库中的任意提交，都被认为是**公共提交**。只有只存在于本地私有代码库中、从来没有被同步到任何公共代码库中的提交才可以认为是**私有提交**。

在我们讨论 [```git reset```][4] 命令时，我们还会讨论**不要**修改任何公共提交。同样，```git commit -amend``` 命令也**不要**用于修改任何公共提交。

使用 ```git commit -amend``` 命令修改后的提交是一个完完全全的新提交，被修改的提交会从版本记录中移除。如果使用该命令修改公共提交，也会从公共代码库中将该提交从历史纪录中移除，如果该公共提交已经被其他的开发人员继承，并且他们已经基于该提交进行了开发，他们会发现他们的代码的历史基础消失了。这会导致包含被修改的提交的代码都产生混乱。

##Example

下面的例子是使用 Git 的过程中常常会遇到的一个场景。首先修改了一部分文件，并且希望在一个变更集中同时提交这些文件，但是在提交的过程中遗漏了其中一个文件。我们就可以使用 ```git commit -amend``` 命令修复这个问题。

```
# Edit hello.cs and main.cs
git add hello.cs
git commit

# Realize you forgot to add the changes from main.cs
git add main.cs
git commit --amend --no-edit
```

使用 ```git commit -amend``` 命令时，Git 会打开文本编辑器并且允许你基于被修改的提交的提交信息编辑出新的提交信息。如果完全不需要编辑提交信息，而是保持修改后的提交的信息和修改前的提交的信息一致，可以使用 ```--no-edit``` 操作符。执行以上命令之后，新的提交会替换被修改的提交，看起来就像我们当初就将 hello.cs 和 main.cs 在一个变更集中一次提交到版本历史中。

##More resources

- [Git overview article][1]
- [Git tutorials: Rewriting history][2]
- [Git commit][3]
- [Git checkout][4]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/rewriting-history/git-commit--amend
[3]: ./git-command-git-commit.md
[4]: ./git-command-git-checkout.md

<!-- Images -->
[m1]: ./media/git-commit-amend/git-commit-amend.png
