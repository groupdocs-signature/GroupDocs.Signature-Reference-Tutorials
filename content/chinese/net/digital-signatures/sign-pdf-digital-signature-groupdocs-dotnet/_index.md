---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 对 PDF 进行数字签名。自定义外观、应用字体和图像，确保文档的安全性和真实性。"
"title": ".NET 中的数字 PDF 签名——使用 GroupDocs.Signature 的指南"
"url": "/zh/net/digital-signatures/sign-pdf-digital-signature-groupdocs-dotnet/"
"weight": 1
type: docs
---
# .NET 中的数字 PDF 签名：使用 GroupDocs.Signature 的指南

## 介绍

PDF 文档上的数字签名可确保其真实性、安全性和完整性——这对于法律合同、发票和官方记录至关重要。 **适用于 .NET 的 GroupDocs.Signature** 简化了 PDF 的数字签名添加流程，同时允许自定义外观，提升视觉吸引力。本教程将指导您使用 GroupDocs.Signature 完成 PDF 文档签名，并重点讲解图像和字体的配置。

### 您将学到什么：
- 如何使用 .NET 对 PDF 文档进行数字签名
- 将自定义外观设置（如图像和字体）应用于您的数字签名
- 在您的项目中设置并初始化 .NET 的 GroupDocs.Signature

让我们首先介绍一下开始所需的先决条件。

## 先决条件（H2）

要遵循本教程，您需要：

- **适用于 .NET 的 GroupDocs.Signature** 库：确保它是通过 .NET CLI 或 NuGet 包管理器安装的。
  - **.NET CLI**： `dotnet add package GroupDocs.Signature`
  - **包管理器**： `Install-Package GroupDocs.Signature`

- PFX 格式的有效数字证书
- C# 和 .NET 环境设置的基础知识

## 为 .NET 设置 GroupDocs.Signature（H2）

首先安装 GroupDocs.Signature 库：

**.NET CLI**
```shell
dotnet add package GroupDocs.Signature
```

**包管理器**
```shell
Install-Package GroupDocs.Signature
```

或者，使用 NuGet 包管理器 UI 搜索并安装“GroupDocs.Signature”。

### 许可证获取

- **免费试用**：使用临时评估许可证探索全部功能。
- **临时执照**：从 [这里](https://purchase。groupdocs.com/temporary-license/).
- **购买**：如需长期使用，请购买订阅 [此链接](https://purchase。groupdocs.com/buy).

### 基本初始化和设置

要在 .NET 项目中初始化 GroupDocs.Signature：

```csharp
using GroupDocs.Signature;

// 使用源 PDF 文件初始化签名对象。
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF.pdf")) {
    // 您签署文件的代码放在这里。
}
```

## 实施指南

### 使用数字签名 (H2) 签署 PDF 文档

此功能允许您向 PDF 文档添加数字签名，以确保其真实性和完整性。

#### 功能概述
通过实现此功能，您可以使用 GroupDocs.Signature for .NET 对任何 PDF 文件进行数字签名。您还可以应用自定义设置来定制签名的外观，包括图像和字体。

#### 实施步骤（H3）

##### 步骤 1：设置您的环境

确保您的项目配置了必要的引用：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain;

namespace DigitalSignatureExample {
    public class SignPdfWithDigitalSignature {
        // 定义源 PDF 和数字证书的路径
        private static string sourceFile = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF.pdf";
        private static string outputFile = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithPdfDigitalAdvanced_Signed.pdf");
        private static string certificatePath = "YOUR_DOCUMENT_DIRECTORY/CertificatePfx.pfx";

        public static void Run() {
            // 初始化签名对象
            using (Signature signature = new Signature(sourceFile)) {
                // 设置数字签名选项
                DigitalSignOptions options = new DigitalSignOptions(certificatePath) {
                    Password = "1234567890",  // 证书密码
                    Reason = "Sign",          // 签名原因
                    Contact = "JohnSmith",    // 联系信息
                    Location = "Office1",     // 签约地点
                    Visible = true,            // 使签名可见
                    Left = 400,                // 水平位置
                    Top = 20,                  // 垂直位置
                    Height = 70,               // 签名高度
                    Width = 200,               // 签名宽度
                    ImageFilePath = "YOUR_DOCUMENT_DIRECTORY/ImageHandwrite.png", // 外观图
                    Appearance = new PdfDigitalSignatureAppearance() {
                        Foreground = System.Drawing.Color.FromArgb(50, System.Drawing.Color.Gray),
                        FontFamilyName = "TimesNewRoman",
                        FontSize = 12
                    }
                };

                // 签署文件并将其保存到输出路径。
                SignResult signResult = signature.Sign(outputFile, options);
                Console.WriteLine($"Document signed successfully with {signResult.Succeeded.Count} signature(s). File saved at {outputFile}.");
            }
        }
    }
}
```

##### 步骤 2：自定义签名外观

使用字体和图像设置自定义数字签名的外观：

```csharp
using System;
using GroupDocs.Signature.Options;
using GroupDocs.Signature.Domain;
using System.Drawing;

namespace DigitalSignatureAppearanceExample {
    public class CustomizeDigitalSignatureAppearance {
        public static void Run() {
            // 初始化数字签名的外观设置。
            PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance() {
                Foreground = Color.FromArgb(50, Color.Gray),  // 设置自定义字体颜色
                FontFamilyName = "TimesNewRoman",          // 指定字体系列
                FontSize = 12                               // 定义字体大小
            };

            Console.WriteLine("Custom appearance settings for digital signature have been applied.");
        }
    }
}
```

#### 关键配置选项
- **证书路径**：确保您提供了 PFX 文件的正确路径。
- **密码**：使用与您的数字证书关联的密码。
- **外观设置**：自定义字体和颜色以符合品牌要求。

##### 故障排除提示
- 验证您的数字证书是否有效且配置正确。
- 确保所有路径（PDF、输出、图像）都可以从应用程序环境访问。

### 将自定义外观设置应用于数字签名 (H2)

使用 GroupDocs.Signature for .NET 通过自定义字体和图像设置增强数字签名的视觉吸引力。

#### 概述
自定义数字签名的外观可以使其更具视觉吸引力，并符合品牌标准。此功能允许您设置特定的字体、颜色和图像。

#### 实施步骤（H3）

##### 步骤1：初始化外观设置

创建一个实例 `PdfDigitalSignatureAppearance`：

```csharp
using System.Drawing;

// 定义数字签名的自定义外观设置。
PdfDigitalSignatureAppearance appearance = new PdfDigitalSignatureAppearance() {
    Foreground = Color.FromArgb(50, Color.Gray),  // 自定义字体颜色
    FontFamilyName = "TimesNewRoman",            // 字体系列
    FontSize = 12                                // 字体大小
};
```

##### 步骤 2：应用外观设置

将这些设置集成到您的数字签名选项中：

```csharp
DigitalSignOptions options = new DigitalSignOptions(certificatePath) {
    ImageFilePath = "YOUR_DOCUMENT_DIRECTORY/ImageHandwrite.png",
    Appearance = appearance
};
```

## 实际应用（H2）

以下是使用 GroupDocs.Signature 签署 PDF 的一些实际场景：
1. **合同签订**：确保法律协议以数字方式签署和验证。
2. **发票审批**：对发票进行数字签名，以便财务部门更快地处理。
3. **文件认证**：验证官方文件的真实性，防止未经授权的更改。

通过遵循本指南，您将使用 GroupDocs.Signature 将数字签名有效地集成到您的 .NET 应用程序中，从而增强安全性和专业性。