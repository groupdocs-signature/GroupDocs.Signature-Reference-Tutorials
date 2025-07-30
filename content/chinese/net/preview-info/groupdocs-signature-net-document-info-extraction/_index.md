---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 提取详细的文档信息，包括签名、元数据等。本指南涵盖设置、实施和最佳实践。"
"title": "掌握 GroupDocs.Signature for .NET&#58; 高效提取和显示文档信息"
"url": "/zh/net/preview-info/groupdocs-signature-net-document-info-extraction/"
"weight": 1
---

# 掌握 .NET 的 GroupDocs.Signature：高效提取和显示文档信息

## 介绍

您是否希望高效地从应用程序中的文档中提取全面的详细信息？无论是管理合同、协议还是多页 PDF，强大的解决方案都至关重要。 **适用于 .NET 的 GroupDocs.Signature** 提供强大的功能，旨在通过检索和显示表单字段、签名、元数据等元素来简化文档分析。本教程将指导您如何利用这些功能来增强应用程序的功能。

**您将学到什么：**
- 如何使用 GroupDocs.Signature for .NET 检索详细文档信息
- 显示各种签名类型和表单字段详细信息
- 提取元数据和页面特定属性

在深入实施之前，让我们先回顾一下先决条件。

## 先决条件

在利用 GroupDocs.Signature for .NET 之前，请确保您的环境已正确设置。本教程假设您熟悉 C# 并具备文档处理概念的基础知识。

### 所需的库和依赖项
- **适用于 .NET 的 GroupDocs.Signature**：我们将使用的主要库。
- **.NET Framework 或 .NET Core**：取决于您的项目设置。

### 环境设置
确保您已准备好 Visual Studio 或其他支持 .NET 项目的合适 IDE 的开发环境。

### 知识前提
- 对 C# 编程有基本的了解。
- 熟悉文档类型（PDF、Word、Excel）及其属性。

## 为 .NET 设置 GroupDocs.Signature

要使用 GroupDocs.Signature for .NET，您需要安装该库。以下是几种方法：

### 安装说明

**使用 .NET CLI：**
```bash
dotnet add package GroupDocs.Signature
```

**使用包管理器控制台：**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 包管理器 UI：**
在 NuGet 包管理器中搜索“GroupDocs.Signature”并安装最新版本。

### 许可证获取
要充分利用 GroupDocs.Signature，请考虑获取许可证：
- **免费试用**：从免费试用开始探索功能。
- **临时执照**：获取临时许可证以进行延长测试。
- **购买**：购买用于生产用途的完整许可证。

安装并获得许可后，通过设置 GroupDocs.Signature 环境来初始化您的项目，如下所示：

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;

public class GetDocumentInfoFeature
{
    public static void Run()
    {
        // 定义要分析的文档的文件路径
        string filePath = "YOUR_DOCUMENT_DIRECTORY\Sample_Signed_Multi_Document.pdf";  // 替换为您的实际文档路径
        
        SignatureSettings signatureSettings = new SignatureSettings
        {
            IncludeStandardMetadataSignatures = true
        };

        using (Signature signature = new Signature(filePath, signatureSettings))
        {
            IDocumentInfo documentInfo = signature.GetDocumentInfo();
            // 进一步的操作将在这里进行...
        }
    }
}
```

## 实施指南

设置完成后，让我们探索如何实现 GroupDocs.Signature for .NET 的各种功能。

### 检索并显示基本文档属性

**概述**：提取文件格式、大小和页数等基本属性。

#### 逐步实施：
1. **初始化签名对象**：创建 `Signature` 与您的文档路径相关的类。
2. **GetDocumentInfo 方法**：使用 `GetDocumentInfo()` 方法来检索有关文档的详细信息。
3. **显示文档属性**：使用以下方式输出格式、扩展名和大小等基本属性 `Console.WriteLine` 用于调试或记录目的。

```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
```

### 显示有关每个文档页面的信息

**概述**：通过检索和显示有关文档中每一页的信息来深入了解。

#### 逐步实施：
1. **遍历页面**：循环遍历 `documentInfo.Pages` 访问单个页面的详细信息，例如宽度和高度。

```csharp
foreach (PageInfo pageInfo in documentInfo.Pages)
{
    Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```

### 显示表单字段签名信息

**概述**：提取并显示与文档内的表单字段相关的信息。

#### 逐步实施：
1. **访问表单字段**： 使用 `documentInfo.FormFields` 检索文档中存在的所有表单字段签名。
2. **显示每个表单字段的详细信息**：遍历每个表单字段并输出其类型、名称和值。

```csharp
Console.WriteLine($"Document Form Fields information: count = {documentInfo.FormFields.Count}");
foreach (FormFieldSignature formField in documentInfo.FormFields)
{
    Console.WriteLine($" - type #{formField.Type}: Name: {formField.Name} Value: {formField.Value}");
}
```

### 显示各种签名信息

**概述**：检索和显示文本、图像、数字、条形码、二维码、表单字段和元数据签名的信息。

#### 实施步骤：
- **文本签名**： 使用权 `documentInfo.TextSignatures` 获取每个文本签名的详细信息，包括其 ID、位置、大小和创建日期。

```csharp
Console.WriteLine($"Document Text signatures: {documentInfo.TextSignatures.Count}");
foreach (TextSignature textSignature in documentInfo.TextSignatures)
{
    Console.WriteLine($" - #{textSignature.SignatureId}: Text: {textSignature.Text} Location: {textSignature.Left}x{textSignature.Top}. Size: {textSignature.Width}x{textSignature.Height}. CreatedOn/ModifiedOn: {textSignature.CreatedOn.ToShortDateString()} / {textSignature.ModifiedOn.ToShortDateString()}");
}
```

- **图像签名**：与文本签名类似，使用 `documentInfo.ImageSignatures` 有关图像签名的大小和格式等详细信息。

```csharp
Console.WriteLine($"Document Image signatures: {documentInfo.ImageSignatures.Count}");
foreach (ImageSignature imageSignature in documentInfo.ImageSignatures)
{
    Console.WriteLine($" - #{imageSignature.SignatureId}: Size: {imageSignature.Size} bytes, Format: {imageSignature.Format}. CreatedOn/ModifiedOn: {imageSignature.CreatedOn.ToShortDateString()} / {imageSignature.ModifiedOn.ToShortDateString()}");
}
```

- **数字签名**：对于数字签名，利用 `documentInfo.DigitalSignatures` 提取签名 ID 和时间戳。

```csharp
Console.WriteLine($"Document Digital signatures: {documentInfo.DigitalSignatures.Count}");
foreach (DigitalSignature digitalSignature in documentInfo.DigitalSignatures)
{
    Console.WriteLine($" - #{digitalSignature.SignatureId}. CreatedOn/ModifiedOn: {digitalSignature.CreatedOn.ToShortDateString()} / {digitalSignature.ModifiedOn.ToShortDateString()}");
}
```

- **条形码和二维码签名**： 使用 `documentInfo.BarcodeSignatures` 和 `documentInfo.QrCodeSignatures` 分别收集条形码和二维码的详细信息。

```csharp
Console.WriteLine($"Document Barcode signatures: {documentInfo.BarcodeSignatures.Count}");
foreach (BarcodeSignature barcodeSignature in documentInfo.BarcodeSignatures)
{
    Console.WriteLine($" - #{barcodeSignature.SignatureId}: Type: {barcodeSignature.EncodeType?.TypeName}. Text: {barcodeSignature.Text}");
}

Console.WriteLine($"Document QR Code signatures: {documentInfo.QrCodeSignatures.Count}");
foreach (QrCodeSignature qrCodeSignature in documentInfo.QrCodeSignatures)
{
    Console.WriteLine($" - #{qrCodeSignature.SignatureId}: Type: {qrCodeSignature.EncodeType?.TypeName}. Text: {qrCodeSignature.Text}");
}
```

### 结论

通过本教程，您学习了如何利用 GroupDocs.Signature for .NET 高效地提取和显示全面的文档信息。这项技能将增强您的应用程序精准、轻松地管理文档的能力。

**后续步骤：**
- 探索 GroupDocs.Signature 的其他功能。
- 在您的应用程序中实施签名验证。
- 将此功能集成到更大的工作流程中，以实现自动化文档处理。