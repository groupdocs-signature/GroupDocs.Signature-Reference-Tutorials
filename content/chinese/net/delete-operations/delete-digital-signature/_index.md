---
title: 从文档中删除数字签名
linktitle: 从文档中删除数字签名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 从文档中删除数字签名。遵循我们的分步指南进行高效管理。
weight: 13
url: /zh/net/delete-operations/delete-digital-signature/
---

# 从文档中删除数字签名

## 介绍
在数字文档的世界中，确保真实性和安全性至关重要。数字签名在验证电子文档的完整性方面发挥着至关重要的作用。 GroupDocs.Signature for .NET 提供了强大的工具来有效管理 .NET 应用程序中的数字签名。
## 先决条件
在深入使用 GroupDocs.Signature for .NET 从文档中删除数字签名之前，请确保您具备以下条件：
1. Visual Studio：在您的系统上安装 Visual Studio IDE。
2.  GroupDocs.Signature for .NET：从[下载页面](https://releases.groupdocs.com/signature/net/).
3. 示例文档：准备包含数字签名的示例文档以进行测试。

## 导入命名空间
首先，请确保在 .NET 项目中导入必要的命名空间：
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```
## 步骤 1：定义文件路径
首先定义源文档和输出文档的文件路径：
```csharp
string filePath = "sample.pdf"_SIGNED_DIGITAL;
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteDigital", fileName);
```
## 第 2 步：复制源文档
自从`Delete`方法适用于同一文档，需要将源文件复制到新位置：
```csharp
File.Copy(filePath, outputFilePath, true);
```
## 第三步：初始化签名对象
初始化一个`Signature`具有输出文件路径的对象：
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    //你的代码放在这里
}
```
## 第 4 步：搜索数字签名
在文档中搜索电子数字签名：
```csharp
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```
## 第5步：删除数字签名
如果找到数字签名，则删除找到的第一个签名：
```csharp
if (signatures.Count > 0)
{
    DigitalSignature digitalSignature = signatures[0];
    bool result = signature.Delete(digitalSignature);
    if (result)
    {
        Console.WriteLine($"Digital signature #{digitalSignature.Thumbprint} from {digitalSignature.SignTime.ToShortDateString()} was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature# {digitalSignature.Thumbprint} was not found!");
    }
}
```

## 结论
使用 GroupDocs.Signature 可以轻松管理 .NET 应用程序中的数字签名。通过执行上述简单步骤，您可以无缝地从文档中删除数字签名，从而确保数据的完整性和安全性。
## 常见问题解答
### 我可以从单个文档中删除多个数字签名吗？
是的，您可以修改代码以迭代找到的所有数字签名并相应地删除它们。
### GroupDocs.Signature 是否支持除数字签名之外的其他类型的签名？
是的，GroupDocs.Signature 支持各种类型的签名，包括电子签名、数字签名和手写签名。
### GroupDocs.Signature适合企业级文档管理吗？
当然，GroupDocs.Signature 旨在满足个人开发人员和企业级应用程序的需求，提供强大的功能和可扩展性。
### 我可以自定义数字签名的删除流程吗？
是的，GroupDocs.Signature 提供了广泛的选项和设置，可根据您的具体要求自定义签名删除过程。
### 是否有可用于测试 GroupDocs.Signature 的试用版？
是的，您可以从以下位置下载免费试用版[发布页面](https://releases.groupdocs.com/).