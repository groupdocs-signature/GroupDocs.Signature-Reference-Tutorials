---
"description": "了解如何使用 GroupDocs.Signature for .NET 在文档中搜索多种签名类型。本指南包含增强文档安全性的代码示例，内容全面。"
"linktitle": "搜索多个签名"
"second_title": "GroupDocs.签名 .NET API"
"title": "在文档中搜索多种签名类型"
"url": "/zh/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
---

## 介绍

在现代文档管理系统中，在单个文档中搜索和验证多种签名类型的能力日益重要。组织通常使用各种签名类型（例如数字签名、文本签名、条形码、二维码等）来增强文档安全性并简化验证流程。GroupDocs.Signature for .NET 提供了一个强大的框架，使开发人员能够跨各种文档格式实现全面的签名搜索功能。

本教程将指导您使用 GroupDocs.Signature for .NET 在文档中搜索多种签名类型的过程，并提供详细的解释和实用的代码示例。

## 先决条件

在深入实现多重签名搜索功能之前，请确保您满足以下先决条件：

1. 开发环境：Visual Studio 或系统上安装的任何首选的 .NET 开发环境。
  
2. GroupDocs.Signature for .NET：从以下位置下载并安装 GroupDocs.Signature for .NET 库 [这里](https://releases。groupdocs.com/signature/net/).

3. 基本 C# 知识：熟悉 C# 编程语言和 .NET 框架概念。

4. 样本文件：准备包含各种类型签名的测试文件，以供测试目的。

## 导入命名空间

首先导入访问 GroupDocs.Signature 功能所需的命名空间：

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

现在，让我们将搜索多种签名类型的过程分解为清晰、易于管理的步骤：

## 步骤 1：加载文档

首先，加载包含要搜索的签名的文档：

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // 多重签名搜索代码将在此处添加
}
```

## 步骤 2：定义不同签名类型的搜索选项

为您想要搜索的每种签名类型创建搜索选项：

```csharp
// 定义文本签名的搜索选项
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // 在所有页面上搜索
    Text = "Signature",  // 可选：要查找的文本
    MatchType = TextMatchType.Contains  // 匹配条件
};

// 定义数字签名的搜索选项
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// 定义条形码签名的搜索选项
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // 可选：要匹配的条形码文本
    MatchType = TextMatchType.Exact  // 匹配条件
};

// 定义二维码签名的搜索选项
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // 可选：要匹配的二维码文本
    MatchType = TextMatchType.Contains  // 匹配条件
};

// 定义元数据签名的搜索选项
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## 步骤 3：向集合添加选项

将所有搜索选项添加到集合中：

```csharp
// 创建一个列表来保存所有搜索选项
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## 步骤 4：执行搜索并处理结果

使用组合搜索选项执行搜索并处理结果：

```csharp
// 使用定义的选项搜索所有签名类型
SearchResult result = signature.Search(searchOptions);

// 检查是否找到签名
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // 遍历找到的签名
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // 处理特定签名类型
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## 完整示例

这是一个完整的、可运行的示例，演示了如何在文档中搜索多种签名类型：

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文档路径
            string filePath = "sample_multiple_signatures.docx";
            
            // 初始化签名实例
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // 定义文本签名的搜索选项
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // 定义数字签名的搜索选项
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // 定义条形码签名的搜索选项
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // 定义二维码签名的搜索选项
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // 定义元数据签名的搜索选项
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // 创建一个列表来保存所有搜索选项
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // 搜索所有签名类型
                    SearchResult result = signature.Search(searchOptions);

                    // 检查是否找到签名
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // 按签名类型处理结果
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // 处理特定签名类型
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // 在签名之间添加换行符
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## 高级多重签名搜索技术

### 过滤搜索结果

您可以实施高级过滤来缩小搜索结果：

```csharp
// 按页码过滤结果
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// 按签名类型过滤结果
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// 过滤包含特定内容的文本签名
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### 验证多个签名

针对不同的签名类型实现验证逻辑：

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // 检查文档是否具有有效的数字签名
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // 检查文档是否具有所需的二维码
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### 使用自定义处理进行搜索

您可以为搜索操作定义自定义处理逻辑：

```csharp
// 使用自定义处理创建搜索选项
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // 使用委托定义自定义处理
    ProcessCompleted = (signature) =>
    {
        // 自定义验证逻辑 - 仅接受指定页面上的签名
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## 结论

在本指南中，我们探讨了如何使用 GroupDocs.Signature for .NET 在文档中搜索多种签名类型。从设置不同签名类型的搜索选项到处理和验证结果，您现在掌握了在 .NET 应用程序中实现强大签名搜索功能的知识。

同时搜索多种签名类型的功能可增强文档验证流程、强化安全措施并简化文档验证工作流程。GroupDocs.Signature 提供了一个强大而灵活的框架，可用于处理不同文档格式的各种签名类型，使其成为文档处理应用程序的理想选择。

## 常见问题解答

### 我可以搜索受密码保护的文档中的签名吗？

是的，GroupDocs.Signature 支持在受密码保护的文档中搜索签名。您可以在初始化时提供密码 `Signature` 目的：

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // 搜索签名
}
```

### 签名搜索支持哪些文档格式？

GroupDocs.Signature 支持多种文档格式，包括 PDF、Microsoft Office 文档（Word、Excel、PowerPoint）、OpenOffice 格式、图像等。

### 我可以将搜索限制在文档中的特定页面吗？

是的，每种搜索选项类型都有允许您指定要搜索的页面的属性：

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // 不要搜索所有页面
    PageNumber = 1,    // 仅搜索第 1 页
    
    // 或指定多个页面
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### 如何优化在大型文档中搜索时的性能？

对于大型文档，您可以通过以下方式优化性能：

1. 将搜索限制在特定页面或页面范围
2. 使用更具体的搜索条件来减少潜在匹配的数量
3. 在结果显示中实现分页
4. 如果不需要同时获得结果，则一次搜索一种签名类型

### 我可以扩展 GroupDocs.Signature 以支持自定义签名类型吗？

虽然 GroupDocs.Signature 为常见签名类型提供了内置支持，但您可以通过以下方式扩展其功能：

1. 创建派生自的自定义搜索选项类 `SearchOptions`
2. 使用实现自定义处理逻辑 `ProcessCompleted` 代表
3. 开发将多个签名搜索与高级业务逻辑相结合的包装类

## 参见

* [API 参考](https://reference.groupdocs.com/signature/net/)
* [GitHub 上的代码示例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [产品文档](https://docs.groupdocs.com/signature/net/)
* [产品页面](https://products.groupdocs.com/signature/net/)
* [下载最新版本](https://releases.groupdocs.com/signature/net/)
* [博客文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [免费支持论坛](https://forum.groupdocs.com/c/signature/13)
* [临时执照](https://purchase.groupdocs.com/temporary-license/)