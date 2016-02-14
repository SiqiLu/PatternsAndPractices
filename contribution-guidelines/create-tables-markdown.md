#Create tables in markdown
在markdown文件中使用表格。

在markdown中使用表示最简单的方法是使用竖线和短横线。

 ![Markdown中的表格语法。][1]

可以使用半角冒号:控制行内容的对齐格式：

    |-----:| - 右对齐
    |:-----| -  左对齐
    |:-----:| - 居中

如果使用HTML格式的表格，并且2个表格之间的markdown不能正常显示。则需要在 `</table>` 标签后添加 `<br/>` 标签。

![Markdown中使用TABLE标签][2]

有关更多的在markdown中使用表格的信息，请参考：
- Markdown tables generator: http://www.tablesgenerator.com/markdown_tables
- https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#wiki-tables
- http://michelf.ca/projects/php-markdown/extra/#table

##More resources

- [Overview article](./../README.md)
- [Index of the contribution guidelines](./contribution-guidelines-index.md)

<!--image references-->
[1]: ./media/create-tables-markdown/table-markdown.png
[2]: ./media/create-tables-markdown/break-tables.png