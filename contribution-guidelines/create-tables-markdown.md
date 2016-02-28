#Create tables in markdown

在 markdown 文件中使用表格。

在 markdown 中使用表格最简单的方法是使用竖线和短横线。

 ![Markdown 中的表格语法。][1]

可以使用半角冒号:控制行内容的对齐格式：

    |-----:| - 右对齐
    |:-----| -  左对齐
    |:-----:| - 居中

如果使用 HTML 格式的表格，并且2个表格之间的 markdown 不能正常显示。则需要在 `</table>` 标签后添加 `<br/>` 标签。

![Markdown 中使用 TABLE 标签][2]

有关更多的在markdown中使用表格的信息，请参考：
- [Markdown tables generator][1] 
- [GitHub wiki: Markdown-Cheatsheet#wiki-tables][2]

##More resources

- [Overview article](./../README.md)
- [Index of the contribution guidelines](./contribution-guidelines-index.md)

<!-- Links -->
[1]: http://www.tablesgenerator.com/markdown_tables
[2]: https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#wiki-tables

<!-- Images -->
[1]: ./media/create-tables-markdown/table-markdown.png
[2]: ./media/create-tables-markdown/break-tables.png