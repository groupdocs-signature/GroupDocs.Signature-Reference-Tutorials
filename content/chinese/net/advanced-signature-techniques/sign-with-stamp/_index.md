---
title: 使用 GroupDocs.Signature 进行 Stamp 签名
linktitle: 盖章签名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 轻松将图章签名添加到 .NET 文档中。增强文档安全性。
type: docs
weight: 16
url: /zh/net/advanced-signature-techniques/sign-with-stamp/
---
## 介绍
在本教程中，我们将引导您完成使用 GroupDocs.Signature for .NET 使用图章签署文档的过程。通过遵循这些分步说明，您将能够轻松地在文档中添加印章签名。
## 先决条件
在我们开始之前，请确保您满足以下先决条件：
1.  GroupDocs.Signature for .NET SDK：从以下位置下载并安装 SDK：[网站](https://releases.groupdocs.com/signature/net/).
2. 开发环境：确保您为 .NET 开发设置了合适的开发环境。
3. 要签名的文档：准备您要盖章签名的文档（例如 PDF）。

## 导入命名空间
首先将必要的命名空间导入到您的项目中：
```csharp
using System;
using System.IO;
using System.Drawing;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：加载文档
```csharp
string filePath = "sample.pdf";
using (Signature signature = new Signature(filePath))
{
    //你的代码放在这里
}
```
## 第 2 步：设置图章标志选项
```csharp
StampSignOptions options = new StampSignOptions()
{
    Left = 50,
    Top = 150,                    
    Width = 200,
    Height = 200
};
```
## 步骤 3：配置图章外观
```csharp
StampLine outerLine = new StampLine();
outerLine.Text = " * European Union ";
outerLine.TextRepeatType = StampTextRepeatType.FullTextRepeat;
outerLine.Font.Size = 12;
outerLine.Height = 22;
outerLine.TextBottomIntent = 6;
outerLine.TextColor = Color.WhiteSmoke;
outerLine.BackgroundColor = Color.DarkSlateBlue;
options.OuterLines.Add(outerLine);
StampLine innerLine = new StampLine();
innerLine.Text = "John Smith";
innerLine.TextColor = Color.MediumVioletRed;
innerLine.Font.Size = 20;
innerLine.Font.Bold = true;
innerLine.Height = 40;
options.InnerLines.Add(innerLine);
```
## 第 4 步：签署文件
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignWithStamp", fileName);
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 结论
使用 GroupDocs.Signature for .NET 将图章签名添加到文档中是一个简单的过程，如本教程中所示。通过提供的步骤，您可以轻松增强文档的安全性和真实性。
## 常见问题解答
### 我可以自定义印章签名的外观吗？
是的，您可以根据您的要求定制印章签名的文本、字体、颜色和位置等各个方面。
### GroupDocs.Signature 是否支持签署多种文档格式？
是的，GroupDocs.Signature 支持多种文档格式，包括 PDF、Microsoft Word、Excel、PowerPoint 等。
### GroupDocs.Signature 是否有试用版？
是的，您可以从以下位置访问免费试用版：[网站](https://releases.groupdocs.com/).
### 我可以在单个文档中添加多个签名吗？
当然，GroupDocs.Signature 允许您向单个文档添加多个签名，包括图章、文本、图像和数字签名。
### 如果在实施过程中遇到任何问题，我可以在哪里寻求支持？
您可以从 GroupDocs.Signature 社区论坛找到支持和帮助[这里](https://forum.groupdocs.com/c/signature/13).