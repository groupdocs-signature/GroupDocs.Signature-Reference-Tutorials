---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 高效地签署、验证、搜索、更新和删除文档中的文本签名。立即简化您的数字签名流程。"
"title": "使用 GroupDocs.Signature for .NET 进行主文档签名和验证"
"url": "/zh/net/digital-signatures/master-document-signing-groupdocs-signature-net/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature for .NET 进行主文档签名和验证

## 如何使用 GroupDocs.Signature for .NET 掌握文档签名和验证

在当今的数字时代，高效的文档签名解决方案对于管理合同、协议或任何法律文件至关重要。自动化此流程可以节省时间并减少错误。 **适用于 .NET 的 GroupDocs.Signature** 提供强大的解决方案，简化应用程序中的文本签名管理。本指南将带您了解 GroupDocs.Signature for .NET 的功能，包括签名、验证、搜索、更新和删除文本签名。

## 您将学到什么

- 如何使用可自定义的文本签名签署文档
- 有效验证签名文件的技术
- 在文档中搜索现有文本签名的方法
- 根据需要更新和删除文本签名的步骤
- 优化性能和内存管理的最佳实践

让我们先了解一下先决条件。

## 先决条件

开始之前，请确保您的开发环境已设置必要的工具：

### 所需的库和依赖项

- **适用于 .NET 的 GroupDocs.Signature**：该库使您能够在应用程序中添加签名功能。
- **.NET Framework 4.6.1 或更高版本** （或 .NET Core 2.x+）

### 环境设置要求

您将需要一个 C# 开发环境（例如 Visual Studio）和互联网连接来下载必要的软件包。

### 知识前提

建议您熟悉基本的 C# 编程概念。如果您是 GroupDocs.Signature for .NET 的新手，不用担心——本指南将指导您完成每个步骤。

## 为 .NET 设置 GroupDocs.Signature

首先，您需要在项目中安装 GroupDocs.Signature 库。具体操作如下：

### 通过 .NET CLI 安装
```bash
dotnet add package GroupDocs.Signature
```

### 程序包管理器控制台
```powershell
Install-Package GroupDocs.Signature
```

### NuGet 包管理器 UI
1. 在 Visual Studio 中打开您的项目。
2. 导航至 **工具** > **NuGet 包管理器** > **管理解决方案的 NuGet 包**。
3. 搜索“GroupDocs.Signature”并安装最新版本。

#### 许可证获取步骤
- **免费试用**：从下载开始免费试用 [GroupDocs 免费试用](https://releases。groupdocs.com/signature/net/).
- **临时执照**：获取临时许可证以评估完整功能 [临时执照](https://purchase。groupdocs.com/temporary-license/).
- **购买**：如需继续使用，请从 [GroupDocs 购买页面](https://purchase。groupdocs.com/buy).

#### 基本初始化和设置

安装后，在您的项目中初始化 GroupDocs.Signature，如下所示：

```csharp
using GroupDocs.Signature;

// 使用文档路径初始化签名实例。
Signature signature = new Signature("path/to/your/document.pdf");
```

现在您已完成设置，让我们探索如何利用 GroupDocs.Signature 实现各种功能。

## 实施指南

### 使用文本签名签署文档

此功能允许您向文档添加文本签名。让我们来详细了解一下：

#### 概述
您可以使用字体大小、颜色、对齐方式等各种选项自定义文本签名的外观和位置。

#### 逐步实施

**步骤 1**：定义文件路径和输出位置。
```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY"; // 原始文档的路径
string outputFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignedDocument.docx");
```

**第 2 步**：使用创建文本签名 `TextSignOptions`。
```csharp
using (Signature signature = new Signature(filePath))
{
    TextSignOptions signOptions = new TextSignOptions("John Smith")
    {
        VerticalAlignment = GroupDocs.Signature.Options.VerticalAlignment.Top,
        HorizontalAlignment = GroupDocs.Signature.Options.HorizontalAlignment.Center,
        Width = 100,
        Height = 40,
        Margin = new Padding(20),
        ForeColor = Color.Red,
        Font = new SignatureFont { Size = 12, FamilyName = "Comic Sans MS" }
    };
```

**步骤3**：签署文件并输出结果。
```csharp
    SignResult signResult = signature.Sign(outputFilePath, signOptions);
    foreach (BaseSignature temp in signResult.Succeeded)
    {
        Console.WriteLine($"Signed Text Signature: Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
```

#### 关键配置选项
- **垂直对齐和水平对齐**：控制签名在页面上出现的位置。
- **字体**：自定义文本签名的字体大小和样式。

### 验证文档中的文本签名

验证可确保文档已按预期签署。具体实现方式如下：

#### 概述
验证文档中现有的文本签名以确认其真实性和完整性。

#### 逐步实施

**步骤 1**：指定签名文档的文件路径。
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // 签名文档的路径
```

**第 2 步**：使用以下方式创建验证选项 `TextVerifyOptions`。
```csharp
using (Signature signature = new Signature(filePath))
{
    TextVerifyOptions verifyOptions = new TextVerifyOptions()
    {
        AllPages = false,
        PageNumber = 1,
        Text = "John Smith",
        MatchType = GroupDocs.Signature.Options.TextMatchType.Exact
    };
```

**步骤3**：验证文件。
```csharp
    VerificationResult verifyResult = signature.Verify(verifyOptions);
    if (verifyResult.IsValid)
    {
        Console.WriteLine("Document was verified successfully!");
    }
    else
    {
        Console.WriteLine("Document failed verification process.");
    }
}
```

#### 故障排除提示
- 确保 `Text` 属性与文档中的内容完全匹配。
- 检查 `PageNumber` 对应于包含签名的正确页面。

### 搜索文档中的文本签名

使用此功能可以有效地在文档中定位文本签名。

#### 概述
搜索文档的全部或选定页面以查找特定的文本签名。

#### 逐步实施

**步骤 1**：定义文件路径。
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // 签名文档的路径
```

**第 2 步**： 使用 `TextSearchOptions` 进行搜索。
```csharp
using (Signature signature = new Signature(filePath))
{
    TextSearchOptions searchOptions = new TextSearchOptions()
    {
        AllPages = true,
        MatchType = GroupDocs.Signature.Options.TextMatchType.Exact,
        Text = "John Smith"
    };
```

**步骤3**：执行搜索。
```csharp
    List<TextSignature> signatures = signature.Search<TextSignature>(searchOptions);
    foreach (TextSignature textSignature in signatures)
    {
        if (textSignature != null)
        {
            Console.WriteLine($"Found Text signature at page {textSignature.PageNumber} with type [{textSignature.SignatureImplementation}] and text '{textSignature.Text}'. Location: {textSignature.Left}-{textSignature.Top}. Size is {textSignature.Width}x{textSignature.Height}.");
        }
    }
}
```

### 更新文档文本签名

在需要时修改文档中现有的文本签名。

#### 概述
调整现有文本签名的属性，例如大小和位置。

#### 逐步实施

**步骤 1**：指定文件路径和签名ID。
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // 签名文档的路径
List<string> signatureIds = new List<string>(); // 假设此列表中填充了有效的签名 ID
```

**第 2 步**： 创造 `TextSignature` 需要更新的对象。
```csharp
using (Signature signature = new Signature(filePath))
{
    foreach (var item in signatureIds)
    {
        TextSignature temp = new TextSignature(item)
        {
            Width = 150,
            Height = 50,
            HorizontalAlignment = GroupDocs.Signature.Options.HorizontalAlignment.Right
        };
```

**步骤3**：更新文档。
```csharp
        SignResult signResult = signature.UpdateSignatures(temp);
        if (signResult.Succeeded.Count > 0)
        {
            Console.WriteLine($"Updated Text Signature: Id:{temp.SignatureId}");
        }
    }
}
```

#### 关键配置选项
- **宽度和高度**：调整签名的大小。
- **水平对齐**：控制更新后的签名在页面上出现的位置。

## 结论

通过本指南，您学习了如何使用 GroupDocs.Signature for .NET 来签名、验证、搜索、更新和删除文档中的文本签名。这些功能对于在应用程序中自动化数字签名流程至关重要。有关更多详细信息和高级选项，请参阅 [官方文档](https://docs。groupdocs.com/signature/net/).