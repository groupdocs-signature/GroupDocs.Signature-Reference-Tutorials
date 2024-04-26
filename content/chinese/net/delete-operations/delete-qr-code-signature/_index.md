---
title: 从文档中删除二维码签名
linktitle: 从文档中删除二维码签名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 从文档中删除 QR 代码签名。请按照我们的分步指南进行高效的签名管理。
type: docs
weight: 16
url: /zh/net/delete-operations/delete-qr-code-signature/
---
## 介绍
在本教程中，我们将指导您完成使用 GroupDocs.Signature for .NET 从文档中删除 QR 代码签名的过程。按照这些分步说明有效删除 QR 码签名。
## 先决条件
在开始之前，请确保您具备以下先决条件：
- 适用于 .NET 的 GroupDocs.Signature：确保您的 .NET 项目中安装了 GroupDocs.Signature 库。您可以从以下位置下载：[这里](https://releases.groupdocs.com/signature/net/).
- 带有二维码签名的文档：准备包含要删除的二维码签名的文档。
- C# 基础知识：熟悉 C# 编程语言基础知识。

## 导入命名空间
在深入研究代码之前，将必要的命名空间导入到您的 C# 文件中：
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 步骤 1：定义文件路径
```csharp
//文档目录的路径。
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
//定义修改后的文档的输出文件路径。
string outputFilePath = Path.Combine("Your Document Directory", "DeleteQRCode", fileName);
//复制源文件，因为删除方法适用于同一文档。
File.Copy(filePath, outputFilePath, true);
```
## 第2步：初始化签名对象
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    //创建用于搜索 QR 码签名的选项。
    QrCodeSearchOptions options = new QrCodeSearchOptions();
    //在文档中搜索二维码签名。
    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);
```
## 步骤 3：检查二维码签名是否存在
```csharp
    if (signatures.Count > 0)
    {
        //获取文档中找到的第一个二维码签名。
        QrCodeSignature qrCodeSignature = signatures[0];
```
## 第四步：删除二维码签名
```csharp
        //从文档中删除 QR 码签名。
        bool result = signature.Delete(qrCodeSignature);
        if (result)
        {
            Console.WriteLine($"Signature with QR-Code '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was deleted from document ['{fileName}'].");
        }
        else
        {
            Helper.WriteError($"Signature was not deleted from the document! Signature with Barcode '{qrCodeSignature.Text}' and encode type '{qrCodeSignature.EncodeType.TypeName}' was not found!");
        }
    }
}
```
恭喜！您已使用 GroupDocs.Signature for .NET 成功从文档中删除了 QR 代码签名。

## 结论
在本教程中，我们学习了如何使用 GroupDocs.Signature for .NET 从文档中删除 QR 码签名。通过遵循提供的步骤，您可以有效地管理和操作 .NET 应用程序中的签名。
## 常见问题解答
### 我可以从文档中删除多个二维码签名吗？
是的，您可以修改代码以迭代所有二维码签名并相应地删除它们。
### GroupDocs.Signature是否支持除二维码之外的其他类型签名？
是的，GroupDocs.Signature 支持各种签名类型，例如文本、图像、条形码等。
### GroupDocs.Signature 是否与所有文档格式兼容？
GroupDocs.Signature 支持多种文档格式，包括 PDF、Microsoft Word、Excel、PowerPoint 等。
### 我可以自定义签名的搜索选项吗？
是的，您可以根据您的要求定制搜索选项，以查找文档中的特定签名。
### GroupDocs.Signature 是否有试用版？
是的，您可以访问 GroupDocs.Signature 的免费试用版：[这里](https://releases.groupdocs.com/).