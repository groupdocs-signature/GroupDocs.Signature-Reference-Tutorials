---
title: 验证数字签名
linktitle: 验证数字签名
second_title: GroupDocs.Signature .NET API
description: 使用 GroupDocs.Signature 轻松验证 .NET 中的数字签名。轻松确保文件的真实性和完整性。
weight: 11
url: /zh/net/verify-operations/verify-digital/
---
## 介绍
在数字文档领域，确保真实性和完整性至关重要。数字签名相当于手写签名的数字形式，提供了一种验证电子文档的来源和完整性的安全方法。 GroupDocs.Signature for .NET 提供了一个强大的工具包，用于在 .NET 应用程序中处理数字签名，从而轻松地促进数字签名的验证。
## 先决条件
在深入使用 GroupDocs.Signature for .NET 进行验证过程之前，请确保满足以下先决条件：
### 1. 安装 .NET 的 GroupDocs.Signature
首先，下载并安装适用于 .NET 的 GroupDocs.Signature。你可以找到下载链接[这里](https://releases.groupdocs.com/signature/net/).
### 2. 获取数字签名文件
您需要一个数字签名文件（例如，YourSignature.pfx）用于验证目的。确保您有权访问该文件及其关联的密码。

## 导入命名空间
在您的 .NET 项目中，导入必要的命名空间以利用 GroupDocs.Signature 功能。

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1.指定文档路径
```csharp
string filePath = "sample_multiple_signatures.docx";
```
指定要验证的文档的路径。
## 2. 初始化签名对象
```csharp
using (Signature signature = new Signature(filePath))
```
通过将文档路径作为参数传递来创建新的 Signature 对象。
## 3. 设置验证选项
```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",
    Password = "1234567890"
};
```
创建 DigitalVerifyOptions 对象，指定数字签名文件（例如 YourSignature.pfx）的路径，以及任何其他选项，例如联系信息和密码。
## 4. 验证签名
```csharp
VerificationResult result = signature.Verify(options);
```
调用 Signature 对象上的 verify 方法，传递验证选项。
## 5. 处理验证结果
```csharp
if (result.IsValid)
{
    //找到有效签名
    foreach (DigitalSignature item in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature is found.");
    }
}
else
{
    //验证失败
    Helper.WriteError($"\nDocument {filePath} failed verification process.");
}
```
检查验证结果是否有效。如果有效，则遍历成功签名的列表。否则，处理验证失败。

## 结论
总之，GroupDocs.Signature for .NET 简化了在 .NET 应用程序中验证数字签名的过程。通过遵循上述分步指南并利用 GroupDocs.Signature 的强大功能，您可以放心地确保数字文档的真实性和完整性。
## 常见问题解答
### GroupDocs.Signature 可以验证单个文档中的多个签名吗？
是的，GroupDocs.Signature 支持在单个文档中验证多个签名，提供全面的验证功能。
### GroupDocs.Signature 是否与不同类型的数字签名文件兼容？
GroupDocs.Signature 支持各种数字签名文件格式，包括 PFX、P12 等，确保验证过程的灵活性。
### 我可以在验证过程中自定义验证选项，例如联系信息吗？
是的，GroupDocs.Signature 允许自定义验证选项，使用户能够根据需要指定联系信息、密码和其他参数。
### GroupDocs.Signature 是否提供故障排除和帮助支持？
是的，GroupDocs.Signature 通过其论坛提供专门支持，用户可以在其中寻求帮助、分享见解并有效地解决问题。
### GroupDocs.Signature 是否有试用版？
是的，感兴趣的用户可以访问 GroupDocs.Signature 的免费试用版，在做出购买决定之前探索其特性和功能。