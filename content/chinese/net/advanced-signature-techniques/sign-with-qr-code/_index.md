---
title: 使用 GroupDocs.Signature 通过 QR 码签署文档
linktitle: 使用二维码签名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 将 QR 代码签名添加到文档中。轻松增强安全性和身份验证。
weight: 15
url: /zh/net/advanced-signature-techniques/sign-with-qr-code/
---
## 介绍
在本教程中，我们将介绍使用 GroupDocs.Signature for .NET 使用二维码签署文档的过程。GroupDocs.Signature for .NET 是一个功能强大的 API，允许开发人员以编程方式向数字文档添加各种类型的签名。使用二维码签署文档可以为您的文档提供额外的安全性和身份验证。
## 先决条件
在开始之前，请确保您已安装以下先决条件：
1.  GroupDocs.Signature for .NET：您可以从[网站](https://releases.groupdocs.com/signature/net/).
2. 开发环境：确保您的机器上已设置 .NET 开发环境。
3. 示例文档：准备您想要使用二维码签名的示例文档（例如 PDF）。

## 导入必要的命名空间
在深入研究代码之前，让我们导入必要的命名空间：
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## 步骤 1：定义文件路径
```csharp
string filePath = "sample.pdf";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "SignWithQRCode", fileName);
```
确保更换`"Your Document Directory"`使用您想要保存签名文档的目录路径。
## 第2步：初始化签名对象
```csharp
using (Signature signature = new Signature(filePath))
{
    //签名代码位于此处
}
```
初始化一个`Signature`对象包含您要签名的文档的路径。
## 第3步：创建QRCodeSignOptions
```csharp
QrCodeSignOptions options = new QrCodeSignOptions("JohnSmith")
{
    EncodeType = QrCodeTypes.QR,
    Left = 50,
    Top = 150,
    Width = 200,
    Height = 200
};
```
创建一个`QrCodeSignOptions`具有 QR 码签名所需设置的对象。您可以自定义参数，例如要编码的文本、QR 码的位置和尺寸。
## 第 4 步：签署文件
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
使用`Sign`的方法`Signature`对象使用指定选项签署文档。该方法返回一个`SignResult`包含有关签名过程的信息的对象。
## 第5步：显示结果
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
显示一条消息，指示签名过程成功以及签名文档的保存位置。

## 结论
在本教程中，我们学习了如何使用 GroupDocs.Signature for .NET 通过 QR 码签署文档。通过执行这些简单的步骤，您可以将 QR 码签名添加到您的数字文档中，从而增强安全性和身份验证。

## 常见问题解答
### 我可以自定义二维码的外观吗？
是的，您可以根据您的需求自定义二维码的大小、位置、编码类型等各种参数。
### 二维码签名支持哪些文档格式？
GroupDocs.Signature for .NET 支持多种文档格式，包括 PDF、Word、Excel、PowerPoint 等。
### 是否可以批量签署多个文件？
当然，您可以使用 GroupDocs.Signature for .NET 同时签署多个文档，从而简化您的工作流程。
### 我可以验证使用二维码签名的文件的真实性吗？
是的，GroupDocs.Signature for .NET 提供验证机制来确保签名文档的完整性和真实性。
### 购买前是否有试用版来测试功能？
是的，您可以从以下位置下载免费试用版[网站](https://releases.groupdocs.com/)评估 GroupDocs.Signature for .NET 的特性和功能。