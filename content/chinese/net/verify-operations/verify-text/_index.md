---
"description": "使用 GroupDocs.Signature 掌握 .NET 应用程序中的文本签名验证。提供包含完整代码示例和最佳实践的分步实施指南。"
"linktitle": "验证文本"
"second_title": "GroupDocs.签名 .NET API"
"title": "验证文档中的文本签名"
"url": "/zh/net/verify-operations/verify-text/"
"weight": 13
type: docs
---
## 介绍

文本签名虽然通常比数字或电子签名更简单，但在文档管理和验证中却起着至关重要的作用。无论是水印、页脚文本还是特定的内容模式，验证文本签名的存在性和完整性都是文档验证流程中的一个重要环节。

GroupDocs.Signature for .NET 提供了一个强大的 API，用于验证各种格式文档中的文本签名。本教程将指导您在 .NET 应用程序中实现文本验证功能，确保您的文档保持完整性和真实性。

## 先决条件

在实现文本验证功能之前，请确保您已满足以下先决条件：

1. GroupDocs.Signature for .NET：从下载并安装库 [下载页面](https://releases。groupdocs.com/signature/net/).
2. .NET 开发环境：Visual Studio 或任何兼容的 .NET 开发环境。
3. 基础知识：熟悉 C# 编程和 .NET 框架概念。
4. 测试文档：包含用于验证目的的文本签名的文档。

## 导入所需的命名空间

首先导入必要的命名空间来访问 GroupDocs.Signature 功能：

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

让我们将文本验证过程分解为清晰、易于管理的步骤：

## 步骤 1：指定文档路径

```csharp
// 包含文本签名的文档的路径
string filePath = "sample_multiple_signatures.docx";
```

确保将示例路径替换为包含文本签名的文档的实际路径。

## 步骤2：初始化签名对象

```csharp
// 通过传递文档路径创建 Signature 类的实例
using (Signature signature = new Signature(filePath))
{
    // 验证码将在此处执行
}
```

Signature 类是 GroupDocs.Signature API 中所有操作的主要入口点。

## 步骤 3：配置文本验证选项

```csharp
// 定义文本验证选项
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // 检查文件的所有页面
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // 待验证的文本
    MatchType = TextMatchType.Contains             // 指定匹配条件
};
```

验证选项允许您定义验证过程的具体标准：
- `AllPages`：设置为 true 则检查所有文档页面
- `SignatureImplementation`：指定文本的实现方式（原生或贴纸）
- `Text`：文档中要匹配的文本内容
- `MatchType`：文本匹配的方法（Contains、Exact、StartsWith 等）

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
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // 显示成功签名的信息
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

此代码检查验证是否成功并提供有关已验证的文本签名的详细信息。

## 完整示例

以下是演示文本签名验证的完整工作示例：

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
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // 验证文档签名
                    VerificationResult result = signature.Verify(options);
                    
                    // 工艺验证结果
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
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

### 使用正则表达式进行验证

为了更灵活的模式匹配，您可以使用正则表达式：

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // 匹配诸如“发票 #12345”之类的模式
    MatchType = TextMatchType.Regex
};
```

### 验证特定文档区域中的文本

您可以将验证限制在文档的特定区域：

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // 仅在第一页验证
    
    // 定义搜索区域（以点为单位的坐标）
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // 矩形面积（以毫米为单位）
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### 同时验证多个文本模式

您可以创建多个验证选项来检查不同的文本模式：

```csharp
// 创建验证选项列表
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// 添加第一个文本验证
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// 添加二次文本验证
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// 使用多个选项进行验证
VerificationResult result = signature.Verify(listOptions);
```

### 验证具有特定外观的文本

您还可以验证具有特定格式特征的文本：

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // 验证特定外观属性
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## 文本验证的最佳实践

1. 选择适当的匹配类型：根据您的验证要求选择正确的匹配类型（包含、精确、正则表达式）。
2. 优化性能：对于大型文档，请考虑验证特定页面而不是整个文档。
3. 错误处理：实施适当的错误处理，以优雅地管理意外情况。
4. 考虑大小写敏感性：在文本匹配中要注意大小写敏感性，特别是对于关键验证。
5. 彻底测试：使用各种文档格式和文本模式进行测试验证，以确保兼容性。

## 常见问题故障排除

### 未检测到文本
- 检查文本格式或编码是否影响检测
- 确保文本确实以常规文本（而非图像）的形式存在于文档中
- 尝试不同的匹配条件（包含而不是精确）

### 性能问题
- 通过定位特定页面或区域来优化验证
- 使用更具体的文本模式来减少误报

### 验证失败
- 检查空格、特殊字符或格式是否影响匹配
- 验证文本不是扫描图像的一部分（需要 OCR）
- 确保文档自添加文本以来未被修改

## 结论

文本验证是一种多功能且实用的文档身份验证方法，可以单独使用，也可以与其他验证方法结合使用。GroupDocs.Signature for .NET 提供了一个全面且易于使用的 API，可用于在 .NET 应用程序中实现强大的文本验证功能。

通过遵循本分步指南，您学会了如何：
- 配置并初始化文本验证过程
- 指定各种验证标准
- 处理和解释验证结果
- 实施高级验证场景

这些功能使您能够构建安全可靠的文档处理系统，以验证各种文档格式的文本的真实性。

## 常见问题解答

### GroupDocs.Signature 可以验证扫描文档中的文本吗？
GroupDocs.Signature 主要用于数字文本验证。对于扫描文档，您需要先使用 OCR（光学字符识别）技术将扫描图像转换为文本。

### 文本验证支持哪些文档格式？
GroupDocs.Signature 支持多种文档格式，包括 PDF、Word 文档（DOC、DOCX）、Excel 电子表格（XLS、XLSX）、PowerPoint 演示文稿（PPT、PPTX）、图像等。

### 我可以验证格式化的文本（粗体、斜体、特定字体）吗？
是的，GroupDocs.Signature 提供了验证具有特定格式特征的文本的选项，包括字体系列、大小、样式（粗体、斜体）和颜色。

### 是否可以验证受密码保护的文档中的文本？
是的，GroupDocs.Signature 提供了在打开受保护的文档进行验证时指定文档密码的选项。

### 我可以验证水印和背景文字吗？
是的，GroupDocs.Signature 可以验证各种类型的文本签名，包括水印和背景文本，具体取决于它们在文档中的实现方式。

### 相关资源
* [GroupDocs.Signature API 参考](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature 下载](https://releases.groupdocs.com/signature/net/)
* [GitHub 上的代码示例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [文档](https://docs.groupdocs.com/signature/net/)
* [产品页面](https://products.groupdocs.com/signature/net/)
* [博客文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [支持论坛](https://forum.groupdocs.com/c/signature/13)
* [临时执照](https://purchase.groupdocs.com/temporary-license/)