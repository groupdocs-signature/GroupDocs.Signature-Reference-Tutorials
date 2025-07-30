---
"description": "通过我们的分步开发人员指南，了解如何使用 GroupDocs.Signature for .NET 轻松地从文档中删除二维码签名。"
"linktitle": "从文档中删除二维码签名"
"second_title": "GroupDocs.签名 .NET API"
"title": "如何从 .NET 文档中删除二维码签名"
"url": "/zh/net/delete-operations/delete-qr-code-signature/"
"weight": 16
---

# 如何从文档中删除二维码签名

## 介绍

您是否曾经需要通过编程方式从文档中删除二维码签名？无论您是清理过期信息，还是准备重新分发文档，有效地管理文档签名对于 .NET 开发人员来说都是一项至关重要的技能。

在本指南中，我们将详细指导您如何使用 GroupDocs.Signature for .NET 从文档中删除二维码签名。这个强大的库使签名管理变得简单易行，让您可以专注于构建出色的应用程序，而无需费力应对文档操作的挑战。

## 开始之前你需要什么

在深入研究代码之前，请确保一切准备就绪：

- GroupDocs.Signature for .NET：您需要在项目中安装该库。您可以直接从 [GroupDocs 发布页面](https://releases。groupdocs.com/signature/net/).
- 带有二维码的文档：为了练习，准备一份包含至少一个您想要删除的二维码签名的文档。
- 基本 C# 知识：您应该熟悉 C# 基础知识，以便能够遵循我们的示例。

一旦满足了这些先决条件，您就可以开始删除这些二维码了！

## 使用正确的命名空间设置你的项目

首先，让我们导入必要的命名空间，以使我们的代码顺利运行：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

这些导入使我们能够访问 GroupDocs.Signature 库中所需的所有功能，以及一些用于文件处理的基本 .NET 类。

## 步骤1：你的文件在哪里？设置文档路径

让我们首先定义文档的位置以及我们想要保存修改版本的位置：

```csharp
// 文档目录的路径。
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

// 定义修改后的文档的输出文件路径。
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);

// 复制源文件，因为 Delete 方法适用于同一个 Document。
File.Copy(filePath, outputFilePath, true);
```

请注意，我们正在创建原始文档的副本。这一点很重要，因为签名删除过程会直接修改文件，而我们始终希望保留原始文档。

## 步骤 2：创建要使用的签名对象

现在我们将创建一个连接到我们文档的签名对象：

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    // 创建搜索二维码签名的选项。
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    
    // 在文档中搜索二维码签名。
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```

这段代码使用我们的文档初始化 Signature 对象，然后搜索其中存在的任何二维码签名。搜索将返回找到的所有二维码签名的列表。

## 步骤 3：是否有需要删除的二维码？

在尝试删除任何内容之前，我们应该检查是否存在二维码：

```csharp
    if (signatures.Count > 0)
    {
        // 获取文档中找到的第一个二维码签名。
        QrCodeSignature qrCodeSignature = signatures[0];
```

这个简单的检查确保只有文档中至少有一个二维码签名时，我们才能继续执行。在本例中，我们的目标是找到的第一个二维码，但您可以根据需要轻松修改它以处理多个签名。

## 步骤4：从文档中删除二维码

现在进入正题——删除二维码：

```csharp
        // 从文档中删除二维码签名。
        bool result = signature.Delete(qrCodeSignature);
        
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Console.WriteLine($"Signature was not deleted from the document! Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```

代码会删除签名并提供操作是否成功的反馈。此反馈对于调试和确认代码是否按预期工作至关重要。

## 我们取得了什么成就？

恭喜！您刚刚学习了如何使用 GroupDocs.Signature for .NET 从文档中删除二维码签名。这项技能将为您的应用程序中的文档管理带来无限可能。

只需几行代码，您现在就可以以编程方式清理文档，删除过时或不必要的二维码签名，确保您的文档始终只包含相关信息。

## 您可能遇到的常见问题

### 我可以一次删除多个二维码吗？

当然！除了删除找到的第一个签名之外，您还可以遍历整个签名列表，然后删除每个签名，如下所示：

```csharp
foreach(var qrSignature in signatures)
{
    signature.Delete(qrSignature);
}
```

### 我可以使用 GroupDocs.Signature 管理哪些其他类型的签名？

GroupDocs.Signature 功能极其丰富，支持各种签名类型，包括：
- 文本签名
- 图像签名
- 条形码签名
- 数字签名
- 还有更多！

### 这适用于我所有的文档格式吗？

您会很高兴地知道 GroupDocs.Signature 适用于多种文档格式，包括：
- PDF 文档
- Microsoft Word 文档
- Excel 电子表格
- PowerPoint 演示文稿
- 以及其他许多人

### 我可以搜索特定的二维码而不是删除所有二维码吗？

是的！ `QrCodeSearchOptions` 该类提供各种属性来过滤搜索结果。例如，您可以搜索包含特定文本或以特定格式编码的二维码。

### 有没有办法在购买之前试用 GroupDocs.Signature？

是的，您可以从下载免费试用版 [GroupDocs 网站](https://releases.groupdocs.com/) 在做出承诺之前，用你的具体用例来测试它。