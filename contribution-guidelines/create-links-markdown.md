# Create links in markdown

在 markdown 文件中使用链接。

## Guidelines

| Link scenario | Guidance for the target link  |
|---------------|-----------|
|从本项目内的文档链接到本项目的另一篇文档。|使用最短相对路径。|
|从本项目内的文档链接到网络上的任意一篇文档。|使用绝对路径。|

### 使用友好的链接信息

使用友好的链接信息 - 最好使用原文章的标题或者能涵盖主旨的概述作为链接信息。 不要使用 “点击这里” 或者 "click here" 这类无法表明链接的目标文档的内容，也无法被搜索引擎解析的链接信息。

**推荐:**

- `更多信息，请参考 [Index of the contribution guidelines](./contribution-guidelines-index.md)。`

- `更多信息，请参考 [SET TRANSACTION ISOLATION LEVEL](https://msdn.microsoft.com/library/ms173763.aspx)。`

**避免:**

- `更多信息，请参考 [https://msdn.microsoft.com/library/ms173763.aspx](https://msdn.microsoft.com/library/ms173763.aspx)。`

- `更多信息，请参考 [这里](./contribution-guidelines-index.md)。`

### Markdown 中相对路径链接语法

使用以下语法创建本项目内部的链接。

子目录中的文档链接到根目录中的文档：

    [link text](../article-name.md)

根目录中的文档链接到子目录中的文档： 

    [link text](topic-directory/article-name.md)

主题目录中的文档链接到另一个主题目录中的文档：

    [link text](../topic-directory/article-name.md)

链接到同目录中的其他文档：

    [link text](article-name.md)


不需要为文档创建锚点 - 一般的网站在渲染 markdown 文件的时候，比如 GitHub，会自动为 H1、H2、H3 标题创建锚点，只要创建链接指向标题块即可：

    [link](#the-text-of-the-header-section-separated-by-hyphens)
    [Create cache](#create-cache)

链接到同目录中的其他文档内的锚点：

    [link text](./article-name.md#anchor-name)
    [Configure your profile](./media-services-create-account.md#configure-your-profile)

根目录中的文档链接到其他目录中的文档内的锚点：

    [link text](./topic-directory/article-name.md#anchor-name)
    [Configure your profile](./topic-directory/media-services-create-account.md#configure-your-profile)

## Reference-style links

可以使用引用形式的链接语法，可以使文档的源文件保持更好的可读性。可以将链接整齐地放置在文档源文件的底部，这些链接会按照序号替换文档中内联的链接。比如：

内联的文档：

    I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].

文档底部的引用链接：

    <!--Reference links in article-->
    [1]: http://google.com/
    [2]: http://search.yahoo.com/  
    [3]: http://search.msn.com/

## 短链和跳转链接

不要使用短链或者其他形式的跳转链接。

## More resources

- [Overview article](./../README.md)
- [Index of the contribution guidelines](./contribution-guidelines-index.md)
