# gitignore

Git 将工作区中的每一个文件都归为一下三个类别的文件之一：

1. tracked - 已经添加到暂存区或者已经提交的文件；

1. untracked - 没有被添加到暂存区并且也没有被提交过的文件；

1. ignored - 指定被 Git 系统忽略的文件。

一般编译的临时文件或者结果文件、机器生成的文件都应该被排除到 Git 的仓库之外，即应该被显式设置为忽略文件。比如：

- 依赖包的本地缓存文件。如：/packages 或者 /node_modules

- 编译的结果文件。如：/*.min.js, .o, 或者 .pyc

- 编译的输出文件夹。如：/bin, /out, 或者 /target

- 运行时生成的文件。如：.log, .lock, 或者 .tmp

- 系统的隐藏文件。如：.DS_Store 或者 Thumbs.db

- 个人的 IDE 配置文件。如：.idea/workspace.xml 或者 .vs/*

需要被显示忽略的文件，会被登记在 ```.gitignore``` 文件中。该文件应该在 Git 仓库的根目录下。Git 系统中并没有特定的 ```git ignore``` 命令。只能通过更新 ```.gitignore``` 文件的方式忽略新的需要被忽略的文件。```.gitignore``` 可以使用模式匹配来判断某一个文件是否需要被忽略。

## Git ignore patterns

```.gitignore``` 使用 [```globbing patterns```][4] 对文件名进行模式匹配。

<!-- markdownlint-disable MD033 -->
|Pattern|Example matches|Explanation|
| :--- | :--- | :--- |
|**/logs|logs/debug.log <br/> logs/monday/foo.bar <br/> build/logs/debug.log|可以用前置双星号匹配存储库中任何位置的目录。|
|**/logs/debug.log|logs/debug.log <br/> logs/monday/foo.bar <br/> **but not** logs/build/debug.log|可以用前置双星号模式限制忽略文件的父文件夹名称。|
|*.log|debug.log <br/> foo.log <br/> .log <br/> logs/debug.log|星号是匹配零个或多个字符的通配符。|
|*.log <br/> !important.log|debug.log <br/> trace.log <br/> **but not** important.log <br/> **but not** logs/important.log|对模式前置加上感叹号可以否定它。如果一个文件匹配一个模式，但也匹配文件后面定义的否定模式，它将不会被忽略。|
|*.log <br/> !important.log <br/> trace.*|debug.log <br/> important/trace.log <br/> **but not** important/debug.log|在否定模式之后定义的模式将重新忽略之前被否定的文件。|
|/debug.log|debug.log <br/> **but not** logs/debug.log|只在存储库根目录中预先加入斜杠匹配文件。|
|debug.log|debug.log <br/> logs/debug.log|默认情况下，模式匹配任何目录中的文件。|
|debug?.log|debug0.log <br/> debugg.log <br/> **but not** debug10.log|问号完全匹配且只匹配一个字符。|
|debug[0-9].log|debug0.log <br/> debug1.log <br/> **but not** debug10.log|方括号也可用于匹配指定范围内的单个字符。|
|debug[01].log|debug0.log <br/> debug1.log <br/> **but not** debug2.log <br/> **but not** debug01.log|方括号匹配指定集合中的单个字符。|
|debug[!01].log|debug2.log <br/> **but not** debug0.log <br/> **but not** debug1.log <br/> **but not** debug01.log|感叹号可以用来匹配除了指定集之外的任何字符。|
|debug[a-z].log|debuga.log <br/> debugb.log <br/> **but not** debug01.log|范围可以是数字或字母。|
|logs|logs <br/> logs/debug.log <br/> logs/latest/foo.bar <br/> build/logs <br/> build/logs/debug.log|如果不附加斜线，则该模式将匹配文件以及具有该名称的目录。在左侧的示例匹配中，将忽略名为日志的目录和文件。|
|/logs|logs/debug.log <br/> logs/latest/foo.bar <br/> build/logs/foo.bar <br/> build/logs/latest/debug.log|附加一个斜线表示该模式是一个目录。存储库中与该名称相匹配的任何目录（包括其所有文件和子目录）的全部内容将被忽略。|
|/logs <br/> !logs/important.log|logs/debug.log <br/> logs/important.log|由于Git中一个与性能相关的怪癖，你不能否定由于模式匹配目录而被忽略的文件。|
|logs/**/debug.log|logs/debug.log <br/> logs/monday/debug.log <br/> logs/monday/pm/debug.log|双星号匹配零个或多个目录。|
|logs/*day/debug.log|logs/monday/debug.log <br/> logs/tuesday/debug.log <br/> **but not** logs/latest/debug.log|通配符也可以在目录名称中使用。|
|logs/debug.log|logs/debug.log <br/> build/logs/debug.log <br/> **but not** debug.log|指定特定目录中的文件的模式与存储库根目录相关。（如果你愿意的话，你可以前置添加一个斜线，但是它并不会造成任何影响。）|
<!-- markdownlint-enable MD033 -->

除了这些之外，还可以使用＃将注释包含在.gitignore文件中：

<!-- markdownlint-disable MD031 -->
``` plain
    # ignore all logs
    *.log
```
<!-- markdownlint-enable MD031 -->

可以使用\来转义.gitignore模式字符：

<!-- markdownlint-disable MD031 -->
``` plain
    # ignore the file literally named foo[01].txt
    foo\[01\].txt
```
<!-- markdownlint-enable MD031 -->

## Shared .gitignore files in your repository

Git 忽略规则通常在仓库根目录下的 ```.gitignore``` 文件中定义。但是，也可以选择在存储库的不同目录中定义多个 ```.gitignore``` 文件。特定 ```.gitignore``` 文件中的每个模式都是相对于包含该文件的目录进行测试的。然而，约定和最简单的方法是在根中定义一个 ```.gitignore``` 文件。当您的 ```.gitignore``` 文件被签入时，它就像版本库中的任何其他文件一样版本化，并在推送时与您的队友共享。通常情况下，您应该只在 ```.gitignore``` 中包含可以使存储库的其他用户受益的模式。

## Personal Git ignore rules

您还可以在 .git/info/exclude 的指定文件中为特定存储库定义个人私有的忽略模式。这些文件不会被 Git 管理，并且不会与您的存储库一起分发，因此这是一个适当的地方，可以包含个人私有的模式。例如，如果您有自定义的日志记录设置，或者在存储库的工作目录中生成文件的特殊开发工具，则可以考虑将它们添加到 .git/info/exclude 中，以防止它们意外被添加到存储库中。

## Global Git ignore rules

另外，可以通过设置 Git 的 core.excludesFile 属性来为本地系统上的所有存储库定义全局的 Git 忽略模式。你必须自己创建这个配置文件，如果您不确定将全局 ```.gitignore``` 文件放在哪里，那么您的主目录将是一个不错的选择（并且以后可以很容易找到）。一旦你创建了这个文件，你需要用 [```git config```][5] 来配置它的位置：

<!-- markdownlint-disable MD031 -->
``` bash
    touch ~/.gitignore
    git config --global core.excludesFile ~/.gitignore
```
<!-- markdownlint-enable MD031 -->

您应该谨慎选择全局忽略的模式，因为不同的文件类型与不同的项目相关。 特殊的操作系统文件（例如.DS_Store和thumbs.db）或由某些开发人员工具创建的临时文件是全局忽略的典型候选文件。

## Ignoring a previously committed file

如果您想忽略过去提交的文件，则需要从存储库中删除该文件，然后为其添加一个```.gitignore``` 规则。 在 ```git rm``` 中使用 ```--cached``` 选项意味着文件将从你的版本库中被删除，但是将作为一个被忽略的文件保留在你的工作目录中。

<!-- markdownlint-disable MD031 -->
``` bash
    $ echo debug.log >> .gitignore

    $ git rm --cached debug.log
    rm 'debug.log'

    $ git commit -m "Start ignoring debug.log"
```
<!-- markdownlint-enable MD031 -->

如果要从存储库和本地文件系统中删除文件，可以省略 ```--cached``` 选项。

## Committing an ignored file

可以使用 [```git add -f```][6]（或 ```--force``` ）选项强制忽略的文件提交到存储库：

<!-- markdownlint-disable MD031 -->
``` bash
    $ cat .gitignore
    *.log

    $ git add -f debug.log

    $ git commit -m "Force adding debug.log"
```
<!-- markdownlint-enable MD031 -->

当这个时候往往是因为有一个一般的模式（如* .log）定义，但你想提交一个特定的文件。然而，更好的解决方案是定义一个通用规则的例外：

<!-- markdownlint-disable MD031 -->
``` bash
    $ echo !debug.log >> .gitignore

    $ cat .gitignore
    *.log
    !debug.log

    $ git add debug.log

    $ git commit -m "Adding debug.log"
```
<!-- markdownlint-enable MD031 -->

这种方法更加明显，而且不那么令人困惑。

## Debugging .gitignore files

如果你有复杂的 ```.gitignore``` 模式，或者模式分布在多个 ```.gitignore``` 文件中，那么可能很难追查为什么某个文件被忽略。 您可以使用 ```-v```（或 ```--verbose```）选项的 ```git check-ignore``` 命令来确定哪个模式导致特定的文件被忽略：

<!-- markdownlint-disable MD031 -->
``` bash
    $ git check-ignore -v debug.log
    .gitignore:3:*.log debug.log
```
<!-- markdownlint-enable MD031 -->

输出：

<!-- markdownlint-disable MD031 -->
``` bash
    <file containing the pattern> : <line number of the pattern> : <pattern> <file name>
```
<!-- markdownlint-enable MD031 -->

你可以传递多个文件名到 ```git check-ignore``` 命令中，并且这些名字本身甚至不需要和存储库中存在的文件相对应。

## More resources

- [Git overview article][1]
- [Git tutorials: gitignore][2]
- [GitHub: gitignore][3]
- [globbing patterns][4]
- [Git config][5]
- [Git add][6]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/gitignore
[3]: https://github.com/github/gitignore
[4]: https://linux.die.net/man/7/glob
[5]: ./git-command-git-config.md
[6]: ./git-command-git-add.md
