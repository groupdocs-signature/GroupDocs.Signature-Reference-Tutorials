---
title: 从文档中删除多个签名
linktitle: 从文档中删除多个签名
second_title: GroupDocs.Signature .NET API
description: 使用 GroupDocs.Signature for .NET 轻松删除文档中的多个签名。简化您的文档管理工作流程。
weight: 15
url: /zh/net/delete-operations/delete-multiple-signatures/
---

# 从文档中删除多个签名

## 介绍
在数字世界中，文档管理通常涉及处理各种签名。以编程方式从文档中删除多个签名可以简化工作流程并提高效率。借助 GroupDocs.Signature for .NET，此任务变得无缝且简单。本教程将指导您逐步完成从文档中删除多个签名的过程。
## 先决条件
在深入学习本教程之前，请确保您满足以下先决条件：
- 对 C# 编程语言有基本了解。
- 为 .NET 库安装了 GroupDocs.Signature。
- 用于测试的具有多个签名的示例文档。

## 导入命名空间
首先导入必要的命名空间以访问 GroupDocs.Signature for .NET 的功能：
```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：定义文档路径和文件名
设置包含多个签名的文档的文件路径。确保您具有适当的文件路径和文件名：
```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```
## 第 2 步：复制文件进行处理
为了避免修改原始文档，请创建一个副本进行处理：
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "DeleteMultiple", fileName);
File.Copy(filePath, outputFilePath, true);
```
## 第三步：初始化签名对象
使用输出文件路径实例化 Signature 对象：
```csharp
using (Signature signature = new Signature(outputFilePath))
{
    //签名处理代码放在这里
}
```
## 第 4 步：定义搜索选项
定义各种搜索选项来识别文档中的签名。选项包括文本搜索、图像搜索、条形码搜索和二维码搜索：
```csharp
TextSearchOptions textSearchOptions = new TextSearchOptions();
ImageSearchOptions imageSearchOptions = new ImageSearchOptions();
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions();
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions();
//将选项添加到列表
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textSearchOptions);
listOptions.Add(imageSearchOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
```
## 第 5 步：搜索签名
执行搜索操作，根据定义的搜索选项查找文档中的所有签名：
```csharp
SearchResult result = signature.Search(listOptions);
```
## 第6步：删除签名
如果找到签名，请继续删除它们：
```csharp
if (result.Signatures.Count > 0)
{
    //尝试删除所有签名
    DeleteResult deleteResult = signature.Delete(result.Signatures);
    //检查是否删除成功
    if(deleteResult.Succeeded.Count == result.Signatures.Count)
    {
        Console.WriteLine("\nAll signatures were successfully deleted!");                        
    }
    else
    {
        Console.WriteLine($"Successfully deleted signatures : {deleteResult.Succeeded.Count}");
        Helper.WriteError($"Not deleted signatures : {deleteResult.Failed.Count}");
    }
    //显示有关已删除签名的信息
    Console.WriteLine("\nList of deleted signatures:");
    int number = 1;
    foreach(BaseSignature temp in deleteResult.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## 结论
以编程方式从文档中删除多个签名是文档管理中的一项关键任务。借助 GroupDocs.Signature for .NET，此过程变得高效且可靠。通过遵循本教程中概述的步骤，您可以轻松地将签名删除功能集成到您的 .NET 应用程序中。
## 常见问题解答
### GroupDocs.Signature for .NET 可以处理各种文档格式吗？
是的，GroupDocs.Signature for .NET 支持多种文档格式，包括 DOCX、PDF、PPTX、XLSX 等。
### 是否可以自定义签名检测的搜索选项？
当然，您可以定制文本搜索、图像搜索、条形码搜索和二维码搜索等搜索选项来满足您的特定要求。
### GroupDocs.Signature for .NET 是否提供错误处理机制？
是的，该库提供强大的错误处理功能，以确保文档处理任务的顺利执行。
### 我可以将 GroupDocs.Signature for .NET 与其他第三方库集成吗？
当然，GroupDocs.Signature for .NET 旨在与其他 .NET 库无缝集成，提供灵活性和可扩展性。
### 在哪里可以找到针对 .NET 的 GroupDocs.Signature 的其他支持和资源？
您可以访问 GroupDocs[论坛](https://forum.groupdocs.com/c/signature/13)致力于签名相关的讨论并寻求社区和专家的帮助。