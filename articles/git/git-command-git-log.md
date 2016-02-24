#Git log

![```git log``` 示意图][m1]

```git log``` 命令可以输出某一次提交的信息。可以使用该命令查看项目的版本历史纪录，还可以搜索需要的变更。[```git status```][4] 会输出当前的工作区和暂存区状态，而不涉及版本历史纪录；相反，```git log``` 则只会处理已经提交的记录。

日志输出可以以多种方式进行定制，从简单的过滤器到在完全用户定义的格式都能输出。一些常见的 ```git log``` 输出格式的配置介绍如下：

##Usage

一般默认的输出格式为：

```
commit 3157ee3718e180a9476bf2e5cab8e3f1e78a73b7
Author: John Smith
```

使用默认的格式输出全部的历史纪录。如果输出超过一屏，可以使用空格键加载更多的历史，使用 ```q``` 键退出：

```bash
    git log
```

使用默认的格式输出特定数量的历史记录。比如， ```git log -n``` 只会输出3条记录。

```bash
    git log -n <limit>
```

将每次提交的信息概要成一行输出。这种方式在获取项目的历史纪录概要时非常有用。

```bash
    git log --oneline
```

上一行命令的输出示意如下：
```
0e25143 Merge branch 'feature'
ad8621a Fix a bug in the feature
16b36c6 Add a new feature
23ad9ad Add the initial code base
```

不仅输出简单的提交信息，还输出在该次提交中有哪些文件被改变和改变的行数。

```bash
    git log --stat
```

上一行命令的输出示意如下：
```
commit f2a238924e89ca1d4947662928218a06d39068c3
Author: John <john@example.com>
Date:   Fri Jun 25 17:30:28 2014 -0500

    Add a new feature

 hello.py | 105 ++++++++++++++++++++++++-----------------
 1 file changed, 67 insertion(+), 38 deletions(-)
```

输出每次提交的详细信息，这种格式化方式能输出最详细的项目提交记录。

```bash
    git log -p
```

上一行命令的输出示意如下：
```
commit 16b36c697eb2d24302f89aa22d9170dfe609855b
Author: Mary <mary@example.com>
Date:   Fri Jun 25 17:31:57 2014 -0500

    Fix a bug in the feature

diff --git a/hello.py b/hello.py
index 18ca709..c673b40 100644
--- a/hello.py
+++ b/hello.py
@@ -13,14 +13,14 @@ B
-print("Hello, World!")
+print("Hello, Git!")
```

搜索特定用户的提交。参数 ```<pattern>``` 可以是平文本也可以是正则表达式。

```bash
    git log --author="<pattern>"
```

搜索提交信息符合匹配的提交。参数 ```<pattern>``` 可以是平文本也可以是正则表达式。

```bash
    git log --grep="<pattern>"
```

只输出范围内的提交。从 ```<since>``` 到 ```<until>```，这2个参数可以是 ```commit ID```，也可以是分支名，```HEAD```，或者其他能被 Git 解析成 ```commit ID``` 的 Git 引用。

```bash
    git log <since>..<until>
```

只输出特定文件相关的提交。这是查看某个文件历史纪录最方面的方式。

```bash
    git log <file>
```

还有一些其它的参数可以使用。```--graph``` 操作符会在提交信息左方绘制文本格式的提交图。```--decorate``` 会在原有的输出内容上添加分支名、```tag``` 名称。

```bash
    git log --graph --decorate --oneline
```

上一行命令的输出示意如下：
```
*   0e25143 (HEAD, master) Merge branch 'feature'
|\  
| * 16b36c6 Fix a bug in the new feature
| * 23ad9ad Start a new feature
* | ad8621a Fix a critical security issue
|/  
* 400e4b7 Fix typos in the documentation
* 160e224 Add the initial code base
```

```bash
   git log --decorate --oneline
```

上一行命令的输出示意如下：
```
0e25143 Merge branch 'feature'
ad8621a Fix a bug in the feature
16b36c6 Add a new feature
23ad9ad Add the initial code base
```

还可以自定义输出的格式，语法如下：

```bash
    git log --pretty=format:"%cn committed %h on %cd"
```

其中，%cn, %h 和 %cd 符号分别表示提交者姓名，提交的摘要值和提交的时间。

上面的命令的输出示意如下：
```
John committed 400e4b7 on Fri Jun 24 12:30:04 2014 -0500
John committed 89ab2cf on Thu Jun 23 17:09:42 2014 -0500
Mary committed 180e223 on Wed Jun 22 17:21:19 2014 -0500
John committed f12ca28 on Wed Jun 22 13:50:31 2014 -0500
```

##Discussion

```git log``` 是查看 Git 版本历史纪录的基本命令。当需要查找一个特定版本的提交或者查看一些操作产生的提交时，可以使用此命令。

```
commit 3157ee3718e180a9476bf2e5cab8e3f1e78a73b7
Author: John Smith
```

输出的信息内容都很容易理解，如上图，第一条内容是一个40个字符的 SHA-1 摘要值。这个摘要值主要有2方面用途，第一可以使用该摘要值验证提交的完整性，如果该提交后续被修改，则摘要值一定会改变；第二可以使用该摘要值唯一标识一个提交，即该值又被记为 ```commit ID```。

```commit ID``` 可以在类似 ```git log <since>..<until>``` 的命令中使用。比如，```git log 3157e..5ab91``` 会输出ID 在3157e 和5ab91之间的所有提交的信息。除了使用摘要值之外，分支名、关键字 ```HEAD``` 都可以用作提交的引用。 ```HEAD``` 一般引用当前的最后一次提交。

```~``` 波浪线可以作为相对提交的应用。比如
，3157e~1 引用3157e提交的上一次提交，```HEAD~2``` 引用当前最后一次提交之前的第二次提交，也称为当前最后一次提交的祖父提交（父提交的父提交）。

这些提交的唯一标识方法，主要是用于哪些需要指定唯一一个提交的命令，```git log``` 就是其中的一个。

##Example

在 *Usage* 一节中展示了很多 ```git log``` 的用法。其中的参数可以组合使用：

```bash
git log --author="John Smith" -p hello.cs
```

以上命令将输出关于 hello.cs 文件的由 John Smith 做出的所有提交的详细信息。

```..``` 语法在表示一个范围时非常有效。还可以表示一些特殊的范围，比如使用以下语法的命令就是输出在 *some-feature* 分支中但是不在 *master* 分支中的所有提交的简要信息。

```bash
git log --oneline master..some-feature
```

##More resources

- [Git overview article][1]
- [Git tutorials: Inspecting a repository][2]
- [Git tutorials: Advanced Git log][3]
- [Git status][4]
- [Git checkout][5]

<!-- Links -->
[1]: ./git-articles-overview.md
[2]: https://www.atlassian.com/git/tutorials/inspecting-a-repository/git-log
[3]: https://www.atlassian.com/git/tutorials/git-log
[4]: ./git-command-git-status.md
[5]: ./git-command-git-checkout.md

<!-- Images -->
[m1]: ./media/git-command-git-log/git-log.png