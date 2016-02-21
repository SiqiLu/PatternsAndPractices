#Git config

可以通过 ```git config``` 命令配置 git 应用或者是 git 在某个代码库中的设置项。（或单个存储库）。此命令可以用于配置用户信息或者代码库的设置。一些常见配置如下。

##Usage

1.  设置提交变更时使用的用户名。如果想为当前用户设置提交时用户名的全局配置，可以在命令中使用 ```--global``` 参数。单个代码库中的配置会覆盖全局配置。

    ```bash
        git config user.name <name>
    ```

    ```bash
        git config --global user.name <name>
    ```

2.  设置用户提交变更时使用的电子邮箱地址，当然同样可以使用 ```--global``` 参数设置全局配置。

    ```bash
        git config user.email <email>
    ```
    
    ```bash
        git config --global user.email <email>
    ```
3.  为 ```git``` 命令创建 ```alias``` 。 同样可以使用 ```--global``` 参数创建全局命令别名。

    ```bash
        git config alias.<alias name> <git command>
    ```
    
    ```bash
        git config --global alias.<alias name> <git command>
    ```
4.  设置 ```git``` 命令中需要编辑文本时，使用的编辑器。```git command``` 命令就经常需要用户在编辑器中编辑提交的信息。```<editor>``` 应该是你需要配置的编辑器在命令行中开打的命令，比如 ```vi```。

    ```bash
        git config --system code.editor <editor>
    ```

5.  在文本编辑器中打开 ```git``` 的配置文件，可以使用 ```--global``` 参数打开全局配置文件，可以手动更改配置。

    ```bash
        git config --edit
    ```
    
    ```bash
        git config --global --edit
    ```

##Discussion

```Git``` 的所有配置选项都存储在平文本文件中，使用 ```git config``` 命令可以很容易地修改这些配置项。通常情况下，你只需要在新的开发环境中设置一次，几乎所有情况下，都可以直接使用 ```--global``` 参数设置全局配置。

```Git``` 将这些配置项保存在三个独立的文件中，这三个配置文件的作用域不同，分别是代码库、用户、系统：

- ```<repository directory>/.git/config``` – 特定代码库的配置。

- ```~/.gitconfig``` – 当前用户的配置。 使用 ```--global``` 参数设置的配置项就保存在这个文件中。

- ```$(git installation)/etc/gitconfig(linux)```, ```$(git installation)/mingw64/etc/gitconfig(windows x64)``` - 系统级别的配置。

当三个配置文件中的配置项有冲突时，代码库级别的优先级大于用户级别的配置，用户级别的优先级大于系统级别的优先级。

如果你打开其中任意一个配置文件，你会看到类似下面的文本：

```
[user] 
name = John Smith
email = john@example.com
[alias]
st = status
co = checkout
br = branch
up = rebase
ci = commit
[core]
editor = vim
```

你可以手动修改任意配置项，并且保存配置文件，同样可以达到设置配置的效果。

##Example

当在新的开发环境中安装 ```git``` 之后，首先要进行配置的是用户名和用户电子邮箱，之后再自定义一些配置项。一个常用的初始化配置命名会和以下命令非常相似：

```bash
# Tell Git who you are
git config --global user.name "John Smith"
git config --global user.email john@example.com
# Select your favorite text editor
git config --global core.editor vim
# Add some SVN-like aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.up rebase
git config --global alias.ci commit
```

这些命令设置的配置项都会被记录在上一节的用户级别配置文件中 ```~/.gitconfig```。

##More resources

- [Git overview article][1]
- [Git tutorials: Setting up a repository][2]
- [Git add][3]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/setting-up-a-repository/git-init
[3]: ./git-command-git-add.md