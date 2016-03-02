#Git clone

`git clone` 命令会创建一个已经存在的项目的副本，这有点类似 SVN 中的 `checkout` 命令。创建出的项目的副本不仅仅已经复制了原项目的所有内容，而且还可以拥有自己的版本历史和文件快照，使用 `git clone` 创建出的项目副本同时也是一个功能完备的、与原项目库隔离的 Git 项目。

`git clone` 会自动将原项目代码库的链接加进本地工作副本的 [`git remote`][4] 列表中，并且会使用 origin 命名该链接，这样可以很方便地与中央代码库进行交互。

##Usage

从地址为 `<original repository>` 的代码库在本地创建一个本地工作副本。原项目的地址可以是本地的文件路径、或者远程的HTTP协议链接、也可以是远程的SSH协议链接。推荐使用SSH协议和HTTPS协议。

```bash
    git clone <original repository>
```

从地址为 `<original repository>` 的代码库在本地创建一个本地工作副本，并且设置该副本在本地的目录名为 `<directory>` 。

```bash
    git clone <original repository> <directory>
```

##Discussion

当已经在服务器上创建了中央代码库后，使用 `git clone` 创建本地工作副本是最常用的方法。类似 `git init` ， `git clone` 通常是一次性操作，一旦创建了本地工作副本，在本地上的所有的代码版本控制操作和团队协作都都通过这个本地副本进行。

##More resources

- [Git overview article][1]
- [Git tutorials: Setting up a repository][2]
- [Git config][3]
- [Git remote][4]
- [Git init][5]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-clone
[3]: ./git-command-git-config.md
[4]: ./git-command-git-remote.md
[5]: ./git-command-git-init.md