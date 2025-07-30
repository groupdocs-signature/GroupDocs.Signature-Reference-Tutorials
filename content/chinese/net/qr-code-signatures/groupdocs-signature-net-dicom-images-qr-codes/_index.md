---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 为 DICOM 图像签名二维码。本指南涵盖医学影像中二维码签名的设置、实现和验证。"
"title": "如何使用 GroupDocs.Signature for .NET 为 DICOM 图像签名（二维码）——综合指南"
"url": "/zh/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
---

# 如何使用 GroupDocs.Signature for .NET 对带有二维码的 DICOM 图像进行签名：综合指南

您是否正在寻找一种安全的方法来验证您的 DICOM 文件？本详细指南将向您展示如何使用 GroupDocs.Signature for .NET 将二维码签名集成到 DICOM 图像中。本教程涵盖从设置到实施的整个过程，非常适合医疗专业人士、开发人员以及任何使用数字医疗文档的人员。

## 您将学到什么：
- 使用 GroupDocs.Signature for .NET 设置您的开发环境。
- 使用二维码签署 DICOM 图像的分步说明。
- 验证和搜索 DICOM 文件中的二维码签名的方法。
- 用于生成签名文档预览以供审查的技术。
- 优化性能和有效管理资源的最佳实践。

让我们从先决条件开始吧！

## 先决条件

要使用 GroupDocs.Signature for .NET，请确保您的环境已准备就绪。您需要：

### 所需的库和版本
- **适用于 .NET 的 GroupDocs.Signature**：确保与您的 .NET 框架兼容。

### 环境设置要求
- Windows 或 Linux 上的开发环境。
- 安装了 Visual Studio 或其他与 .NET 兼容的 IDE。

### 知识前提
- 对 C# 编程有基本的了解。
- 熟悉 .NET 应用程序中的文件 I/O。

## 为 .NET 设置 GroupDocs.Signature

使用您喜欢的方法安装 GroupDocs.Signature 库：

**使用 .NET CLI：**
```bash
dotnet add package GroupDocs.Signature
```

**包管理器：**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 包管理器 UI：**
- 搜索“GroupDocs.Signature”并安装最新版本。

### 许可证获取

先免费试用，探索各项功能。如需长期使用，请考虑从 [群组文档](https://purchase。groupdocs.com/buy).

安装完成后，初始化库：

```csharp
using GroupDocs.Signature;
// 使用您的 DICOM 文件路径初始化签名对象。
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## 实施指南

### 使用二维码签署 DICOM 图像

#### 概述
添加二维码签名，确保医疗文件的真实性和可追溯性。

**步骤1：初始化签名对象**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // 继续签名操作...
}
```

**步骤 2：创建二维码签名选项**

配置文本、大小和对齐等属性。

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**步骤 3：添加 XMP 元数据**

使用附加元数据来增强文档。

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**步骤4：签署文件**

执行签名并保存。

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### 获取文档信息

从签名的 DICOM 文件中检索元数据以确保数据完整性。

**概述：**
访问文档信息和 XMP 元数据签名进行验证。

**步骤 1：检索文档信息**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**步骤 2：迭代并打印 XMP 数据**

显示元数据详细信息。

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### 验证 DICOM 签名

验证 DICOM 图像中的二维码签名的真实性。

**概述：**
确保签名正确且真实。

**步骤 1：创建二维码验证选项**

设置与二维码中的特定文本匹配的选项。

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**第 2 步：验证签名**

检查签名是否符合标准。

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### 在 DICOM 中搜索签名

在签名的 DICOM 图像中找到二维码签名。

**概述：**
有效地查找所有二维码签名以管理文档真实性。

**步骤 1：搜索二维码签名**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**步骤 2：迭代并打印签名详细信息**

检查每个找到的签名的详细信息。

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### 生成签名 DICOM 的预览

创建视觉预览以供验证。

**概述：**
生成图像预览来验证内容，无需专门的软件。

**步骤 1：定义流方法**

设置预览生成期间文件流管理的方法。

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**第 2 步：生成预览**

执行预览生成过程。

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## 实际应用

1. **医疗记录管理**：使用二维码签名验证患者记录是否合规。
2. **医疗保健系统中的审计跟踪**：跟踪文档变化并使用二维码验证真实性。
3. **安全数据共享**：通过嵌入数字签名确保医学图像的安全共享。
4. **合规性验证**：定期验证 DICOM 文件的完整性以满足法律要求。
5. **与 EHR 系统集成**：将签名的 DICOM 文件无缝集成到电子健康记录 (EHR) 系统中，以简化操作。