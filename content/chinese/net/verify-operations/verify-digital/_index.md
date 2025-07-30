---
"description": "使用 GroupDocs.Signature 在 .NET 应用程序中实现安全的数字签名验证。提供文档身份验证的分步指南和完整的代码示例。"
"linktitle": "验证数字签名"
"second_title": "GroupDocs.签名 .NET API"
"title": "验证文档中的数字签名"
"url": "/zh/net/verify-operations/verify-digital/"
"weight": 11
---

## 介绍

在现代商业流程中，数字签名在确保文档的真实性、完整性和不可否认性方面发挥着至关重要的作用。与传统的手写签名不同，数字签名使用加密技术来验证签名者的身份，并确保文档自签名以来未被更改。

GroupDocs.Signature for .NET 提供了一个全面的工具包，使开发人员能够在其 .NET 应用程序中实现强大的数字签名验证。本详细教程将指导您完成使用 GroupDocs.Signature for .NET 验证文档中数字签名的过程。

## 先决条件

在实施数字签名验证功能之前，请确保您已满足以下先决条件：

1. GroupDocs.Signature for .NET：从以下位置下载并安装该库 [GroupDocs.Signature for .NET 版本](https://releases。groupdocs.com/signature/net/).
2. .NET 开发环境：Visual Studio 或任何兼容的 .NET 开发环境。
3. 数字证书：用于签署文档的数字证书文件（例如 .pfx）或属于受信任链的证书。
4. 待验证文件：包含需要验证的数字签名的文档。

## 导入所需的命名空间

首先导入必要的命名空间来访问 GroupDocs.Signature 功能：

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

让我们将验证数字签名的过程分解为清晰、易于管理的步骤：

## 步骤 1：指定文档路径

```csharp
// 包含数字签名的文档的路径
string filePath = "sample_multiple_signatures.docx";
```

将示例路径替换为包含数字签名的文档的实际路径。

## 步骤2：初始化签名对象

```csharp
// 通过传递文档路径创建 Signature 类的实例
using (Signature signature = new Signature(filePath))
{
    // 验证码将在此处执行
}
```

Signature 类是 GroupDocs.Signature API 中所有操作的主要入口点。

## 步骤 3：配置数字验证选项

```csharp
// 设置验证选项
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",     // 预期签名者联系方式
    Password = "1234567890",  // 如果需要，证书密码
    AllPages = true           // 检查所有页面的签名
};
```

验证选项允许您指定：
- 数字证书文件路径
- 预期签名者联系信息
- 如果证书受密码保护，则输入证书的密码
- 验证页面范围（默认为所有页面）

## 步骤4：执行验证过程

```csharp
// 执行验证
VerificationResult result = signature.Verify(options);
```

这将根据您指定的选项执行验证过程。

## 步骤5：处理验证结果

```csharp
// 查看验证结果并进行相应处理
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid digital signatures!");
    
    // 显示有效签名的详细信息
    foreach (DigitalSignature digitalSignature in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature found:");
        Console.WriteLine($"Signer: {digitalSignature.Subject}");
        Console.WriteLine($"Issuer: {digitalSignature.Issuer}");
        Console.WriteLine($"Valid From: {digitalSignature.ValidFrom}");
        Console.WriteLine($"Valid To: {digitalSignature.ValidTo}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    
    // 如果需要，显示有关失败签名的信息
    foreach (DigitalSignature failedSignature in result.Failed)
    {
        Console.WriteLine($"Failed signature reason: {failedSignature.Comments}");
    }
}
```

此代码检查验证是否成功并提供有关已验证签名的详细信息。

## 完整示例

以下是演示数字签名验证的完整工作示例：

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文档路径
            string filePath = "sample_multiple_signatures.docx";
            
            try
            {
                // 初始化签名实例
                using (Signature signature = new Signature(filePath))
                {
                    // 设置验证选项
                    DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
                    {
                        Contact = "Mr.Smith",
                        Password = "1234567890"
                    };
                    
                    // 验证文档签名
                    VerificationResult result = signature.Verify(options);
                    
                    // 工艺验证结果
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid digital signatures!");
                        
                        foreach (DigitalSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found.");
                            Console.WriteLine($"Subject: {item.Subject}");
                            Console.WriteLine($"Comments: {item.Comments}");
                            Console.WriteLine($"Sign Time: {item.SignTime}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## 高级验证场景

GroupDocs.Signature 为更复杂的验证场景提供了附加选项：

### 验证多个数字签名

```csharp
// 创建验证选项列表
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// 添加第一个证书验证选项
listOptions.Add(new DigitalVerifyOptions("Certificate1.pfx")
{
    Contact = "John Smith"
});

// 添加第二个证书验证选项
listOptions.Add(new DigitalVerifyOptions("Certificate2.pfx")
{
    Contact = "Jane Doe"
});

// 使用多个选项进行验证
VerificationResult result = signature.Verify(listOptions);
```

### 验证特定页面上的签名

```csharp
// 仅验证第一页的数字签名
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    AllPages = false,
    PageNumber = 1
};
```

### 使用时间戳和证书颁发机构验证

```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    ValidateTimeStampOnly = true,   // 仅验证时间戳
    CertificateAuth = CertificateAuthType.Standard  // 验证签名者的证书
};
```

## 数字签名验证的最佳实践

1. 适当的证书管理：安全地存储证书文件并适当管理密码。
2. 证书验证：实施证书链验证以确保证书本身有效。
3. 错误处理：实施强大的错误处理，以优雅地管理验证失败。
4. 日志记录：记录验证尝试和结果以供审计和合规目的。
5. 定期证书更新：确保证书在到期前更新。

## 常见问题故障排除

### 证书无效
- 验证证书文件路径是否正确
- 确保证书密码正确
- 检查证书是否已过期

### 未找到签名
- 确认文档确实包含数字签名
- 确认您正在检查正确的页面

### 验证失败
- 检查文档在签名后是否被修改
- 验证签名者的证书是否在受信任的证书链中

## 结论

GroupDocs.Signature for .NET 提供了一个强大而灵活的解决方案，用于验证文档中的数字签名。按照本分步指南，您可以在 .NET 应用程序中实现强大的数字签名验证，确保文档的真实性和完整性。

数字签名验证是现代商业环境中安全文档工作流程的关键组成部分。借助 GroupDocs.Signature，您可以轻松自信地实现此功能，并利用全面的 API 处理各种验证场景。

## 常见问题解答

### GroupDocs.Signature 能否验证使用 Adobe Acrobat 签名的 PDF 文档中的签名？
是的，GroupDocs.Signature 可以验证由 Adobe Acrobat 和其他兼容 PDF 软件创建的 PDF 文档中的标准数字签名。

### GroupDocs.Signature 是否支持文档时间戳验证？
是的，API 提供了验证文档时间戳的选项，作为数字签名验证过程的一部分。

### 我可以验证多页文档中特定页面上的签名吗？
是的，您可以配置验证选项来检查特定页面而不是整个文档上的签名。

### GroupDocs.Signature 是否支持验证单个文档中的多个签名？
是的，GroupDocs.Signature 可以验证单个文档中的多个数字签名，并为每个签名提供详细的结果。

### 是否可以验证使用来自不同证书颁发机构的证书创建的签名？
是的，GroupDocs.Signature 支持验证使用来自不同证书颁发机构的证书创建的签名，只要它们位于受信任的证书链中。

### 相关资源
* [GroupDocs.Signature API 参考](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature 下载](https://releases.groupdocs.com/signature/net/)
* [GitHub 上的代码示例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [文档](https://docs.groupdocs.com/signature/net/)
* [产品页面](https://products.groupdocs.com/signature/net/)
* [博客文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [支持论坛](https://forum.groupdocs.com/c/signature/13)
* [临时执照](https://purchase.groupdocs.com/temporary-license/)