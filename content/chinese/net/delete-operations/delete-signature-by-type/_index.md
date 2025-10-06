---
"description": "了解如何使用 GroupDocs.Signature for .NET 轻松从文档中删除特定类型的签名。只需几分钟即可掌握签名管理！"
"linktitle": "按类型删除签名"
"second_title": "GroupDocs.签名 .NET API"
"title": "如何在 .NET 中按类型删除文档签名"
"url": "/zh/net/delete-operations/delete-signature-by-type/"
"weight": 12
type: docs
---
# 如何在 .NET 中按类型删除文档签名

## 为什么签名管理在文档处理中如此重要

在当今文档驱动的商业世界中，高效管理数字签名至关重要，也可能影响您的工作流程。无论您是处理需要多次审批的合同、处理法律文件，还是维护合规记录，掌控文档中的签名都至关重要。GroupDocs.Signature for .NET 恰好能帮您解决这一难题，它提供了一种简单易用的签名管理方法，包括按类型选择性地删除签名。

想一想：您有多少次需要更新文档，删除过期的二维码或数字签名，同时保留其他内容？我们将向您展示如何用最少的代码实现这一点，帮助您简化文档管理流程。

## 开始之前你需要什么

在深入研究代码之前，请确保一切准备就绪：

- 对 C# 编程有基本的了解（不用担心，我们的示例对初学者很友好）
- 安装在项目中的 GroupDocs.Signature for .NET（下载 [这里](https://releases.groupdocs.com/signature/net/))
- Visual Studio 或您首选的 .NET 开发环境
- 包含您想要删除的签名的示例文档（我们将使用包含多种签名类型的文档进行演示）

## 设置项目环境

首先，让我们导入必要的命名空间以访问 GroupDocs.Signature 所需的所有功能：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

这些导入使我们能够访问整个过程中所需的核心签名操作工具和文档处理功能。

## 步骤 1：您的文件位于何处？

让我们首先定义文档的位置以及您想要保存修改版本的位置：

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
string outputFilePath = Path.Combine("Your Document Directory", "DeleteBySignatureType", fileName);
```

请记住将“您的文档目录”替换为您存储文档的实际文件夹路径。此设置可确保您的原始文件在我们进行复制时保持完整。

## 步骤2：创建文档的工作副本

删除签名时，最好保留原始文档。以下是我们在进行任何更改之前创建备份的方法：

```csharp
File.Copy(filePath, outputFilePath, true);
```

这行简单的代码会创建文档的副本，以便我们可以安全地进行修改。“true”参数确保我们覆盖所有同名的现有文件，从而每次运行代码时都能获得全新的效果。

## 步骤3：删除不需要的签名

现在来看看主要事件——让我们初始化 GroupDocs.Signature 对象并告诉它要删除哪些签名类型：

```csharp
using (Signature signature = new Signature(outputFilePath))
{
    DeleteResult result = signature.Delete(SignatureType.QrCode);
```

在此示例中，我们的目标是删除二维码签名。需要删除其他类型吗？只需替换 `SignatureType.QrCode` 使用适当的类型，例如：
- `SignatureType.Text` 用于基于文本的签名
- `SignatureType.Image` 用于图像签名
- `SignatureType.Digital` 用于数字证书签名
- `SignatureType.Barcode` 用于标准条形码

## 步骤 4：验证文档中发生了哪些更改

删除签名后，准确了解删除的内容会很有帮助。让我们添加一些代码来提供反馈：

```csharp
if (result.Succeeded.Count > 0)
{
    Console.WriteLine("Successfully removed the following QR-Code signatures:");
    int number = 1;
    foreach (QrCodeSignature temp in result.Succeeded)
    {
        Console.WriteLine($"Signature #{number++}: Type: {temp.SignatureType} Id:{temp.SignatureId}, Text: {temp.Text}");
    }
}
else
{
    Console.WriteLine("No QR-Code signatures were found to delete in this document.");
}
```

这可以让您清楚地确认哪些签名已被删除，包括其详细信息 - 在处理批量文档或需要跟踪更改以达到合规性目的时非常有用。

## 控制您的文档签名

管理文档中的签名并非易事。GroupDocs.Signature for .NET 为您提供强大的工具，让您可以根据签名类型选择性地删除签名。当您需要更新文档、删除过期的审批或为新的签名周期准备模板时，此功能非常有用。

最好的部分？您可以将此功能直接集成到您现有的文档管理系统中，为您的团队或客户创建无缝的工作流程。

准备好将您的文档处理提升到一个新的水平了吗？不妨在您的下一个项目中尝试一下这段代码，体验一下程序化签名管理的高效性。

## 关于删除签名的常见问题

### 我可以一次删除多种类型的签名吗？
是的！您可以串联多个删除操作，也可以使用签名类型集合一次性删除多个类型。例如：
```csharp
DeleteResult result = signature.Delete(new[] { SignatureType.QrCode, SignatureType.Barcode });
```

### GroupDocs.Signature for .NET 支持哪些文档格式？
该库支持多种格式，包括 PDF、Word 文档 (DOC、DOCX)、Excel 电子表格 (XLS、XLSX)、PowerPoint 演示文稿 (PPT、PPTX)、图像等等。无论文件类型如何，都能满足您的文档管理需求。

### 我可以根据内容或其他属性过滤要删除的签名吗？
当然！GroupDocs.Signature 提供高级选项，可根据签名内容、位置、外观和其他属性进行定向删除。您可以制定特定的条件，精确控制哪些签名需要删除。

### 有没有办法在购买之前试用 GroupDocs.Signature？
是的，您可以从下载免费试用版 [GroupDocs 网站](https://releases.groupdocs.com/) 在做出决定之前探索所有特征。

### 如果我遇到签名删除问题，我可以在哪里获得帮助？
GroupDocs 社区非常活跃，并且乐于提供帮助。请访问 [GroupDocs.Signature 论坛](https://forum.groupdocs.com/c/signature/13) 寻求开发团队和其他用户的帮助。