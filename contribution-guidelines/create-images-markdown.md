# Create images in markdown

在markdown文件中使用图片。

## 图片目录与链接语法

对于一篇新的文档，需要先创建新的媒体目录，用于保存文档中所使用的媒体文件。目录的地址格式如下所示：

    /articles/<topic-directory>/media/<article-name>/

例如:

    /articles/git/media/git-workflow/

在建立媒体目录之后，可以将所要使用的图片保存在该目录中，并且使用如下的语法在文档中引用图片：

```
![Alt image text](./media/article-name/your-image-filename.png)
```

例如:

在[the markdown template](../markdown-templates/markdown-template-for-new-articles.md)文档的头部 有图片的引用实例.

## Guidelines

当描述操作步骤的时候，如果不能使用脚本或者代码重现想要表达的步骤，则需要在文档中保留所有的步骤截图。并且一定要使用文字将步骤描述清晰，当避免图片无法加载的时候，文档的阅读者依旧可以了解文档所要描述的内容。

使用媒体文件时，请考虑以下原则:
- 不要直接引用别的文档所引用的媒体文件。而是应该把需要的文件复制一份，并且保存到该文档对应的媒体目录中。直接引用其它文档中的媒体文件，很可能在该文件被删除之后，永久丢失媒体文件。

- 推荐使用 .png 格式的图片作为图片媒体文件。

- 推荐使用 .pdf 格式的文档作为文档媒体文件。

- 使用 5 px 宽的红色方框来表示提示。在画图板中默认的红色方框即为 5 px。  

    例如:
    
    ![插图中使用的红色方框。](./media/create-images-markdown/gs13noauth.png)

- 避免截图的边缘有无意义的空白区域。如果你截图的背景是白色，而且无法避免白色的空白区域，则需要使用一个像素的浅灰色边框明确划分出图片的边框。可以使用画图板中的浅灰色 (0xC3C3C3)作为边框的颜色。需要使用其他的画图工具，控制浅灰色的颜色 RGB 值为 R195, G195, B195。使用Visio可以很容易为截图添加符合要求的边框，选中图片，选择“线条”(Line),设定线条(Line)的颜色, 最后更改线条(Line)的宽度为 1/2 pt。截图的浅灰色边框可以帮助读者很容易区分截图的白色区域与网页的白色背景。

    例如:

    ![白色截图和浅灰色边框的实例。](./media/create-images-markdown/agent.png)

- 白色背景的思维导图、拓扑图、架构图等概念图不需要加浅灰色边框。  
    
    例如:

    ![不加边框的白色背景概念图实例。](./media/create-images-markdown/ic727360.png)

- 需要控制图片的宽度。过宽的图片在网页浏览时会被自动缩放。但是自动缩放会导致图片失真模糊。图片的宽度最大应该控制在 780 px 之内（包含边框的宽度），宽度大于该值的图片需要在使用前手动缩放到　780 px 之内。

- 保留命令执行后的截图。 如果文档描述的是用户使用shell的步骤，需要将命令执行后的输出结果通过截图的形式呈现。截图依旧需要控制宽度在 780 px 以内。在截图前，需要调整窗口的大小，确保只有相关的输出内容出现在截取的图片中 (可以前后适当保留一部分空行)。

- 截图尽量保留完整的窗口。当对浏览器窗口进行截图时, 调整浏览器窗口的大小，控制宽度在 780 px 以内，并且尽量缩小窗口的高度到能展示应用的内容即可。

    例如:

    ![浏览器窗口截图实例。](./media/create-images-markdown/helloworldlocal.png)

- 留意截图中的信息。不要透漏内部重要信息或者任何个人信息。

- 概念图中尽量使用官方图标。微软相关技术产品的官方图标可以在 http://aka.ms/CnESymbols 下载。

##More resources

- [Overview article](./../README.md)
- [Index of the contribution guidelines](./contribution-guidelines-index.md)
