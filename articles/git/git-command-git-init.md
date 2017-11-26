# Git init

![```git init``` 示意图][m1]

```git init``` 命令用于创建一个新的 Git 仓库。不仅可以用于创建一个不包含任何文件的空项目，也可以将现有的、未版本控制的项目转换为 Git 项目。这通常是你将在一个新的项目中运行的第一个命令。

执行 ```git init``` 命令会在项目的根目录创建一个 ```.git``` 隐藏目录，它用于存放 git 管理项目所需的所有元数据。

## Usage

```git init```命令会将执行命令的当前目录转变为一个 git 项目。将在当前目录下添加一个 ```.git``` 隐藏目录，git 将可以开始对目录中的所有文件进行版本控制。

``` bash
    git init
```

当想要使用制定的目录创建 git 项目时，可以使用以下命令，执行该命名会创建一个新的目录，并且只包含 ```.git```隐藏目录。

``` bash
    git init <directory>
```

## Discussion

相比较于 SVN，使用 ```git init``` 命令即可创建一个版本控制的项目是非常简单的。Git 不会要求您创建一个存储库，导入文件，并签出工作区副本。而只需要进入项目目录并且执行 ```git init``` 命令即可。

对于大部分项目，```git init``` 通常只需要在项目创建的时候执行一次，而其他参与项目的开发人员不需要再本地再创建项目，而是使用 [```git clone```][3] 命令在本地创建副本。

## More resources

- [Git overview article][1]
- [Git tutorials: Setting up a repository][2]
- [Git clone][3]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-init
[3]: ./git-command-git-clone.md

<!-- Images -->
[m1]: ./media/git-command-git-init/git-init.png