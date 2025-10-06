---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 将 GS1DotCode 和 HanXin QR Code 签名集成到您的文档中。增强安全性并简化工作流程。"
"title": "使用 GroupDocs.Signature for .NET 对 GS1DotCode 和 HanXin QR 码进行安全文档签名"
"url": "/zh/net/barcode-signatures/sign-documents-gs1dotcode-hanxin-qr-groupdocs-signature-dotnet/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature for .NET 对 GS1DotCode 和 HanXin QR 码进行安全文档签名
## 如何使用 GroupDocs.Signature for .NET 签署带有 GS1DotCode 和 HanXin QR 码的文档
在当今的数字时代，安全地以电子方式签署文档至关重要。无论您是商务人士还是希望实现工作流程自动化的开发人员，集成条形码和二维码签名都能增强安全性并简化流程。本教程将指导您使用 GroupDocs.Signature for .NET 在应用程序中实现 GS1DotCode 和汉信二维码签名。
## 您将学到什么
- 将 GroupDocs.Signature for .NET 集成到您的项目中。
- 使用 GS1DotCode 条形码签署文件。
- 实现汉信二维码签名。
- 列出签署文件后新创建的签名。
- 了解实际应用和性能考虑因素。
准备好增强您的文档工作流程了吗？让我们开始吧！
## 先决条件
开始之前，请确保您已具备以下条件：
### 所需库
- **适用于 .NET 的 GroupDocs.Signature**：此库允许您使用不同的条形码和二维码格式签署各种类型的文档。
### 环境设置要求
- 使用兼容的 .NET 环境（最好是 .NET Core 或 .NET Framework 4.7.2+）。
- 如果您正在使用桌面应用程序，请安装 Visual Studio。
### 知识前提
- 对 C# 和 .NET 开发有基本的了解。
- 熟悉使用 NuGet 包进行依赖项管理。
## 为 .NET 设置 GroupDocs.Signature
首先安装 GroupDocs.Signature 库：
**使用 .NET CLI**
```bash
dotnet add package GroupDocs.Signature
```
**程序包管理器控制台**
```powershell
Install-Package GroupDocs.Signature
```
**NuGet 包管理器 UI**： 
搜索“GroupDocs.Signature”并安装最新版本。
### 许可证获取步骤
- **免费试用**：下载试用版来测试功能。
- **临时执照**：申请临时许可证以进行延长评估。
- **购买**：如果您准备在生产中部署，请购买完整许可证。
#### 基本初始化
要初始化 GroupDocs.Signature，请创建一个实例 `Signature` 类与您的文档路径：
```csharp
using (Signature signature = new Signature("your-document-path"))
{
    // 您的签名代码在这里
}
```
## 实施指南
让我们逐步分解如何实现每个功能。
### 使用 GS1DotCode 条形码签署文件
**概述**：将 GS1DotCode 条形码添加到您的文档中，这是供应链和库存管理的热门选择。
#### 步骤1：初始化签名对象
创建一个实例 `Signature` 使用源文件路径：
```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY"))
{
    // 代码继续...
}
```
#### 步骤 2：配置 GS1DotCode 选项
设置条形码选项，包括内容、格式和尺寸。
```csharp
var gs1DotCodeOptions = new BarcodeSignOptions(
    "(01)04912345123459(15)970331(30)128(10)ABC123", 
    BarcodeTypes.GS1DotCode)
{
    Left = 1,
    Top = 1,
    Height = 150,
    Width = 200,
    ReturnContent = true, // 检索签名图像的内容
    ReturnContentType = FileType.PNG // 输出为 PNG
};
```
#### 步骤 3：签署并保存文档
执行签名流程，并将结果保存到指定路径。
```csharp
var signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY/AdvancedBarCodeTypes.pptx", gs1DotCodeOptions);
```
### 使用汉信二维码签署文件
**概述**：在您的文档中嵌入汉信二维码，广泛用于安全数据共享。
#### 步骤1：初始化签名对象
与条形码设置类似，初始化 `Signature`：
```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY"))
{
    // 代码继续...
}
```
#### 步骤2：配置汉信二维码选项
使用内容和外观设置定义您的二维码选项。
```csharp
var hanXinOptions = new QrCodeSignOptions(
    "(01)04912345123459(15)970331(30)128(10)ABC123", 
    QrCodeTypes.HanXin)
{
    Left = 201,
    Top = 1,
    Height = 200,
    Width = 200,
    ReturnContent = true, // 检索签名图像的内容
    ReturnContentType = FileType.PNG // 输出为 PNG
};
```
#### 步骤 3：签署并保存文档
继续签署并存储您的文件。
```csharp
var signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY/AdvancedQRCodeTypes.pptx", hanXinOptions);
```
### 列出新创建的签名
**概述**：通过列出签名后的内容来验证所添加的签名。
#### 实施步骤：
1. **初始化签名对象**：就像以前的功能一样。
2. **列出并输出签名**：使用一种方法来遍历已签名的项目。
```csharp
void ListNewSignatures(SignResult signResult)
{
    Console.WriteLine("\nList of newly created signatures:");
    int number = 1;
    foreach (var item in signResult.Succeeded)
    {
        switch (item)
        {
            case BarcodeSignature barcodeSignature:
                string barOutputImagePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", $"image{number}{barcodeSignature.Format.Extension}");
                using (FileStream fs = new FileStream(barOutputImagePath, FileMode.Create))
                {
                    fs.Write(barcodeSignature.Content, 0, barcodeSignature.Content.Length);
                }
                number++;
                break;
            case QrCodeSignature qrCodeSignature:
                string qrOutputImagePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", $"image{number}{qrCodeSignature.Format.Extension}");
                using (FileStream fs = new FileStream(qrOutputImagePath, FileMode.Create))
                {
                    fs.Write(qrCodeSignature.Content, 0, qrCodeSignature.Content.Length);
                }
                number++;
                break;
        }
    }
}
```
## 实际应用
- **供应链管理**：使用 GS1DotCode 跟踪产品从制造到零售的整个过程。
- **安全数据共享**：实施汉信二维码，实现商业文件中信息的加密共享。
- **自动发票处理**：使用条形码简化发票验证和批准流程。
## 性能考虑
使用 GroupDocs.Signature 时，请考虑以下提示：
- **优化资源使用**：及时关闭流并释放资源，避免内存泄漏。
- **并行处理**：尽可能使用异步方法或并行处理以获得更好的性能。
- **内存管理**：定期分析您的应用程序以确保有效使用.NET 的垃圾收集器。
## 结论
在本教程中，您学习了如何使用 GroupDocs.Signature for .NET 实现 GS1DotCode 条形码和 HanXin 二维码。这些工具可以显著提高文档工作流程的安全性和效率。
### 后续步骤
- 尝试 GroupDocs.Signature 提供的不同条形码类型。
- 探索与其他系统（如 CRM 或 ERP 解决方案）的集成。
准备好在您的应用程序中签署文档了吗？立即尝试实现这些功能！
## 常见问题解答部分
1. **什么是适用于 .NET 的 GroupDocs.Signature？**
   - 一个在 .NET 应用程序中启用数字签名功能的库，支持各种文档格式和签名类型。
2. **我可以将其他条形码格式与 GroupDocs.Signature 一起使用吗？**
   - 是的，它支持多种条形码标准，包括二维码、Code 128、PDF417 等。
3. **如何处理签名过程中的错误？**
   - 实施异常处理 `Sign` 方法调用来优雅地管理潜在的错误。
4. **在大型文档中添加条形码会对性能产生影响吗？**
   - 虽然添加条形码通常很有效，但性能会根据文档的大小和复杂性而有所不同。