---
title: 检索文档信息
linktitle: 检索文档信息
second_title: GroupDocs.Signature .NET API
description: 使用 GroupDocs.Signature 增强 .NET 中的文档管理。逐步检索文档信息。支持各种格式。
weight: 11
url: /zh/net/document-preview-operations/retrieve-document-information/
---
## 介绍
在数字文档领域，确保真实性和完整性至关重要。 GroupDocs.Signature for .NET 提供了一个强大的解决方案，用于在 .NET 环境中管理文档签名。在本教程中，我们将深入研究使用 GroupDocs.Signature for .NET 检索文档信息的过程，分解每个步骤以便全面理解。
## 先决条件
在深入学习本教程之前，请确保您具备以下先决条件：
1. 安装：通过下载安装 GroupDocs.Signature for .NET[这里](https://releases.groupdocs.com/signature/net/).
2. .NET 环境：具备 .NET 框架的应用知识。
3. 文档：准备样本文档（例如“sample_multiple_signatures.docx”）以用于测试目的。

## 导入命名空间
在继续文档签名检索过程之前，导入必要的命名空间：
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## 步骤1：设置文档文件路径：
定义要从中检索信息的文档的文件路径。
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## 第2步：实例化签名对象：
创建一个实例`Signature`类通过传递文档文件路径。
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## 步骤 3：检索文档信息：
利用`GetDocumentInfo()`获取有关文档的全面信息的方法。
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## 步骤 4：显示文档属性：
输出文档的各种属性，例如格式、扩展名、大小、页数等。
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## 结论
GroupDocs.Signature for .NET 提供了一套功能强大的工具，用于在 .NET 框架内无缝管理文档签名。通过遵循本指南中概述的步骤，您可以有效地检索有关文档的全面信息，从而增强文档管理功能。

## 常见问题解答
### GroupDocs.Signature for .NET 可以处理多种文档格式吗？
是的，GroupDocs.Signature 支持多种文档格式，包括但不限于 DOCX、PDF、PNG 和 JPEG。
### GroupDocs.Signature for .NET 有试用版吗？
是的，您可以访问试用版[这里](https://releases.groupdocs.com/).
### GroupDocs.Signature for .NET 是否提供对数字签名的支持？
当然，GroupDocs.Signature 为数字签名提供强大的支持，确保文档的真实性和完整性。
### 在哪里可以找到针对 .NET 的 GroupDocs.Signature 的其他文档和支持？
您可以参考综合文档[这里](https://tutorials.groupdocs.com/signature/net/)，如需支持，请访问 GroupDocs 论坛[这里](https://forum.groupdocs.com/c/signature/13).
### 能否为 .NET 获得 GroupDocs.Signature 的临时许可证？
是的，可以购买临时许可证[这里](https://purchase.groupdocs.com/temporary-license/).