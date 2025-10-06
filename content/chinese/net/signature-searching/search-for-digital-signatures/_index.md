---
"description": "使用 GroupDocs.Signature for .NET 轻松搜索文档中的数字签名。使用我们详细的分步指南，增强文档安全性和验证能力。"
"linktitle": "搜索数字签名"
"second_title": "GroupDocs.签名 .NET API"
"title": "在文档中搜索数字签名"
"url": "/zh/net/signature-searching/search-for-digital-signatures/"
"weight": 11
type: docs
---
## 介绍

在当今的数字环境中，确保文档的真实性和完整性对企业和组织至关重要。数字签名提供了一种强大的机制来验证文档的真实性和检测未经授权的修改。GroupDocs.Signature for .NET 提供了一个全面的解决方案，用于处理各种文档格式的数字签名，使开发人员能够将签名功能无缝集成到他们的 .NET 应用程序中。

本教程将指导您使用 GroupDocs.Signature for .NET 在文档中搜索数字签名的过程，并提供详细的解释和实际的代码示例。

## 先决条件

在深入了解实施细节之前，请确保您满足以下先决条件：

1. GroupDocs.Signature for .NET：从以下位置下载并安装该库 [这里](https://releases。groupdocs.com/signature/net/).
   
2. 开发环境：使用 Visual Studio 或您喜欢的 IDE 设置 .NET 开发环境。
   
3. 示例文档：准备包含数字签名的示例文档以供测试目的。

4. 基础知识：熟悉 C# 编程语言和 .NET 框架基础知识。

## 导入命名空间

首先导入所需的命名空间以访问 GroupDocs.Signature for .NET 提供的功能：

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

现在，让我们将搜索数字签名的过程分解为清晰、易于管理的步骤：

## 步骤1：初始化签名对象

首先创建一个实例 `Signature` 类，将路径传递给您的文档：

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // 搜索数字签名的代码将在此处添加
}
```

## 第 2 步：搜索数字签名

接下来，使用 `Search` 方法与 `SignatureType.Digital` 在文档中搜索数字签名的参数：

```csharp
// 在文档中搜索数字签名
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## 步骤3：处理并显示结果

最后，处理搜索结果并显示找到的数字签名的相关信息：

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## 完整示例

这是一个完整的、可运行的示例，演示了如何在文档中搜索数字签名：

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文档路径
            string filePath = "sample_multiple_signatures.docx";
            
            // 初始化签名实例
            using (Signature signature = new Signature(filePath))
            {
                // 在文档中搜索数字签名
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // 显示搜索结果
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## 高级搜索选项

如需更有针对性的搜索，您可以使用 `DigitalSearchOptions` 自定义搜索条件：

```csharp
// 创建数字搜索选项
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // 仅搜索特定页面（例如第 1 页和第 2 页）
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // 按数字签名中的注释进行过滤
    Comments = "Approved",
    
    // 设置搜索的日期和时间范围
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// 使用特定选项进行搜索
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## 使用证书信息

数字签名包含您可以访问和验证的宝贵证书信息：

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // 访问证书属性
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // 检查证书是否在有效日期范围内
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // 访问证书颁发者详细信息
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## 结论

GroupDocs.Signature for .NET 提供了一个强大而灵活的解决方案，用于在文档中搜索和验证数字签名。在本教程中，我们逐步探索了在 .NET 应用程序中实现数字签名搜索功能的过程，为您提供了增强文档安全性和完整性验证的知识。

通过利用 GroupDocs.Signature，您可以构建强大的文档管理系统，确保数字文档的真实性和完整性，从而在业务流程中建立信任和合规性。

## 常见问题解答

### GroupDocs.Signature 可以验证数字签名的有效性吗？

是的，GroupDocs.Signature 在搜索过程中自动验证数字签名，并通过 `IsValid` 的财产 `DigitalSignature` 班级。

### 哪些文档格式支持数字签名搜索？

GroupDocs.Signature 支持各种格式的数字签名搜索，包括 PDF、Microsoft Office 文档（Word、Excel、PowerPoint）、OpenOffice 格式等。

### 我可以在受密码保护的文档中搜索数字签名吗？

是的，您可以在初始化时提供密码，在受密码保护的文档中搜索数字签名 `Signature` 目的：

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // 搜索数字签名
}
```

### 如何验证数字签名是否由特定的人创建？

您可以检查证书的主题名称和其他属性来验证签名者的身份：

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### 我可以从数字签名证书中提取公钥吗？

是的，您可以通过证书属性访问公钥信息：

```csharp
if (signature.Certificate != null)
{
    // 访问公钥信息
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## 参见

* [API 参考](https://reference.groupdocs.com/signature/net/)
* [代码示例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [产品文档](https://docs.groupdocs.com/signature/net/)
* [产品页面](https://products.groupdocs.com/signature/net/)
* [下载最新版本](https://releases.groupdocs.com/signature/net/)
* [博客文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [支持论坛](https://forum.groupdocs.com/c/signature/13)
* [临时执照](https://purchase.groupdocs.com/temporary-license/)