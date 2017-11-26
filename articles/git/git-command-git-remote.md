# Git remote

使用 ```git remote``` 命令可以创建，查看和删除到其他存储库的连接。远程连接更像书签，而不是直接链接到其他存储库。它们不是提供对另一个存储库的实时访问，而是用作方便的名称，可以用来引用不太方便的 URL。

例如，下图显示了从本地仓库到中央仓库和另一个开发人员仓库的两个远程连接。开发人员可以使用类似 ```origin``` 这样的别名和其它命令一起使用用来进行对其他存储库的操作，从而免去了使用完成的 URL 的麻烦。

![```git remote``` 示意图][m1]

## Usage

列出所有其他存储库的远程连接。

``` bash
    git remote
```

列出所有其他存储库的远程连接和每一个连接的完整 URL。

``` bash
    git remote -v
```

创建到远程存储库的新连接。添加远程连接后，您可以在其他 Git 命令中使用 ```<name>``` 作为 ```<url>``` 的便捷快捷方式。

``` bash
    git remote add <name> <url>
```

移除 ```<name>``` 表示的远程存储库连接。

``` bash
    git remote rm <name>
```

将一个远程连接从 ```<old-name>``` 重命名为 ```<new-name>```。

``` bash
    git remote rename <old-name> <new-name>
```

当然，除了让当前分支的版本历史回滚之外，也可以选择不仅仅清空暂存区，也丢弃工作区中所有文件在 ```<commit>``` 之后的变更。这样操作就像是让 ```<commit>``` 之后的所有变更都没有发生过一样。而且该次回滚很可能无法挽回。

## Discussion

Git 旨在为每个开发人员提供一个完全隔离的开发环境。 这意味着信息不会自动在存储库之间来回传递。相反，开发人员需要手动将上游提交拉入本地存储库，或手动将其本地提交重新提交到中央存储库。```git remote``` 命令实际上只是将 URL 传递给这些“共享”命令的一种更简单的方法。

### The origin Remote

当你使用 git 克隆一个仓库时，它会自动创建一个名为 ```origin``` 的远程连接，指向克隆的仓库。这对开发人员创建中央存储库的本地副本很有用，因为它提供了一种简单的方法来提取上游更改或发布本地提交。这也是导致大多数基于 Git 的项目将其中央存储库称为 ```orgin``` 的原因。

### Repository URLs

Git 支持很多方法来引用远程存储库。访问远程存储库的两种最简单的方法是通过HTTP和SSH协议。HTTP是一种允许对存储库进行匿名只读访问的简单方法。例如：

``` plain
http://host/path/to/repo.git
```

但是，通常不可能将提交推送到一个HTTP地址。对于读写访问，您应该使用SSH来代替：

``` plain
ssh://user@host/path/to/repo.git
```

您需要在主机上使用有效的SSH帐户，Git 原生支持通过SSH验证访问。

## Example

除了使用 ```origin``` 之外，与队友存储库连接通常也非常方便。例如，如果您的同事John在dev.example.com/john.git上维护了可公开访问的存储库，则可以按如下方式添加连接：

``` bash
git remote add john http://dev.example.com/john.git
```

拥有对各个开发人员存储库的这种访问权限，可以在中央存储库之外进行协作。这对于从事大型项目的小团队来说非常有用。

## More resources

- [Git overview article][1]
- [Git tutorials: Collaborating Syncing][2]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/syncing#git-remote

<!-- Images -->
[m1]: ./media/git-command-git-remote/git-command-git-remote.png
