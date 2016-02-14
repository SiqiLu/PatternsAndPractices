# PatternsAndPractices
构建应用的通用模式和最佳实践。

## Repository organization

项目包含3个根目录：

### \articles

*\articles* 目录保存markdown格式的文档，所有的文档都以.md作为后缀名，文档均以UTF-8编码保存。

* **Article filenames:** 文档名称均尽量使用英文命名，文档名称中不能使用空格、换行符。

* **Media subfolders:** *\articles* 目录中包含了一个名为 *\media* 的子目录。该子目录中存放所有 *\articles* 根目录中的文档所引用的媒体文件（图片、PDF文档、音频、视频等）。*\articles* 中会把主题相关联的文档存放在主题子目录中，每一个主题目录都分别包含一个独立的 *\media* 目录，用于存放该主题内的文档所引用的媒体文件。 每个文档的媒体文件目录和该文档同名，即文档名去除.md后缀即为媒体文件目录名。

### \markdown-templates

目录中存放文档的markdown模板。

### \contribution-guidelines

目录中存放本项目的contribution-guidelines指南。在向该项目提交pull request之前，需要先阅读该目录中的所有内容，并且确保提交的内容均符合该目录中guidelines的要求。 

## Markdown resources

文档编写使用 GitHub flavored markdown. 以下是可以使用的一些资源和工具.

- [Markdown basics][1]

- [Printable markdown cheatsheet][2]

- [Emoji cheatsheet][3]

- [Markdown editor: Visual Studio Code][4]

- [Markdown editor: Atom][5]

- [Markdown editor: Visual Studio Code][6]

- [Markdown editor online: Stack Edit][7]

## More resources

- [Index of the contribution guidelines](./contribution-guidelines/contribution-guidelines-index.md)

<!--links-->
[1]: https://help.github.com/articles/getting-started-with-writing-and-formatting-on-github/
[2]: ./contribution-guidelines/media/documents/markdown-cheatsheet.pdf?raw=true
[3]: http://www.emoji-cheat-sheet.com/
[4]: https://www.visualstudio.com/products/code-vs
[5]: https://atom.io/
[6]: https://www.visualstudio.com/products/code-vs
[7]: https://stackedit.io/ 