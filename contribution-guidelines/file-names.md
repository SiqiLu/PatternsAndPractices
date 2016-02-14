#File names

本项目作为一个文档项目, 将所有的文档保存在单个目录中 (**articles**)。

以下是文档命名时需要关注的内容:

+ [Rules]
+ [Pattern]
+ [Standard examples]
+ [Special file naming convention for the Azure preview portal]
+ [Marketplace content]
+ [File name approval]

##Rules

- 文档使用英文命名。
- 文档名中不能包含空格和特殊字符。
- 使用英文小写字母。
- 名称不要超过80个字母。
- 动词使用一般现在时态，如 develop, buy, build, troubleshoot。不要额外使用ing后缀。
- 避免使用短小的单词 - 不要使用 a, and, the, in, or 等。
- 所有的文件必须使用markdown格式，并且使用 .md 作为文件后缀名。

##Pattern

一般命名模式：

 **topic-tech-content-version.md**

依据上述的命名模式并且参考本项目中的其他文档进行命名。文档名称中应该以该文档涉及的技术领域、框架名称或者开发平台开头。

##Standard examples

以下是推荐的文档命名：

- git-commands-use-rebase-clean-feature-repository.md
- cloud-services-dotnet-continuous-delivery.md
- mobile-services-ios-get-started.md
- documentdb-manage-account.md
- mobile-services-dotnet-backend-get-started-settings-sync.md
- active-directory-java-authenticate-users-access-control-eclipse.md
- virtual-machines-install-windows-server-2008r2.md

##File name approval

It's the job of our group of pull request reviewers to review file names when a new file is submitted to the repository for the first time. Pull request reviewers should review the file name and provide feedback via the pull request comment stream if changes are needed. The file name needs to be corrected before the pull request is accepted. Contributors can easily push the update to the pending pull request.

##More resources

- [Overview article](./../README.md)
- [Index of the contribution guidelines](./contribution-guidelines-index.md)


<!--Anchors-->
[Rules]: #rules
[Pattern]: #pattern
[Standard examples]: #standard-examples
