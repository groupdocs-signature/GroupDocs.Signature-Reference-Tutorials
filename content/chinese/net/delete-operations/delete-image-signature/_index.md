---
title: 删除图像签名
linktitle: 删除图像签名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 从文档中删除图像签名。按照我们的分步指南进行有效的签名管理。
weight: 14
url: /zh/net/delete-operations/delete-image-signature/
---
## 介绍
在本教程中，我们将探讨如何使用 GroupDocs.Signature for .NET 从文档中删除图像签名。GroupDocs.Signature 是一个功能强大的库，允许开发人员处理各种文档格式中的数字签名、印章和表单字段。
## 先决条件
在开始之前，请确保您已准备好以下物品：
### 1. 适用于 .NET 的 GroupDocs.Signature
从以下位置下载并安装 GroupDocs.Signature for .NET[网站](https://releases.groupdocs.com/signature/net/). 按照文档中提供的安装说明进行操作。
### 2. .NET 框架
确保您的机器上安装了.NET Framework。
## 导入命名空间
在您的项目中包含必要的命名空间：
```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
我们将删除图像签名的过程分解为多个步骤：
## 步骤 1：定义文件路径
首先指定输入文档和删除签名后的输出文档的路径：
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteImage", fileName);
```
## 第2步：复制源文件
自从`Delete`方法适用于同一文档，必须将源文件复制到另一个位置：
```csharp
File.Copy(filePath, outputFilePath, true);
```
## 第三步：初始化签名对象
创建一个实例`Signature`类并指定输出文档的路径：
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    //代码放在这里
}
```
## 第 4 步：搜索图像签名
定义搜索选项并在文档中搜索图像签名：
```csharp
ImageSearchOptions options = new ImageSearchOptions();
List<ImageSignature> signatures = signature.Search<ImageSignature>(options);
```
## 第5步：删除图像签名
如果找到图像签名，则删除第一个：
```csharp
if (signatures.Count > 0)
{
    ImageSignature imageSignature = signatures[0];
    bool result = signature.Delete(imageSignature);
    if (result)
    {
        Console.WriteLine($"Image signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature at location {imageSignature.Left}x{imageSignature.Top} and Size {imageSignature.Size} was not found!");
    }
}
```
## 结论
在本教程中，我们学习了如何使用 GroupDocs.Signature for .NET 从文档中删除图像签名。通过遵循分步指南，开发人员可以有效地管理其应用程序中的数字签名。
## 常见问题解答
### 我可以从文档中删除多个图像签名吗？
是的，您可以修改代码以通过迭代来删除多个图像签名`signatures`列表。
### GroupDocs.Signature 是否支持除 DOCX 之外的其他文档格式？
是的，GroupDocs.Signature 支持多种文档格式，包括 PDF、PPT、XLS 等。
### GroupDocs.Signature for .NET 有试用版吗？
是的，您可以从以下位置下载免费试用版[网站](https://releases.groupdocs.com/).
### 我如何获得对 GroupDocs.Signature 的支持？
您可以访问[GroupDocs.Signature 论坛](https://forum.groupdocs.com/c/signature/13)寻求帮助和支持。
### 我可以购买 GroupDocs.Signature 的临时许可证吗？
是的，您可以从[购买页面](https://purchase.groupdocs.com/temporary-license/).