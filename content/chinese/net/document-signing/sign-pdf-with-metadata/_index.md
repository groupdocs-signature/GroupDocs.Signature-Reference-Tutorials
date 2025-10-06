---
"description": "使用 GroupDocs.Signature for .NET 将元数据签名集成到 PDF 文档中。学习如何嵌入作者信息、时间戳和自定义数据，以增强 PDF 的真实性和可追溯性。"
"linktitle": "使用元数据签署 PDF"
"second_title": "GroupDocs.签名 .NET API"
"title": "在 C# .NET 中向 PDF 文档添加元数据签名"
"url": "/zh/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
type: docs
---
## 介绍

PDF（可移植文档格式）文档因其一致性和平台独立性而被广泛应用于各行各业。在许多专业环境中，确保这些文档的真实性和可追溯性至关重要。实现这一点的一个有效方法是将元数据嵌入到 PDF 文件中。

在本综合教程中，我们将探讨如何使用 GroupDocs.Signature for .NET 为 PDF 文档添加元数据签名。元数据签名允许您在文档中嵌入其他信息，例如作者详细信息、创建时间戳、文档标识符和自定义值，而不会明显改变文档的外观。

## 先决条件

在开始之前，请确保您已准备好以下事项：

1. [适用于 .NET 的 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - 下载并安装库
2. 开发环境 - Visual Studio 或任何其他与 .NET 兼容的 IDE
3. PDF 文档 - 用于签名的示例 PDF 文件
4. 基本 C# 知识 - 熟悉 C# 编程语言

## 导入命名空间

首先导入必要的命名空间来访问 GroupDocs.Signature 功能：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## 步骤 1：设置文件路径

首先，定义 PDF 文档的路径并指定要保存签名输出的位置：

```csharp
// 指定 PDF 文档的路径
string filePath = "sample.pdf";

// 定义输出目录和文件路径
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// 确保输出目录存在
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 步骤2：初始化签名对象

使用源 PDF 文档创建 Signature 类的实例：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 签名代码将放在这里
}
```

## 步骤 3：定义元数据选项

创建并配置元数据选项，添加各种类型的元数据签名：

```csharp
// 创建元数据选项对象
MetadataSignOptions options = new MetadataSignOptions();

// 使用流畅的界面添加各种类型的元数据
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // 字符串值
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // 日期时间值
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // 整数值
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // 双倍值
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // 十进制值
    .Add(new PdfMetadataSignature("Total", 123.456F));              // 浮点值
```

## 步骤 4：使用元数据签署 PDF

将元数据签名应用到 PDF 文档并保存结果：

```csharp
// 签署文档并保存到输出路径
SignResult result = signature.Sign(outputFilePath, options);

// 显示成功消息
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## 完整示例

以下是将所有步骤整合在一起的完整代码示例：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 指定文件路径
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // 确保输出目录存在
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // 使用元数据对 PDF 进行签名
            using (Signature signature = new Signature(filePath))
            {
                // 创建元数据选项对象
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 添加不同类型的元数据签名
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // 字符串值
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // 日期时间值
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // 整数值
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // 双倍值
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // 十进制值
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // 浮点值
                
                // 签署文件并保存到文件
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 显示结果
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 高级 PDF 元数据操作

### 添加具有命名空间支持的自定义元数据

PDF 文档支持具有 XML 命名空间支持的自定义元数据：

```csharp
// 使用命名空间添加自定义元数据
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema”
});
```

### 在签名的 PDF 中搜索元数据

签名后，您可能需要验证或提取元数据：

```csharp
// 创建元数据的搜索选项
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// 搜索元数据签名
SearchResult searchResult = signature.Search(searchOptions);

// 显示找到的签名
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### 使用标准 PDF 元数据

PDF 文档具有可以访问和修改的标准元数据字段：

```csharp
// 设置标准 PDF 元数据字段
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## 结论

在本教程中，您学习了如何使用 GroupDocs.Signature for .NET 为 PDF 文档添加元数据签名。将元数据嵌入 PDF 文件，可以有效增强文档真实性、添加关键信息，并改进文档管理工作流程。

PDF 中的元数据签名在商业环境中尤为重要，因为文档的可追溯性和真实性验证至关重要。嵌入的元数据可以包含文档来源、作者、创建时间、版本以及与组织工作流程相关的自定义属性的信息。

通过使用 GroupDocs.Signature 实现元数据签名，您可以确保您的 PDF 文档在其整个生命周期内保持其完整性并提供可验证的信息。

## 常见问题解答

### 我可以修改 PDF 文档中现有的元数据吗？

是的，您可以修改 PDF 文档中现有的元数据。当您应用与现有元数据签名同名的新元数据签名时，其值将相应更新。

### PDF 文档中的元数据签名对最终用户可见吗？

元数据签名在文档内容本身中不可见。但是，可以通过 Adobe Acrobat 等 PDF 阅读器的文档属性面板或使用专门的元数据查看工具来查看它们。

### 我可以加密或保护 PDF 中的元数据吗？

GroupDocs.Signature 提供文档安全选项，包括加密。您可以应用文档级加密来保护整个 PDF，包括其元数据。

### 我可以向 PDF 添加多少元数据有限制吗？

虽然 PDF 规范没有严格限制，但添加过多的元数据可能会增加文件大小。建议在元数据中仅包含相关且必要的信息。

### 添加元数据后，我可以通过编程验证 PDF 是否被篡改吗？

是的，GroupDocs.Signature 提供验证功能，可以帮助检测文档在签名后是否被修改，包括元数据的更改。

### 我可以在哪里找到更多资源和支持？

- [API 参考](https://reference.groupdocs.com/signature/net/)
- [下载](https://releases.groupdocs.com/signature/net/)
- [示例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [文档](https://docs.groupdocs.com/signature/net/)
- [产品页面](https://products.groupdocs.com/signature/net/)
- [博客](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [支持论坛](https://forum.groupdocs.com/c/signature/13)
- [临时执照](https://purchase.groupdocs.com/temporary-license/)