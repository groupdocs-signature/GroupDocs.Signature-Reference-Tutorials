---
"description": "了解如何使用 GroupDocs.Signature for .NET 在图像中签名并嵌入元数据。添加作者信息、时间戳和自定义数据，以增强图像的真实性和可追溯性。"
"linktitle": "使用元数据对图像进行签名"
"second_title": "GroupDocs.签名 .NET API"
"title": "使用 C# .NET 中的元数据对图像进行签名"
"url": "/zh/net/document-signing/sign-image-with-metadata/"
"weight": 10
---

## 介绍

使用元数据进行数字图像签名对于确立真实性、所有权和可追溯性正变得越来越重要。GroupDocs.Signature for .NET 提供了一个强大且易于使用的解决方案，用于为各种图像格式添加元数据签名。本教程将指导您使用 C# 完成使用元数据对图像进行签名的完整过程。

元数据签名允许您将有价值的信息直接嵌入到图像文件中，例如作者信息、创建时间戳、唯一标识符等。这些信息将成为图像文件本身的一部分，从而提供一种可靠的方法来追踪和验证图像的真实性。

## 先决条件

在继续本教程之前，请确保您已具备以下条件：

1. [适用于 .NET 的 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - 下载并安装库
2. 开发环境 - Visual Studio 或任何支持 .NET 的兼容 IDE
3. 图像文件 - 支持格式（PNG、JPG、TIFF 等）的示例图像文件
4. 基本 C# 编程知识 - 熟悉 C# 编程概念

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

定义源图像的路径以及签名输出的保存位置：

```csharp
// 指定源图像文件的路径
string filePath = "sample.png";

// 定义签名图像的输出目录和文件名
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// 确保输出目录存在
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 步骤2：初始化签名对象

使用源图像文件创建 Signature 类的实例：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 其余代码将放在这里
}
```

## 步骤 3：创建和配置元数据签名

接下来，定义要嵌入图像的元数据。GroupDocs.Signature 支持多种元数据数据类型：

```csharp
// 初始化元数据ID（特定于图像格式）
ushort imgsMetadataId = 41996;

// 创建元数据选项对象
MetadataSignOptions options = new MetadataSignOptions();

// 添加各种类型的元数据签名
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // 字符串值
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // 日期时间值
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // 整数值
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // 双倍值
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // 十进制值
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // 浮点值
```

## 步骤 4：使用元数据对图像进行签名

将元数据签名应用于图像并保存结果：

```csharp
// 签署文件并保存到输出文件路径
SignResult result = signature.Sign(outputFilePath, options);

// 显示成功消息
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## 完整示例

以下是将所有步骤整合在一起的完整代码示例：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 指定文件路径
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // 确保输出目录存在
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // 使用元数据对图像进行签名
            using (Signature signature = new Signature(filePath))
            {
                // 初始化元数据ID（特定于图像格式）
                ushort imgsMetadataId = 41996;
                
                // 创建元数据选项
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 添加不同类型的元数据签名
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // 字符串值
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // 日期时间值
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // 整数值
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // 双倍值
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // 十进制值
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // 浮点值
                
                // 签署文件并保存到文件
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 显示结果
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 高级元数据签名技术

### 使用自定义元数据

您还可以创建具有特定 ID 的自定义元数据字段：

```csharp
// 使用特定 ID 创建自定义元数据
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### 验证元数据签名

签名后，您可能需要验证元数据签名：

```csharp
// 创建验证选项
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// 搜索元数据签名
SearchResult result = signature.Search(searchOptions);

// 显示找到的签名
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## 结论

在本教程中，您学习了如何使用 GroupDocs.Signature for .NET 为图像添加元数据签名。将元数据嵌入图像是增强图像真实性、添加关键信息以及改进文档管理工作流程的绝佳方法。该流程简单易用，功能强大，可根据您的具体需求进行定制。

图像文件中嵌入的元数据可用于各种目的，例如版权保护、追踪图像来源、添加描述性信息以及建立数字保管链。通过实施元数据签名，您可以确保图像在整个生命周期内保持完整性和真实性。

## 常见问题解答

### 我可以向现有的签名图像添加元数据吗？

是的，您可以向已包含元数据签名的图像添加额外的元数据。现有元数据将被保留，新的元数据也会相应地添加。

### 元数据签名支持哪些图像格式？

GroupDocs.Signature for .NET 支持多种图像格式的元数据签名，包括 PNG、JPEG、TIFF、BMP、GIF 等。完整列表请参阅 [官方文档](https://docs。groupdocs.com/signature/net/).

### 是否可以加密图像中的元数据？

是的，GroupDocs.Signature 提供了加密元数据的选项，以增强安全性。您可以使用该库提供的加密选项来保护敏感的元数据信息。

### 我可以通过编程验证签名图像的真实性吗？

当然。您可以使用 GroupDocs.Signature 中的验证方法来验证元数据签名并确认签名图像的真实性。

### 使用元数据对图像进行签名时，文件大小是否有限制？

该库本身没有具体的文件大小限制，但处理非常大的文件可能需要更多处理时间和内存。建议在处理超大图像时考虑系统资源。

### 我如何获得用于测试的临时许可证？

您可以获得 [临时执照](https://purchase.groupdocs.com/temporary-license/) 用于在购买之前测试 GroupDocs.Signature。

### 我可以在哪里找到更多资源和支持？

- [API 参考](https://reference.groupdocs.com/signature/net/)
- [下载](https://releases.groupdocs.com/signature/net/)
- [示例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [文档](https://docs.groupdocs.com/signature/net/)
- [产品页面](https://products.groupdocs.com/signature/net/)
- [博客](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [支持论坛](https://forum.groupdocs.com/c/signature/13)