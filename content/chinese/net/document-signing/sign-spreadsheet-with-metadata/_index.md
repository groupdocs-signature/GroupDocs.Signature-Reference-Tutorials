---
"description": "使用 GroupDocs.Signature for .NET 嵌入元数据签名，保护并增强 Excel 电子表格的功能。添加作者信息、时间戳和自定义数据，以提高文档的可追溯性和真实性。"
"linktitle": "使用元数据签署电子表格"
"second_title": "GroupDocs.签名 .NET API"
"title": "在 C# .NET 中向 Excel 电子表格添加元数据签名"
"url": "/zh/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
---

## 介绍

Excel 电子表格通常包含关键业务数据、财务信息和重要计算。在许多专业环境中，确保其真实性、追踪其来源并保护其完整性至关重要。增强电子表格安全性和可追溯性的一种有效方法是嵌入元数据签名。

本教程将指导您使用 GroupDocs.Signature for .NET 为 Excel 电子表格添加元数据签名。通过添加元数据签名，您可以将有价值的信息（例如作者详细信息、创建时间戳、文档标识符和其他自定义属性）直接嵌入到电子表格文件结构中。

## 先决条件

在继续本教程之前，请确保您已具备以下条件：

1. [适用于 .NET 的 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - 下载并安装库
2. 开发环境 - Visual Studio 或任何其他与 .NET 兼容的 IDE
3. Excel 电子表格 - 示例电子表格文件（XLSX、XLS 等）
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

定义源电子表格的路径以及签名输出的保存位置：

```csharp
// 指定 Excel 文件的路径
string filePath = "sample.xlsx";

// 定义签名电子表格的输出目录和文件名
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// 确保输出目录存在
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 步骤2：初始化签名对象

使用源电子表格文件创建 Signature 类的实例：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 其余代码将放在这里
}
```

## 步骤 3：创建和配置元数据签名

接下来，定义元数据选项并创建电子表格元数据签名数组：

```csharp
// 创建元数据选项对象
MetadataSignOptions options = new MetadataSignOptions();

// 创建具有不同数据类型的电子表格元数据签名数组
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // 字符串值
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // 日期时间值
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // 整数值
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // 双倍值
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // 十进制值
    new SpreadsheetMetadataSignature("Total", 123.456F)               // 浮点值
};

// 将签名收集添加到选项
options.Signatures.AddRange(signatures);
```

## 步骤 4：使用元数据对电子表格进行签名

将元数据签名应用到电子表格并保存结果：

```csharp
// 签署文件并保存到输出文件路径
SignResult result = signature.Sign(outputFilePath, options);

// 显示成功消息
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## 完整示例

以下是将所有步骤整合在一起的完整代码示例：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 指定文件路径
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // 确保输出目录存在
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // 使用元数据对电子表格进行签名
            using (Signature signature = new Signature(filePath))
            {
                // 创建元数据选项对象
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 创建具有不同数据类型的电子表格元数据签名数组
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // 字符串值
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // 日期时间值
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // 整数值
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // 双倍值
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // 十进制值
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // 浮点值
                };
                
                // 将签名收集添加到选项
                options.Signatures.AddRange(signatures);
                
                // 签署文件并保存到文件
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 显示结果
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 高级电子表格元数据技术

### 使用自定义和内置电子表格属性

Excel 电子表格具有内置属性和自定义属性，可通过文件属性对话框访问。GroupDocs.Signature 允许您同时使用以下两种属性：

```csharp
// 添加内置属性
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// 添加自定义属性
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### 在签名的电子表格中搜索元数据

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

### 更新现有元数据

您可以使用相同的属性名称更新电子表格中的现有元数据：

```csharp
// 更新现有元数据
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## 结论

在本综合教程中，您学习了如何使用 GroupDocs.Signature for .NET 为 Excel 电子表格添加元数据签名。将元数据嵌入电子表格文件可以增强文档的可追溯性，提供有价值的上下文信息，并有助于确认其真实性。

电子表格中的元数据签名在商业环境中尤为有用，因为文档来源、作者身份和版本跟踪至关重要。嵌入的元数据可以包含与组织需求相关的作者、创建时间、文档标识符以及自定义属性的信息。

通过使用 GroupDocs.Signature 实现元数据签名，您可以确保您的 Excel 电子表格在其整个生命周期内保持其完整性并提供可验证的信息。

## 常见问题解答

### 我可以向已经定义某些属性的电子表格添加元数据吗？

是的，您可以在电子表格中添加新的元数据或更新现有的元数据。GroupDocs.Signature 将处理集成，方法是添加新的属性或更新具有相同名称的现有属性。

### 元数据签名支持哪些电子表格格式？

GroupDocs.Signature for .NET 支持各种电子表格格式的元数据签名，包括 XLSX、XLS、XLSM、ODS 等。完整列表请参阅 [官方文档](https://docs。groupdocs.com/signature/net/).

### 电子表格中的元数据签名对用户可见吗？

元数据签名在电子表格内容本身中不可见。但是，可以通过 Excel 或其他兼容应用程序中的文档属性面板查看。

### 添加元数据后，我可以通过编程验证电子表格是否被篡改吗？

是的，GroupDocs.Signature 提供验证功能，可以帮助检测文档在签名后是否被修改，包括元数据的更改。

### 添加元数据会影响电子表格功能吗？

添加元数据对文件大小的影响极小，并且不会影响电子表格的功能。这是一种增强文档属性的轻量级方法，不会影响计算、公式或其他 Excel 功能。

### 我可以在哪里找到更多资源和支持？

- [API 参考](https://reference.groupdocs.com/signature/net/)
- [下载](https://releases.groupdocs.com/signature/net/)
- [示例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [文档](https://docs.groupdocs.com/signature/net/)
- [产品页面](https://products.groupdocs.com/signature/net/)
- [博客](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [支持论坛](https://forum.groupdocs.com/c/signature/13)
- [临时执照](https://purchase.groupdocs.com/temporary-license/)