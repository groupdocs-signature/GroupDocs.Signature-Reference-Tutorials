---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 为 Excel 电子表格签名二维码，并将其保存为多种格式。高效保护您的文档安全。"
"title": "使用 GroupDocs.Signature 在 Java 中对带有二维码的 Excel 电子表格进行签名和保存"
"url": "/zh/java/qr-code-signatures/sign-save-spreadsheets-java-qr-codes-groupdocs-signature/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature 在 Java 中对带有二维码的 Excel 电子表格进行签名和保存

## 介绍

在当今的数字时代，确保文件的真实性比以往任何时候都更加重要。无论您处理的是合同、协议还是财务电子表格，安全签名文件都能节省时间并防止欺诈。 **GroupDocs.Signature for Java** 是一个功能强大的库，可以简化各种文档格式的电子签名。本教程将指导您使用 GroupDocs.Signature 对带有二维码的 Excel 电子表格进行签名，并将其保存为不同的格式。

### 您将学到什么：
- 如何使用二维码签名签署电子表格。
- 以多种输出格式保存签名的文件，如 PDF、XLSX 等。
- 处理文档签名时优化 Java 应用程序的性能。

完成本教程后，您将对如何在 Java 应用程序中集成和使用 GroupDocs.Signature 执行签名任务有深入的理解。在开始实现这些功能之前，让我们先深入了解一下必要的工具设置！

## 先决条件

在继续本指南之前，请确保您已具备以下条件：
- **Java 开发工具包 (JDK)** 安装在您的机器上。
- 具备 Java 编程基础知识并熟悉 Maven 或 Gradle 构建系统。
- 像 IntelliJ IDEA、Eclipse 或 NetBeans 这样的 IDE。

此外，您需要在项目中为 Java 设置 GroupDocs.Signature。设置过程非常简单，可以使用 Maven 或 Gradle 依赖项来实现，如下所示：

## 为 Java 设置 GroupDocs.Signature

首先，将 GroupDocs.Signature 依赖项添加到项目的构建文件中。

### Maven
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

或者，您可以直接从 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

#### 许可证获取
要充分利用 GroupDocs.Signature 的功能：
- **免费试用**：从免费试用开始探索基本功能。
- **临时执照**：在评估期间获取临时许可证以获得完全访问权限。
- **购买**：为了长期使用，请考虑购买商业许可证。

### 基本初始化和设置
初始化 `Signature` 通过传递文档文件路径来分类，如下所示：
```java
import com.groupdocs.signature.Signature;

// 使用文档路径进行初始化
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SampleSpreadsheet.xlsx");
```

## 实施指南
在本节中，我们将介绍使用 GroupDocs.Signature 签署电子表格并保存的步骤。

### 使用二维码签署电子表格
#### 概述
此功能允许您在 Excel 电子表格中添加二维码签名。它对于添加易于扫描的安全电子标识符特别有用。
##### 步骤 1：定义文件路径
首先定义输入和输出文件的路径：
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleSpreadsheet.xlsx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signedDocument.pdf";
```
##### 步骤2：初始化签名对象
创建一个 `Signature` 对象与您的文档的文件路径。
```java
Signature signature = new Signature(filePath);
```
##### 步骤 3：创建二维码签名选项
配置二维码签名选项。指定二维码的文本、类型和位置等属性：
```java
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100); // X坐标
signOptions.setTop(100);  // Y坐标
```
##### 步骤 4：配置保存选项
指定已签名文档的保存方式，包括其格式：
```java
import com.groupdocs.signature.options.saveoptions.SpreadsheetSaveOptions;
import com.groupdocs.signature.domain.enums.SpreadsheetSaveFileFormat;

SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions();
saveOptions.setFileFormat(SpreadsheetSaveFileFormat.Pdf);
saveOptions.setOverwriteExistingFiles(true);
```
##### 步骤 5：签署并保存文档
最后，使用 `sign` 应用二维码签名并保存文档的方法：
```java
try {
    signature.sign(outputFilePath, signOptions, saveOptions);
} catch (Exception e) {
    e.printStackTrace();
}
```
### 将文档保存为不同的输出文件格式
#### 概述
GroupDocs.Signature 允许您将签名的文档保存为各种格式，例如 PDF、XLSX 和 DOCX。
##### 步骤 1：定义输出路径
指定所需的输出文件路径和格式：
```java
String outputPath = "YOUR_OUTPUT_DIRECTORY/signedDocument.pdf"; // 根据需要更改格式
```
##### 第 2 步：设置保存选项
配置 `SpreadsheetSaveOptions` 定义文档的保存方式：
```java
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions();
saveOptions.setFileFormat(SpreadsheetSaveFileFormat.Pdf); // 可以改变为不同的格式
saveOptions.setOverwriteExistingFiles(true);
```
##### 步骤3：实施签名操作
在签名操作中使用这些选项。确保 `signature` 对象已正确初始化：
```java
// 使用示例（假设签名对象存在）
signature.sign(outputPath, signOptions, saveOptions);
```
## 实际应用
以下是此功能可以发挥作用的一些实际场景：
- **法律文件**：使用二维码安全签署合同，以便于验证。
- **财务报告**：向包含敏感财务数据的电子表格添加签名。
- **库存管理**：在库存表上使用二维码，以简化跟踪和身份验证。

## 性能考虑
处理文档签名时，请考虑以下提示：
- 通过分析签名操作期间的资源使用情况来优化 Java 内存管理。
- GroupDocs.Signature 针对性能进行了优化，但请确保您在合适的环境中运行它以有效地处理大型文档。

## 结论
现在，您应该已经能够熟练使用 GroupDocs.Signature 来签名并保存带有二维码的 Excel 电子表格。这款强大的工具可以显著增强您数字文档的安全性和真实性。接下来，您可以探索其他功能，例如文本签名或图章签名，以进一步保护您的文档。

**号召性用语**：立即尝试在您的项目中实施这些解决方案！

## 常见问题解答部分
1. **GroupDocs.Signature 支持哪些格式？**
   - 它支持 PDF、XLSX、DOCX 等。
2. **如何解决签名问题？**
   - 检查异常消息以寻找线索；确保所有文件路径正确。
3. **是否可以在一份文件中签署多页？**
   - 是的，在您的签名选项中指定页码。
4. **GroupDocs.Signature 可以在 Web 应用程序中使用吗？**
   - 绝对的，它非常适合服务器端 Java 应用程序。
5. **如果需要，我如何获得支持？**
   - 使用 [GroupDocs 支持论坛](https://forum.groupdocs.com/c/signature) 寻求帮助。

## 资源
- **文档**：可以在以下位置找到综合指南和 API 参考 [GroupDocs 文档](https://docs。groupdocs.com/signature/java/).
- **API 参考**：详细信息请参阅 [API 参考页面](https://reference。groupdocs.com/signature/java/).
- **下载**：访问最新版本 [GroupDocs 发布](https://releases。groupdocs.com/signature/java/).
- **购买和许可**：详细了解许可选项，请访问 [GroupDocs 购买](https://purchase.groupdocs.com/buy) 并通过以下方式获得免费试用 [GroupDocs 免费试用](http://www.groupdocs.com/pricing)