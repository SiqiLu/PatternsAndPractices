# Markdown template (Heading 1 H1): 文档的标题

可以通过复制本地项目中该文件的方式使用此模板。或者可以点击 Raw 按钮查看模板的源文件，然后复制markdown文本使用此模板。

  ![Alt text; 请填写图片的描述信息。][1]

概要段落。可以在这里概述文档的主要内容。

## Heading 2 (H2)

每一段的前后需要保留一个空行，并且段落使用左对齐。在段落中注意使用准确的标点符号。在中文内容的前后需要使用全角标点符号，在英文前后需要使用半角标点符号。在中英文混合的句子中，尽量使用全角的标点符合。代码片段除注释外应该使用半角标点符号，特别是代码片段中的小括号、中括号和大括号。

可以在文档中使用绝对路径链接网络上的任意地址，但是并且使用清晰和准确的链接描述信息。[外部链接的描述信息。](https://github.com/MoeStack)。使用相对路径引用同一项目内的文档，当然也必须使用清晰的链接描述信息。[内部链接的描述信息](../contribution-guidelines/contribution-guidelines-index.md).

还可以使用应用形式的链接，比如：我经常使用 [Google] [gog] ，使用次数远超过使用 [Yahoo] [yah] 或者 [MSN] [msn] 的次数。

> **Note:**

> 提示内容。使用 markdown 的 note 语法将文档中的提示内容以缩进的区域块展示。并且使用加粗的字体表示此区域块的类型。

> **Warning:**

> 提示内容。使用 markdown 的 note 语法将文档中的提示内容以缩进的区域块展示。并且使用加粗的字体表示此区域块的类型。

## Heading (H2)

在文档中可以使用有序列表。

1. 第一项，C#代码片段

```csharp

public int BinarySearch(int index, int count, T item, IComparer<T> comparer)
{
    if (index < 0)
        throw new ArgumentOutOfRangeException("index", index, SR.ArgumentOutOfRange_NeedNonNegNum);
    if (count < 0)
        throw new ArgumentOutOfRangeException("count", count, SR.ArgumentOutOfRange_NeedNonNegNum);
    if (_size - index < count)
        throw new ArgumentException(SR.Argument_InvalidOffLen);
    Contract.Ensures(Contract.Result<int>() <= index + count);
    Contract.EndContractBlock();

    return Array.BinarySearch<T>(_items, index, count, item, comparer);
}
 
```

2. 第二项；

3. 第三项。

也可以使用无序列表。

- 文档中的代码如非特别说明，均使用C#编写。

- 文档中的脚本如非特别说明，均是在powershell环境中编写。并且powershell环境中安装了最新版本的nodejs、git、Azure PowerShell。

- 统一使用 “推荐” 或者 "Do" 表示推荐使用的模式和实践。

- 统一使用 “避免” 或者 "Don't" 表示要求避免使用做法。

##More resources 

文档的最后可以把相关联的文档和参考的文档的链接以无序列表的形式列在底部的 More resources区域。

<!--Image references-->
[1]: ./media/markdown-template-for-new-articles/copytemplate.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[gog]: http://google.com/        
[yah]: http://search.yahoo.com/  
[msn]: http://search.msn.com/    
