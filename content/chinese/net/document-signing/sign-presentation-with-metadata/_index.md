---
title: 使用元数据签署演示文稿
linktitle: 使用元数据签署演示文稿
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 使用元数据对演示文稿文件进行签名。增强文档完整性并添加有价值的信息。
type: docs
weight: 12
url: /zh/net/document-signing/sign-presentation-with-metadata/
---
## 介绍
在本教程中，我们将学习如何使用 GroupDocs.Signature for .NET 库对演示文稿文件 (PPTX) 进行元数据签名。使用元数据对演示文稿进行签名会向文档添加有价值的信息，例如作者姓名、创建日期、文档 ID、签名 ID 和各种数值。
## 先决条件
在我们开始之前，请确保您具备以下条件：
1.  GroupDocs.Signature for .NET Library：从以下位置下载并安装该库[这里](https://releases.groupdocs.com/signature/net/).
2. 开发环境：确保您已设置 .NET 开发环境。
3. 演示文件：准备好示例演示文件（PPTX 格式）以供签名。
4. 对 C# 的基本了解：熟悉 C# 编程语言将会很有帮助。

## 导入命名空间
在深入研究代码之前，让我们导入必要的命名空间：
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## 第 1 步：加载演示文件
```csharp
string filePath = "sample.pptx";
```
代替`"sample.pptx"`以及演示文稿文件的路径。
## 第2步：指定输出文件路径
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
指定要保存签名的演示文稿文件及其文件名的目录。
## 第三步：初始化签名对象
```csharp
using (Signature signature = new Signature(filePath))
```
通过提供演示文件的路径来初始化 Signature 对象。
## 第 4 步：定义元数据签名选项
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
创建 MetadataSignOptions 的实例来定义元数据签名选项。
## 第 5 步：创建元数据签名
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
创建一个PresentationMetadataSignature 对象数组，每个对象代表一个元数据签名。您可以添加各种类型的元数据，包括字符串、日期时间、整数、双精度、小数和浮点。
## 第 6 步：将签名添加到选项
```csharp
options.Signatures.AddRange(signatures);
```
将创建的元数据签名添加到 MetadataSignOptions 对象。
## 第 7 步：签署文件
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
使用指定的选项使用元数据对演示文稿文件进行签名，并将签名的文件保存到输出路径。
## 第8步：显示结果
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
显示成功消息以及应用的签名数量以及签名文件的保存路径。

## 结论
在本教程中，我们学习了如何使用 GroupDocs.Signature for .NET 库使用元数据对演示文稿文件进行签名。添加元数据签名可以增强文档的完整性并提供有关其内容的有价值的信息。

## 常见问题解答
### 我可以使用 GroupDocs.Signature for .NET 对除 PPTX 之外的其他文档格式使用元数据进行签名吗？
是的，GroupDocs.Signature 支持各种文档格式，包括 Word、Excel、PDF 等，以便使用元数据进行签名。
### GroupDocs.Signature for .NET 是否与 .NET Core 兼容？
是的，该库与 .NET Framework 和 .NET Core 兼容。
### 我可以自定义元数据签名的外观吗？
是的，您可以根据您的要求自定义元数据签名的外观、位置和其他属性。
### GroupDocs.Signature for .NET 是否为签名文档提供加密？
是的，GroupDocs.Signature 提供加密选项来保护签名文档免遭未经授权的访问。
### 购买前是否有试用版可供测试？
是的，您可以从以下位置免费试用 GroupDocs.Signature for .NET：[这里](https://releases.groupdocs.com/).