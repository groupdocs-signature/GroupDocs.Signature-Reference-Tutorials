---
"description": "通过我们全面的分步指南和代码示例，了解如何使用 GroupDocs.Signature for .NET 高效地搜索文档中的文本签名。"
"linktitle": "搜索文本签名"
"second_title": "GroupDocs.签名 .NET API"
"title": "在文档中搜索文本签名"
"url": "/zh/net/signature-searching/search-for-text-signatures/"
"weight": 16
type: docs
---
## 介绍

文本签名是指示文档作者身份、批准或验证的常用方法。在数字文档管理中，以编程方式搜索和提取文本签名的能力对于文档验证、工作流自动化和合规性验证至关重要。GroupDocs.Signature for .NET 提供了一个全面的解决方案，用于在 .NET 应用程序中实现文本签名搜索功能，支持各种文档格式和高级搜索功能。

本教程将指导您使用 GroupDocs.Signature for .NET 在文档中搜索文本签名的过程，提供详细的解释、分步说明和实用的代码示例。

## 先决条件

在深入文本签名搜索之前，请确保您满足以下先决条件：

1. GroupDocs.Signature for .NET 库：从 [发布页面](https://releases。groupdocs.com/signature/net/).

2. 开发环境：设置合适的开发环境，例如 Visual Studio 或任何支持 .NET 的兼容 IDE。

3. 样本文档：准备包含文本签名的测试文档，以供验证和测试。

4. 基本 C# 知识：熟悉 C# 编程语言和 .NET 框架概念。

## 导入命名空间

首先导入访问 GroupDocs.Signature 功能所需的命名空间：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

现在，让我们将搜索文本签名的过程分解为清晰、易于管理的步骤：

## 步骤 1：加载文档

首先，定义文档路径并初始化 `Signature` 目的：

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

using (Signature signature = new Signature(filePath))
{
    // 文本签名搜索代码将在此处添加
}
```

## 第 2 步：配置搜索选项

创建和配置 `TextSearchOptions` 指定如何搜索文本签名：

```csharp
// 配置文本搜索选项
TextSearchOptions options = new TextSearchOptions
{
    // 在所有页面上搜索
    AllPages = true,
    
    // 可选：指定要匹配的文本
    // 文本 =“已批准”，
    
    // 可选：指定匹配类型
    // 匹配类型 = 文本匹配类型.包含
};
```

## 步骤3：执行文本签名搜索

使用配置的选项执行搜索操作：

```csharp
// 搜索文本签名
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

## 步骤4：处理并显示结果

遍历找到的文本签名并显示其详细信息：

```csharp
// 显示搜索结果
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");

foreach (TextSignature textSignature in signatures)
{
    Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
    Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
    Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
    Console.WriteLine();
}
```

## 完整示例

这是一个完整的工作示例，演示了如何在文档中搜索文本签名：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace TextSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文档路径 - 使用您的文件路径更新
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // 初始化签名实例
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // 配置文本搜索选项
                    TextSearchOptions options = new TextSearchOptions
                    {
                        // 在所有页面上搜索
                        AllPages = true
                    };
                    
                    // 搜索文本签名
                    List<TextSignature> signatures = signature.Search<TextSignature>(options);
                    
                    // 显示搜索结果
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");
                    
                    foreach (TextSignature textSignature in signatures)
                    {
                        Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
                        Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
                        Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## 高级文本签名搜索技术

### 使用特定文本条件搜索

为了更有针对性的搜索，您可以自定义 `TextSearchOptions` 按特定文本内容进行过滤：

```csharp
// 使用特定文本条件创建搜索选项
TextSearchOptions options = new TextSearchOptions
{
    // 在所有页面上搜索
    AllPages = true,
    
    // 搜索特定文本
    Text = "Approved",
    
    // 指定匹配类型（包含、精确、以...开头、以...结尾）
    MatchType = TextMatchType.Contains,
    
    // 区分大小写的搜索
    MatchCase = true
};
```

### 在特定文档区域中搜索

您可以将搜索限制在文档的特定区域：

```csharp
// 为特定文档区域创建搜索选项
TextSearchOptions options = new TextSearchOptions
{
    // 仅在特定页面上搜索
    AllPages = false,
    PageNumber = 1,
    
    // 或指定多个页面
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // 定义要搜索的特定区域
    Rectangle = new Rectangle(100, 100, 400, 200)
};
```

### 高级文本过滤

针对更复杂的搜索要求实现自定义过滤逻辑：

```csharp
// 使用自定义处理创建搜索选项
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    
    // 使用委托定义自定义处理
    ProcessCompleted = (TextSignature signature) =>
    {
        // 自定义验证逻辑
        bool isValid = signature.Text.Length > 5 && 
                      (signature.Text.Contains("Approved") || signature.Text.Contains("Verified"));
        
        return isValid;
    }
};
```

### 搜索不同的文本样式

使用字体和样式属性来过滤文本签名：

```csharp
// 创建针对特定文本外观的搜索选项
TextSearchOptions options = new TextSearchOptions
{
    // 按字体名称过滤
    FontName = "Arial",
    
    // 按字体大小范围过滤
    MinFontSize = 10,
    MaxFontSize = 14,
    
    // 按字体颜色过滤
    ForeColor = System.Drawing.Color.Blue
};
```

### 提取签名元数据

提取并处理与文本签名相关的元数据：

```csharp
foreach (TextSignature signature in signatures)
{
    // 访问签名元数据
    if (signature.Metadata != null && signature.Metadata.Count > 0)
    {
        Console.WriteLine("Signature Metadata:");
        
        foreach (var item in signature.Metadata)
        {
            Console.WriteLine($"  {item.Key}: {item.Value}");
        }
    }
    
    // 检查签名的创建和修改日期
    if (signature.CreatedOn.HasValue)
    {
        Console.WriteLine($"Created on: {signature.CreatedOn.Value}");
    }
    
    if (signature.ModifiedOn.HasValue)
    {
        Console.WriteLine($"Modified on: {signature.ModifiedOn.Value}");
    }
}
```

## 结论

在本指南中，我们探讨了如何使用 GroupDocs.Signature for .NET 在文档中搜索文本签名。从基本的搜索操作到高级技巧，您现在掌握了在 .NET 应用程序中实现强大文本签名功能的知识。

GroupDocs.Signature 提供了一个强大而灵活的文本签名处理框架，使您能够构建复杂的文档验证系统、自动化工作流程解决方案和合规性验证工具。

## 常见问题解答

### 我可以在受密码保护的文档中搜索文本签名吗？

是的，GroupDocs.Signature 支持在受密码保护的文档中搜索文本签名。您可以在初始化时提供密码 `Signature` 目的：

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // 搜索文本签名
}
```

### 文本签名搜索支持哪些文档格式？

GroupDocs.Signature 支持多种文档格式，包括 PDF、Microsoft Office 文档（Word、Excel、PowerPoint）、OpenOffice 格式、图像等。

### 我可以搜索具有特定格式（例如粗体或斜体）的文本签名吗？

是的，您可以使用 `FontBold` 和 `FontItalic` 属性 `TextSearchOptions`：

```csharp
TextSearchOptions options = new TextSearchOptions
{
    FontBold = true,
    FontItalic = true
};
```

### 如何提高大型文档的搜索性能？

对于大型文档，您可以通过以下方式优化搜索性能：

1. 将搜索限制在特定页面而不是搜索整个文档
2. 使用更具体的搜索条件来减少匹配数
3. 使用 `Rectangle` 如果你知道签名通常位于哪里
4. 在应用程序中实现分页以批量处理搜索结果

### 我能否检测文本签名是否以电子方式添加或是否是原始文档内容的一部分？

GroupDocs.Signature 可以区分文档中不同类型的文本元素。 `SignatureImplementation` 的财产 `TextSignature` 指示文本是正式签名还是常规文档内容。然而，最终的判断可能取决于文本最初是如何添加到文档中的。

## 参见

* [API 参考](https://reference.groupdocs.com/signature/net/)
* [GitHub 上的代码示例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [产品文档](https://docs.groupdocs.com/signature/net/)
* [产品页面](https://products.groupdocs.com/signature/net/)
* [下载最新版本](https://releases.groupdocs.com/signature/net/)
* [博客文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [免费支持论坛](https://forum.groupdocs.com/c/signature/13)
* [临时执照](https://purchase.groupdocs.com/temporary-license/)