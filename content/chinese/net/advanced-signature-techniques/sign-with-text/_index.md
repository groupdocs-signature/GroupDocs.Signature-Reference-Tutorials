---
title: 使用 GroupDocs.Signature for .NET 进行文本签名
linktitle: 用文字签名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 对带有文本的文档进行签名。以编程方式添加文本签名的分步指南。
weight: 17
url: /zh/net/advanced-signature-techniques/sign-with-text/
---
## 介绍
在数字时代，电子签名文档已成为一种标准做法，节省了时间和资源。 GroupDocs.Signature for .NET 提供了一个全面的解决方案，用于以编程方式将文本签名添加到各种文档格式。在本教程中，我们将引导您完成使用 GroupDocs.Signature for .NET 对文本文档进行签名的过程。
## 先决条件
在我们深入学习本教程之前，请确保您具备以下先决条件：
1.  GroupDocs.Signature for .NET：确保您已安装 GroupDocs.Signature for .NET 库。您可以从以下位置下载：[这里](https://releases.groupdocs.com/signature/net/).
2. 开发环境：为.NET 开发设置工作环境。
3. 文档：准备要使用文本签名的文档（例如 PDF、Word）。

## 导入命名空间
首先，您需要将必要的命名空间导入到 .NET 项目中才能使用 GroupDocs.Signature 功能。
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

让我们将使用文本签署文档的过程分解为多个步骤：
## 第 1 步：加载文档
加载您要使用文本签名的文档。
```csharp
string filePath = "sample.pdf"; //文档的路径
string fileName = Path.GetFileName(filePath);
```
## 第2步：设置输出文件路径
定义保存签名文档的输出文件路径。
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithText", fileName);
```
## 第 3 步：创建签名选项
设置文本签名的选项，包括文本内容、位置、大小、颜色和字体。
```csharp
TextSignOptions options = new TextSignOptions("John Smith")
{
    Left = 50, //设置签名位置
    Top = 200,
    Width = 100, //设置签名矩形
    Height = 30,
    ForeColor = Color.Red, //设置文字颜色
    Font = new SignatureFont { Size = 14, FamilyName = "Comic Sans MS" } //设置字体
};
```
## 第 4 步：签署文件
使用 GroupDocs.Signature 使用指定选项对文档进行签名，并将签名的文档保存到输出文件路径。
```csharp
using (Signature signature = new Signature(filePath))
{
    SignResult result = signature.Sign(outputFilePath, options); //签署文件
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## 结论
在本教程中，我们学习了如何使用 GroupDocs.Signature for .NET 对包含文本的文档进行签名。通过执行这些步骤，您可以以编程方式高效地将文本签名添加到文档中，从而增强安全性和真实性。
## 常见问题解答
### 我可以自定义文本签名的外观吗？
是的，您可以根据您的喜好自定义文本签名的颜色、字体、大小和位置等各种参数。
### GroupDocs.Signature 是否与多种文档格式兼容？
是的，GroupDocs.Signature 支持各种文档格式，包括 PDF、Word、Excel、PowerPoint 等。
### 我可以在单个文档中添加多个文本签名吗？
当然，您可以向文档添加多个文本签名，每个签名都有自己的一组自定义选项。
### GroupDocs.Signature 是否确保签名后文档的完整性？
是的，GroupDocs.Signature 采用强大的加密算法来确保文档完整性并防止签名后被篡改。
### 购买前是否有试用版可供测试？
是的，您可以从以下位置下载免费试用版[这里](https://releases.groupdocs.com/)在购买前探索功能。