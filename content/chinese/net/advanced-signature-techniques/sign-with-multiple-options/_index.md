---
title: 使用多个选项进行签名
linktitle: 使用多个选项进行签名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 通过多个选项签署文档。通过文本、条形码、QR 码、数字和图像增强文档安全性。
type: docs
weight: 14
url: /zh/net/advanced-signature-techniques/sign-with-multiple-options/
---
## 介绍
在本教程中，我们将探讨如何使用 .NET 的 GroupDocs.Signature 库使用多个签名选项对文档进行签名。使用文本、条形码、二维码、数字、图像和元数据签名等各种选项对文档进行签名可以提供多功能性并增强文档安全性。
## 先决条件
在开始之前，请确保您具备以下先决条件：
1.  GroupDocs.Signature for .NET 库：从以下位置下载并安装 GroupDocs.Signature for .NET 库[这里](https://releases.groupdocs.com/signature/net/).
2. 开发环境：搭建开发环境，安装.NET Framework。
3. 要签名的文档：准备您要签名的文档（例如，sample.docx）。
4. 证书和图像：准备数字和图像签名所需的任何证书和图像。

## 导入命名空间
首先，导入必要的命名空间以在 .NET 应用程序中使用 GroupDocs.Signature 库：
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：加载文档
```csharp
string filePath = "sample.docx";
string outputFilePath = Path.Combine("Your Document Directory", "SignWithMultiple", "SignWithMultiple.docx");
using (Signature signature = new Signature(filePath))
{
    //您的代码继续...
}
```
## 第 2 步：定义签名选项
定义多个不同类型和设置的签名选项，例如文本、条形码、QR 码、数字、图像和元数据签名：
```csharp
TextSignOptions textOptions = new TextSignOptions("Text signature")
{
    VerticalAlignment = VerticalAlignment.Top,
    HorizontalAlignment = HorizontalAlignment.Left
};
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456")
{
    EncodeType = BarcodeTypes.Code128,
    Left = 0,
    Top = 150,
    Height = 50,
    Width = 200
};
//定义其他签名选项（例如，QR 码、数字、图像、元数据）...
```
## 第 3 步：创建签名选项列表
定义包含所有先前定义的选项的签名选项列表：
```csharp
List<SignOptions> listOptions = new List<SignOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
//将其他签名选项添加到列表中...
```
## 第 4 步：签署文件
使用签名选项列表对文档进行签名并保存签名的文档：
```csharp
SignResult result = signature.Sign(outputFilePath, listOptions);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 结论
使用 GroupDocs.Signature for .NET 使用多个选项对文档进行签名，为增强文档安全性和多功能性提供了强大的解决方案。通过遵循本教程中概述的步骤，您可以将各种签名类型无缝集成到您的 .NET 应用程序中。
## 常见问题解答
### 我可以使用自定义图像进行数字签名吗？
是的，您可以使用 GroupDocs.Signature 库为数字签名指定自定义图像。
### GroupDocs.Signature 是否与不同的文档格式兼容？
是的，GroupDocs.Signature 支持各种文档格式，包括 DOCX、PDF、PPTX 等。
### 我可以自定义文本签名的外观吗？
当然，您可以自定义文本签名的外观，包括字体大小、颜色和样式。
### GroupDocs.Signature 是否提供数字签名加密？
是的，GroupDocs.Signature 提供数字签名加密选项，以确保文档安全。
### GroupDocs.Signature for .NET 有试用版吗？
是的，您可以从以下网址下载 GroupDocs.Signature for .NET 的免费试用版[这里](https://releases.groupdocs.com/).