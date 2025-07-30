---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 为 PDF 文档签名 HIBC 二维码。本指南涵盖 LIC 和 PAS 二维码，包括二维码、Aztec 码和 DataMatrix 码。"
"title": "如何使用 GroupDocs.Signature for .NET 签署带有 HIBC 二维码的文档——综合指南"
"url": "/zh/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
---

# 如何使用 GroupDocs.Signature for .NET 签署带有 HIBC QR 码的文档

## 介绍

在当今快节奏的商业环境中，确保文件的真实性和完整性至关重要。无论您处理的是药品、保健产品还是物流，拥有安全的文档签名和追踪方法可以节省时间并避免错误。输入 **适用于 .NET 的 GroupDocs.Signature**，一个强大的库，旨在通过将 HIBC QR 码无缝集成到您的文档中来简化文档管理流程。

在本教程中，我们将探讨如何利用 GroupDocs.Signature for .NET 为带有各种 HIBC QR 码（LIC（许可证）和 PAS（产品认证系统））的 PDF 文档签名，包括 QR 码、Aztec 码和 DataMatrix。最终，您将对如何在 .NET 应用程序中实现这些解决方案有深入的理解。

**您将学到什么：**
- 如何为 .NET 设置 GroupDocs.Signature
- 实施 HIBC LIC QR 码、Aztec 码和 DataMatrix
- 添加 HIBC PAS QR 码、Aztec 码和 DataMatrix
- 实际用例和集成可能性

在开始实现这些功能之前，让我们先深入了解一下先决条件。

## 先决条件

在开始编码之前，请确保您已准备好以下内容：

- **.NET 环境**：确保您的系统上安装了 .NET（最好是 .NET Core 或 .NET 5/6+）。
- **适用于 .NET 的 GroupDocs.Signature**：这个库将成为我们的主要工具。您可以通过 NuGet 安装它。
- **基本编程知识**：建议熟悉 C# 并在 .NET 中处理文件。

### 所需库

要将 GroupDocs.Signature 用于 .NET，您需要使用以下方法之一添加包：

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**包管理器**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 包管理器 UI**
搜索“GroupDocs.Signature”并安装最新版本。

### 许可证获取

您可以获取免费试用许可证进行测试。如需长期使用，请考虑购买订阅或申请临时许可证：

- **免费试用**： 使用权 [这里](https://releases.groupdocs.com/signature/net/)
- **临时执照**：请求于 [此链接](https://purchase.groupdocs.com/temporary-license/)

### 环境设置

设置环境，确保您的项目目标为适当的 .NET 版本并可以访问 GroupDocs.Signature。在应用程序中按如下所示初始化它：

```csharp
using GroupDocs.Signature;
```

## 为 .NET 设置 GroupDocs.Signature

要开始使用 GroupDocs.Signature for .NET，您需要安装库并在项目中配置基本设置。

### 安装

按照上述方法之一将 GroupDocs.Signature 添加到您的项目中。安装后，请在代码文件中引用它，以确保您的项目已配置为使用它。

### 许可证初始化

获取许可证后，按如下方式初始化它：

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

此设置将允许您无限制地访问 GroupDocs.Signature 的所有功能。

## 实施指南

现在，让我们深入研究如何使用 GroupDocs.Signature for .NET 的 HIBC QR 码实现每个功能。

### 使用 HIBC LIC 二维码签署文件

#### 概述

使用 HIBC LIC 二维码对文档进行签名，可确保许可场景中的合规性和可追溯性。本节将指导您如何在 PDF 文档中创建和嵌入二维码。

#### 实施步骤

##### 步骤 1：配置源和输出路径

定义源文档的位置以及签名输出的保存位置：

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### 步骤 2：创建二维码签名选项

使用特定文本和设置配置您的二维码：

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_QR_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR)
    {
        Left = 1,
        Top = 1,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // 使用这些选项签署文件。
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**解释**： 
- `QrCodeSignOptions` 设置二维码的外观和内容。在这里，我们指定 HIBC LIC 二维码类型并将其放置在文档上。
- `ReturnContent` 设置为 true 允许您检索签名文档的渲染图像。

#### 故障排除提示

- 确保文档路径指定正确。
- 验证 GroupDocs.Signature 是否已获得适当许可以实现全部功能。

### 使用 HIBC LIC Aztec 代码签署文件

#### 概述

Aztec 码提供了另一种编码形式，适用于高密度信息存储。本节重点介绍如何使用 GroupDocs.Signature 将 Aztec 码嵌入到您的文档中。

#### 实施步骤

##### 步骤 1：配置路径

与上一个功能类似，定义文件路径：

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### 步骤 2：配置 Aztec 代码选项

使用 GroupDocs.Signature 设置您的 Aztec 代码：

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_AZ_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec)
    {
        Left = 1,
        Top = 200,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_AZ_Options);
}
```

**解释**： 
- 这 `QrCodeSignOptions` 这里再次使用，但采用的是 Aztec 代码类型。
- 定位（`Top`， `Left`) 和内容检索设置与二维码类似。

#### 故障排除提示

- 确认文件路径准确。
- 确保 GroupDocs.Signature 的版本支持 Aztec 代码类型。

### 使用 HIBC LIC DataMatrix 签署文件

#### 概述

DataMatrix 代码提供了另一种强大的数据存储方法。本节演示如何将 DataMatrix 集成到您的 PDF 文档中。

#### 实施步骤

##### 步骤 1：设置文件路径

和以前一样，确定文件所在的位置：

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### 步骤 2：创建 DataMatrix 标志选项

配置并应用 DataMatrix 代码：

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_DM_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix)
    {
        Left = 1,
        Top = 400,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_DM_Options);
}
```

**解释**： 
- `QrCodeSignOptions` 用于设置DataMatrix代码的外观和内容。
- 定位（`Top`， `Left`) 和检索设置遵循与之前的代码相同的模式。

#### 故障排除提示

- 确保所有文件路径均正确指定。
- 验证 GroupDocs.Signature 在您的版本中是否支持 DataMatrix 代码类型。

### 使用 HIBC PAS 二维码签署文件

#### 概述

使用 HIBC PAS 二维码签署文档可增强产品追踪和可追溯性。本节将指导您如何使用 GroupDocs.Signature 将 PAS 二维码嵌入 PDF 文件。

#### 实施步骤

##### 步骤 1：配置源和输出路径

定义源文档的位置以及签名输出的保存位置：

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### 步骤 2：创建二维码签名选项

使用特定文本和设置配置您的 PAS QR 码：

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcPas_QR_Options = new QrCodeSignOptions("PAS123456789012", QrCodeTypes.HIBCPASQR)
    {
        Left = 1,
        Top = 500,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // 使用这些选项签署文件。
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**解释**： 
- `QrCodeSignOptions` 配置为 HIBC PAS QR 码类型并定位在文档上。
- `ReturnContent` 设置为 true 则检索签名文档的渲染图像。

#### 故障排除提示

- 确保所有路径均正确指定。
- 验证 GroupDocs.Signature 在您的版本中是否支持 PAS QR Code 类型。

### 结论

按照本指南，您可以使用 GroupDocs.Signature for .NET 将 HIBC LIC 和 PAS 二维码高效地集成到 PDF 文档中。此流程可增强各行各业的文档安全性、可追溯性和合规性。如需进一步的自定义和高级功能，请参阅 [GroupDocs 文档](https://docs。groupdocs.com/signature/net/).