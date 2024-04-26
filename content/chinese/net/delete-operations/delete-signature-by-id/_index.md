---
title: 按 ID 删除签名
linktitle: 按 ID 删除签名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature 库按 ID 删除 .NET 文档中的签名。简单的分步指南。
type: docs
weight: 11
url: /zh/net/delete-operations/delete-signature-by-id/
---
## 介绍
在本教程中，我们将探讨如何使用 GroupDocs.Signature for .NET 按 ID 删除签名。 GroupDocs.Signature for .NET 是一个功能强大的库，允许开发人员使用 .NET 应用程序添加、删除或验证各种文档格式的数字签名。
## 先决条件
在我们开始之前，请确保您具备以下先决条件：
1.  GroupDocs.Signature for .NET Library：从以下位置下载并安装该库[这里](https://releases.groupdocs.com/signature/net/).
2. .NET Framework：确保您的系统上安装了 .NET Framework。
3. 带有签名的文档：准备带有要删除的签名的文档（例如 DOCX、PDF）。

## 导入命名空间
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 步骤 1：定义文件路径
首先，指定包含签名的文档的文件路径，以及保存修改后的文档的输出文件路径。
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteById", fileName);
```
## 第 2 步：复制文档
自从`Delete`方法就地修改文档，最好创建原始文档的副本。
```csharp
File.Copy(filePath, outputFilePath, true);
```
## 步骤3：按ID删除签名
初始化`Signature`对象与文档文件路径并使用`Delete`方法通过 ID 删除签名。
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    string id = @"eff64a14-dad9-47b0-88e5-2ee4e3604e71";
    bool result = signature.Delete(id);
    if (result)
    {
        Console.WriteLine($"Signature with Id# '{id}' was deleted from document ['{fileName}'].");
    }
    else
    {
        Helper.WriteError($"Signature was not deleted from the document! Signature with id# '{id}' was not found!");
    }
}
```

## 结论
在本教程中，我们学习了如何使用 GroupDocs.Signature for .NET 按 ID 删除签名。该库提供了一种以编程方式管理各种文档格式的数字签名的便捷方法。
## 常见问题解答
### 我可以一次删除多个签名吗？
是的，您可以通过迭代 ID 并调用`Delete`每个 ID 的方法。
### GroupDocs.Signature for .NET 是否与所有文档格式兼容？
GroupDocs.Signature for .NET 支持多种文档格式，包括 PDF、DOCX、XLSX 等。
### 我可以自定义签名的外观吗？
是的，您可以自定义签名的外观，包括其位置、大小、字体和颜色。
### 有试用版吗？
是的，您可以从以下位置下载免费试用版[这里](https://releases.groupdocs.com/).
### 在哪里可以找到 GroupDocs.Signature for .NET 的帮助或支持？
您可以访问支持论坛[这里](https://forum.groupdocs.com/c/signature/13)寻求帮助。