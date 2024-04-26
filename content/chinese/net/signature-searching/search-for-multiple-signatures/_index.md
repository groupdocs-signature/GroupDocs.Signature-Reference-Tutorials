---
title: 搜索多重签名
linktitle: 搜索多重签名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature 在 .NET 文档中搜索多个签名，以实现高效的文档安全性和完整性。
type: docs
weight: 14
url: /zh/net/signature-searching/search-for-multiple-signatures/
---
## 介绍
GroupDocs.Signature for .NET 是一个功能强大的库，使开发人员能够使用 .NET 应用程序添加、搜索和删除流行文档格式中的各种类型的签名。在本教程中，我们将重点介绍使用 GroupDocs.Signature for .NET 在文档中搜索多个签名。
## 先决条件
在我们开始之前，请确保您具备以下先决条件：
- Visual Studio 安装在您的系统上。
- 对 C# 编程语言有基本了解。
- 项目中安装的 .NET 库的 GroupDocs.Signature。您可以从以下位置下载：[这里](https://releases.groupdocs.com/signature/net/).

## 导入命名空间
首先，您需要导入必要的命名空间来访问 GroupDocs.Signature for .NET 提供的类和方法。
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：加载文档
将文档加载到要搜索多个签名的位置。确保您提供正确的文件路径。
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    //你的代码放在这里
}
```
## 第 2 步：定义搜索选项
定义各种类型签名的搜索选项，例如文本、数字、条形码、二维码和元数据。您可以指定搜索条件，例如要匹配的文本、匹配类型以及跨所有页面进行搜索。
```csharp
//定义搜索选项
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## 第 3 步：将搜索选项添加到列表中
将定义的搜索选项添加到列表中。
```csharp
//将选项添加到列表
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## 第 4 步：搜索签名
使用定义的搜索选项在文档中搜索签名。
```csharp
//搜索文档中的签名
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## 结论
在本教程中，我们学习了如何使用 GroupDocs.Signature for .NET 在文档中搜索多个签名。通过遵循提供的步骤，您可以有效地找到文档中的各种类型的签名，从而增强文档的安全性和完整性。
## 常见问题解答
### 我可以搜索不同文档格式的签名吗？
是的，GroupDocs.Signature for .NET 支持多种文档格式，包括 Word、PDF、Excel 等。
### 是否可以自定义签名的搜索条件？
当然，您可以根据您的要求定制搜索条件，例如指定精确的文本匹配或跨所有页面搜索。
### GroupDocs.Signature for .NET 是否提供数字签名支持？
是的，您可以搜索数字签名以及文本、条形码和二维码签名等其他类型。
### 我可以轻松地将签名搜索功能集成到我的 .NET 应用程序中吗？
是的，GroupDocs.Signature for .NET 提供了一个简单的 API，简化了集成过程。
### 我可以在哪里找到额外的支持或帮助？
您可以访问 GroupDocs.Signature 论坛[这里](https://forum.groupdocs.com/c/signature/13)如有任何疑问或需要帮助。