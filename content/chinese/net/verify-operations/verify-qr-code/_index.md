---
title: 验证二维码
linktitle: 验证二维码
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 验证文档中的 QR 码。带有分步指南的综合教程。
weight: 12
url: /zh/net/verify-operations/verify-qr-code/
---
## 介绍
在文档管理和身份验证领域，确保签名的完整性和有效性至关重要。 GroupDocs.Signature for .NET 提供了用于验证文档中嵌入的 QR 代码的全面解决方案。在本教程中，我们将深入研究使用 GroupDocs.Signature for .NET 验证 QR 码的分步过程。
## 先决条件
在深入验证过程之前，请确保满足以下先决条件：
1. 安装 GroupDocs.Signature for .NET：从以下位置下载并安装 GroupDocs.Signature for .NET[下载链接](https://releases.groupdocs.com/signature/net/).
2. 访问包含 QR 码的文档：准备包含 QR 码的示例文档以进行验证。 

## 导入命名空间
首先，您需要导入必要的命名空间以利用 GroupDocs.Signature for .NET 提供的功能。按着这些次序：

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


现在，让我们分解一下使用 GroupDocs.Signature for .NET 验证文档中嵌入的二维码的过程：
## 第1步：指定文档路径
```csharp
string filePath = "sample_multiple_signatures.docx";
```
确保更换`"sample_multiple_signatures.docx"`以及您的文档的路径。
## 第2步：初始化签名对象
```csharp
using (Signature signature = new Signature(filePath))
{
    //验证码在这里
}
```
初始化一个`Signature`对象通过提供文档的路径。
## 步骤 3：指定验证选项
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, //该值是默认设置的
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
定义验证选项，例如`AllPages`验证所有页面，`Text`指定 QR 码中要匹配的文本，以及`MatchType`定义匹配标准。
## 第 4 步：验证文档签名
```csharp
VerificationResult result = signature.Verify(options);
```
调用`Verify`的方法`Signature`对象，传递验证选项。
## 第5步：处理验证结果
```csharp
if (result.IsValid)
{
    //找到有效签名
}
else
{
    //发现无效签名
}
```
根据验证结果，对成功或失败的场景进行相应的处理。

## 结论
在本教程中，我们探索了使用 GroupDocs.Signature for .NET 验证文档中的 QR 码的过程。通过执行这些步骤，您可以将 QR 码验证功能无缝集成到您的 .NET 应用程序中，从而确保文档的完整性和真实性。
## 常见问题解答
### GroupDocs.Signature for .NET 可以跨不同文档格式验证 QR 码吗？
是的，GroupDocs.Signature for .NET 支持多种文档格式，包括 DOCX、PDF 以及更多用于二维码验证的格式。
### GroupDocs.Signature for .NET 是否有免费试用版？
是的，你可以免费试用[发布页面](https://releases.groupdocs.com/).
### GroupDocs.Signature 为 .NET 用户提供哪些支持选项？
用户可以通过以下方式获得支持[论坛](https://forum.groupdocs.com/c/signature/13)用于 GroupDocs.Signature。
### 我可以购买 GroupDocs.Signature for .NET 的临时许可证吗？
是的，可以从[GroupDocs 购买页面](https://purchase.groupdocs.com/temporary-license/).
### 是否有关于 GroupDocs.Signature for .NET 的详尽文档？
当然，你可以参考提供的详细文档[这里](https://tutorials.groupdocs.com/signature/net/)提供有关如何利用 GroupDocs.Signature for .NET 功能的全面指导。