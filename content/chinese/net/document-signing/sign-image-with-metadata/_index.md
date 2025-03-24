---
title: 使用元数据对图像进行签名
linktitle: 使用元数据对图像进行签名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature 在 .NET 中使用元数据对图像进行签名。简单、高效且可定制的元数据签名解决方案。
weight: 10
url: /zh/net/document-signing/sign-image-with-metadata/
---
## 介绍
GroupDocs.Signature for .NET 使开发人员能够有效地使用元数据对图像进行签名。本教程将引导您逐步完成该过程。
## 先决条件
在开始之前，请确保您具备以下条件：
1. GroupDocs.Signature for .NET：在您的 .NET 项目中安装 GroupDocs.Signature 包。您可以从以下位置下载[这里](https://releases.groupdocs.com/signature/net/).   
2. 图像文件：准备要用元数据签名的图像文件。

## 导入命名空间
确保在 C# 代码中导入必要的命名空间：
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 步骤 1：加载图像文件
首先，指定图像文件的路径以及带有元数据的签名图像的输出目录：
```csharp
string filePath = "sample.png";            
string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
```
## 第 2 步：创建元数据签名
接下来创建不同的元数据签名，并添加到选项签名集合中：
```csharp
using (Signature signature = new Signature(filePath))
{
    ushort imgsMetadataId = 41996;
    MetadataSignOptions options = new MetadataSignOptions();
    options
        .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Scherlock Holmes")) //字符串值
        .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          //日期时间值
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                //整数值
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              //双倍值
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              //十进制值
        .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             //浮点值
    
    //签署文件以归档
    SignResult result = signature.Sign(outputFilePath, options);
    Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
}
```

## 结论
在本教程中，您学习了如何使用 GroupDocs.Signature for .NET 对带有元数据的图像进行签名。通过遵循这些步骤，您可以轻松地将元数据签名合并到您的 .NET 应用程序中。

## 常见问题解答
### 我可以使用 GroupDocs.Signature for .NET 对多个图像进行元数据签名吗？
是的，您可以通过迭代每个图像文件并应用元数据签名来使用元数据对多个图像进行签名。
### GroupDocs.Signature for .NET 有试用版吗？
是的，您可以从以下位置下载试用版[这里](https://releases.groupdocs.com/).
### GroupDocs.Signature for .NET 是否支持除图像之外的其他文件格式？
是的，GroupDocs.Signature 支持各种文件格式，包括 PDF、Word、Excel 等。
### 我可以自定义元数据签名的外观吗？
是的，您可以自定义元数据签名的外观，例如字体大小、颜色和位置。
### 在哪里可以获得对 .NET 的 GroupDocs.Signature 的支持？
您可以从 GroupDocs.Signature 论坛获得支持[这里](https://forum.groupdocs.com/c/signature/13).