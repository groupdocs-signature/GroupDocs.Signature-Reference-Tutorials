---
"description": "使用 GroupDocs.Signature for .NET 向 Word 文档添加元数据签名。嵌入作者详细信息、时间戳和自定义属性，以增强文档安全性和可追溯性。"
"linktitle": "使用元数据进行符号文字处理"
"second_title": "GroupDocs.签名 .NET API"
"title": "使用 C# .NET 中的元数据签名增强 Word 文档"
"url": "/zh/net/document-signing/sign-word-processing-with-metadata/"
"weight": 14
type: docs
---
## 介绍

文字处理文档是商业、教育和个人通信中最常用的文件类型之一。在许多专业环境中，确保这些文档的真实性、追踪来源并维护其完整性至关重要。增强文档安全性和可追溯性的一种有效方法是嵌入元数据签名。

本教程将全面指导您使用 GroupDocs.Signature for .NET 为文字处理文档添加元数据签名。通过添加元数据签名，您可以将有价值的信息（例如作者详细信息、创建时间戳、文档标识符和其他自定义属性）直接嵌入到文档文件结构中。

## 先决条件

在继续本教程之前，请确保您已具备以下条件：

1. [适用于 .NET 的 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - 下载并安装库
2. 开发环境 - Visual Studio 或任何其他与 .NET 兼容的 IDE
3. Word 文档 - 示例文档文件（DOCX、DOC 等）
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

定义源 Word 文档的路径以及签名输出的保存位置：

```csharp
// 指定 Word 文档的路径
string filePath = "sample.docx";

// 定义签名文档的输出目录和文件名
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");

// 确保输出目录存在
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 步骤2：初始化签名对象

使用源 Word 文档创建 Signature 类的实例：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 其余代码将放在这里
}
```

## 步骤 3：创建和配置元数据签名

接下来，定义元数据选项并添加不同类型的元数据签名：

```csharp
// 创建元数据选项对象
MetadataSignOptions options = new MetadataSignOptions();

// 使用流畅的界面添加各种类型的元数据
options
    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // 字符串值
    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // 日期时间值
    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // 整数值
    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // 双倍值
    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // 十进制值
    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // 浮点值
```

## 步骤 4：使用元数据签署文档

将元数据签名应用到 Word 文档并保存结果：

```csharp
// 签署文件并保存到输出文件路径
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

namespace SignWordProcessingWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 指定文件路径
            string filePath = "sample.docx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");
            
            // 确保输出目录存在
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // 使用元数据对 Word 文档进行签名
            using (Signature signature = new Signature(filePath))
            {
                // 创建元数据选项对象
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 添加不同类型的元数据签名
                options
                    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // 字符串值
                    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // 日期时间值
                    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // 整数值
                    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // 双倍值
                    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // 十进制值
                    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // 浮点值
                
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

## 高级 Word 文档元数据技术

### 使用自定义和内置文档属性

Word 文档具有内置属性和自定义属性，可通过文档属性面板访问。GroupDocs.Signature 允许您同时使用以下两种属性：

```csharp
// 添加内置属性
options
    .Add(new WordProcessingMetadataSignature("Company", "Sherlock Holmes Consulting"))
    .Add(new WordProcessingMetadataSignature("Category", "Legal Document"))
    .Add(new WordProcessingMetadataSignature("Keywords", "contract,agreement,legal"))
    .Add(new WordProcessingMetadataSignature("Comments", "This document is confidential"))
    .Add(new WordProcessingMetadataSignature("Manager", "John Watson"));

// 添加自定义属性
options.Add(new WordProcessingMetadataSignature("Department", "Legal"));
options.Add(new WordProcessingMetadataSignature("SecurityLevel", "Confidential"));
```

### 在签名的 Word 文档中搜索元数据

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

### 使用文档变量

Word 文档还支持文档变量，这是另一种形式的元数据：

```csharp
// 添加文档变量
options.Add(new WordProcessingMetadataSignature("DocVariable1", "Custom Value 1", true));
options.Add(new WordProcessingMetadataSignature("DocVariable2", DateTime.Now, true));
```

## 结论

在本综合教程中，您学习了如何使用 GroupDocs.Signature for .NET 为 Word 处理文档添加元数据签名。将元数据嵌入 Word 文档可以增强文档的可追溯性，提供有价值的上下文信息，并有助于确认文档的真实性。

Word 文档中的元数据签名在商业和法律环境中尤其有用，因为这些环境中文档来源、作者身份和版本跟踪非常重要。嵌入的元数据可以包含与组织需求相关的作者、创建时间、文档标识符和自定义属性的信息。

通过使用 GroupDocs.Signature 实现元数据签名，您可以确保您的 Word 文档在其整个生命周期内保持其完整性并提供可验证的信息。

## 常见问题解答

### 我可以向已经定义某些属性的 Word 文档添加元数据吗？

是的，您可以在 Word 文档中添加新的元数据或更新现有的元数据。GroupDocs.Signature 将处理集成，方法是添加新的属性或更新具有相同名称的现有属性。

### 元数据签名支持哪些文字处理格式？

GroupDocs.Signature for .NET 支持各种文字处理格式的元数据签名，包括 DOCX、DOC、RTF、ODT 等。完整列表请参阅 [文档](https://docs。groupdocs.com/signature/net/).

### Word 文档中的元数据签名对读者可见吗？

元数据签名在文档内容本身中不可见。但是，可以通过 Microsoft Word 或其他兼容应用程序中的文档属性面板查看。

### 添加元数据后，我可以通过编程验证 Word 文档是否被篡改吗？

是的，GroupDocs.Signature 提供验证功能，可以帮助检测文档在签名后是否被修改，包括元数据的更改。

### 是否可以从 Word 文档中删除元数据？

是的，GroupDocs.Signature 提供了根据需要从文档中删除元数据签名的选项。这对于在外部共享文档之前清理敏感信息非常有用。

### 我可以在哪里找到更多资源和支持？

- [API 参考](https://reference.groupdocs.com/signature/net/)
- [下载](https://releases.groupdocs.com/signature/net/)
- [示例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [文档](https://docs.groupdocs.com/signature/net/)
- [产品页面](https://products.groupdocs.com/signature/net/)
- [博客](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [支持论坛](https://forum.groupdocs.com/c/signature/13)
- [临时执照](https://purchase.groupdocs.com/temporary-license/)