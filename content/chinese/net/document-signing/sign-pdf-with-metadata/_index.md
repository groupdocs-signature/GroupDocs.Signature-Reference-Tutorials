---
title: 使用元数据签署 PDF
linktitle: 使用元数据签署 PDF
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 使用元数据对 PDF 文档进行签名。轻松增强文档的可追溯性和真实性。
weight: 11
url: /zh/net/document-signing/sign-pdf-with-metadata/
---
## 介绍
在本教程中，我们将学习如何使用 GroupDocs.Signature for .NET 使用元数据对 PDF 文档进行签名。向 PDF 添加元数据可以提供有关文档的附加信息，例如作者身份、创建日期、文档 ID 等。
## 先决条件
在我们开始之前，请确保您具备以下条件：
1.  GroupDocs.Signature for .NET：您可以从以下位置下载：[这里](https://releases.groupdocs.com/signature/net/).
2. PDF 文档：准备好示例 PDF 文件以供签名。
3. C# 编程基础知识：需要熟悉 C# 语法才能理解代码示例。
## 导入命名空间
首先，确保导入必要的命名空间来访问所需的类和方法：
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：加载 PDF 文档
加载您要签名的 PDF 文档：
```csharp
string filePath = "sample.pdf";
```
## 第2步：指定输出文件路径
定义保存带有元数据的签名 PDF 的输出文件路径：
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## 步骤3：创建签名实例
通过提供 PDF 文档的路径来初始化 Signature 实例：
```csharp
using (Signature signature = new Signature(filePath))
{
    //签名相关代码将放在这里
}
```
## 第 4 步：定义元数据选项
创建 MetadataSignOptions 并添加元数据字段及其各自的值：
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) //字符串值
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       //日期时间值
    .Add(new PdfMetadataSignature("DocumentId", 123456))            //整数值
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         //双倍值
    .Add(new PdfMetadataSignature("Amount", 123.456M))              //十进制值
    .Add(new PdfMetadataSignature("Total", 123.456F));              //浮点值
```
## 第 5 步：签署文件
使用指定的元数据选项对 PDF 文档进行签名并保存签名的文档：
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 结论
在本教程中，我们介绍了如何使用 GroupDocs.Signature for .NET 使用元数据对 PDF 文档进行签名。通过遵循分步指南，您可以轻松地将元数据信息（例如作者身份、创建日期等）添加到 PDF 文件中，从而增强其实用性和可追溯性。
## 常见问题解答
### 我可以将自定义元数据字段添加到我的 PDF 文档中吗？
是的，您可以通过使用 GroupDocs.Signature for .NET 指定字段名称及其相应值来添加自定义元数据字段。
### GroupDocs.Signature for .NET 是否与所有版本的 .NET Framework 兼容？
GroupDocs.Signature for .NET 与各种版本的 .NET Framework 兼容，确保灵活性和易于集成。
### GroupDocs.Signature 是否支持签署除 PDF 之外的其他文档格式？
是的，GroupDocs.Signature 支持多种文档格式，包括 Word、Excel、PowerPoint 等。
### 我可以使用 GroupDocs.Signature for .NET 批量签署多个文档吗？
是的，您可以通过迭代文件列表并以编程方式应用签名过程来批量签署多个文档。
### GroupDocs.Signature 用户可以获得技术支持吗？
是的，GroupDocs 通过其论坛提供专门的技术支持。您可以访问支持论坛[这里](https://forum.groupdocs.com/c/signature/13).