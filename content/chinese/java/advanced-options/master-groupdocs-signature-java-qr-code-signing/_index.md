---
categories:
- Java Development
date: '2026-05-21'
description: 了解如何在 PDF 中使用 GroupDocs.Signature for Java 生成 QR Code Java 签名。包括 Maven
  设置、定位技巧和生产最佳实践。
keywords:
- generate qr code java
- java generate qr code
- groupdocs signature java
lastmod: '2026-05-21'
linktitle: QR Code Java 签名指南
schemas:
- author: GroupDocs
  dateModified: '2026-05-21'
  description: Learn how to generate qr code java signatures in PDFs using GroupDocs.Signature
    for Java. Includes Maven setup, positioning tips, and production best practices.
  headline: 'generate qr code java: Complete QR Code Signing Guide'
  type: TechArticle
- description: Learn how to generate qr code java signatures in PDFs using GroupDocs.Signature
    for Java. Includes Maven setup, positioning tips, and production best practices.
  name: 'generate qr code java: Complete QR Code Signing Guide'
  steps:
  - name: Use absolute paths or ensure the working directory is correct.
    text: Use absolute paths or ensure the working directory is correct.
  - name: Confirm read permissions for the source and write permissions for the output
      folder.
    text: Confirm read permissions for the source and write permissions for the output
      folder.
  - name: Escape any special characters in the path.
    text: Escape any special characters in the path.
  - name: '**Batch Processing** – process documents in parallel, but cap concurrency
      based on RAM.'
    text: '**Batch Processing** – process documents in parallel, but cap concurrency
      based on RAM.'
  - name: '**Caching** – reuse identical `QrCodeSignOptions` objects across documents.'
    text: '**Caching** – reuse identical `QrCodeSignOptions` objects across documents.'
  - name: '**Async Operations** – move signing to background workers for responsive
      APIs.'
    text: '**Async Operations** – move signing to background workers for responsive
      APIs.'
  - name: '**Memory Monitoring** – set alerts for spikes and tune batch size accordingly.'
    text: '**Memory Monitoring** – set alerts for spikes and tune batch size accordingly.'
  - name: Verify the output file is actually created.
    text: Verify the output file is actually created.
  - name: Confirm you’re opening the correct output file.
    text: Confirm you’re opening the correct output file.
  - name: Check `SignResult` for a success count.
    text: Check `SignResult` for a success count.
  type: HowTo
- questions:
  - answer: GroupDocs.Signature for Java
    question: What library adds QR code signatures in Java?
  - answer: Maven (see *maven dependency groupdocs*)
    question: Which build tool supports the Maven dependency?
  - answer: Yes, using alignment and page‑number options
    question: Can I position QR codes on specific pages?
  - answer: Yes, a commercial GroupDocs license is required
    question: Do I need a license for production?
  - answer: Absolutely, when sized ≥ 100 × 100 px and placed with proper margins
    question: Is the QR code scannable after signing?
  type: FAQPage
tags:
- QR codes
- PDF signing
- digital signatures
- document security
title: 生成 QR Code Java：完整的 QR Code 签名指南
type: docs
url: /zh/java/advanced-options/master-groupdocs-signature-java-qr-code-signing/
weight: 1
---

# 生成 QR 码 Java：完整的 QR 码签名指南

在本教程中，您将学习如何在 PDF 文档中使用 GroupDocs.Signature for Java **generate qr code java** 签名。我们将演示如何添加 QR 码、精确定位以及避免大多数开发者常犯的陷阱。无论您是构建合同管理平台还是安全的发票流水线，本指南都为您提供可投入生产的解决方案。

## 快速答案
- **什么库在 Java 中添加 QR 码签名？** GroupDocs.Signature for Java  
- **哪个构建工具支持 Maven 依赖？** Maven (see *maven dependency groupdocs*)  
- **我可以在特定页面上定位 QR 码吗？** 是的，使用对齐和页码选项  
- **生产环境需要许可证吗？** 是的，需要商业 GroupDocs 许可证  
- **签名后 QR 码可以扫描吗？** 当然，只要尺寸 ≥ 100 × 100 px 且放置有适当的边距  

## 您将学习的内容

通过本指南，您将了解如何：

- 在您的 Java 项目中设置 QR 码签名（Maven、Gradle 或直接下载）  
- 在文档的精确位置添加 QR 码（角落、中心、自定义对齐）  
- 在问题演变为生产问题之前处理常见实现问题  
- 为高吞吐量文档工作流优化性能  
- 将这些技术应用于真实的业务场景  

## 前置条件

在深入代码之前，请确保您拥有：

- **GroupDocs.Signature for Java** – 版本 23.12 或更高（我们将在下文介绍安装）  
- **Java Development Kit** – JDK 8 或更高（大多数生产环境使用 JDK 11+）  
- **Build Tool** – 用于依赖管理的 Maven 或 Gradle  
- **Basic Java Knowledge** – 熟悉 try‑catch 块和文件路径处理  

如果您是 GroupDocs 新手，请不要担心——我们将一步步演示所有内容。

## 设置您的环境

将 GroupDocs.Signature 引入项目非常简单。请选择与您的构建系统匹配的方法。

### 使用 Maven

将此 **maven dependency groupdocs** 添加到您的 `pom.xml` 文件中：

``` 
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

添加后，运行 `mvn clean install` 下载库。

### 使用 Gradle

对于 Gradle 项目，将此行添加到您的 `build.gradle`：

``` 
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

然后使用 `gradle build` 同步项目。

### 直接下载选项

更喜欢手动安装？直接从 [GroupDocs.Signature for Java 发行版](https://releases.groupdocs.com/signature/java/) 下载 JAR 并将其添加到项目的类路径中。

### 许可证设置（重要！）

有一点常常让人意外：GroupDocs 需要生产使用的许可证。选项如下：

- **Free Trial** – 完整功能，有限时间  
- **Temporary License** – 需要更多时间？获取 [temporary license](https://purchase.groupdocs.com/temporary-license/) 进行延长测试  
- **Commercial License** – 用于生产部署，[purchase a license](https://purchase.groupdocs.com/buy)

试用版会添加水印，请在演示时相应安排。

## 基本初始化

`Signature` 是 GroupDocs.Signature for Java 的主要入口类，用于加载和操作文档进行签名。安装库后，初始化它只需指向您的文档：

``` 
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```
```

这将创建一个可供使用的 `Signature` 对象。

## 理解 QR 码签名

QR 码签名将可验证的数据（如时间戳、签署者身份或验证 URL）嵌入文档内可扫描的 QR 图像中。扫描后，QR 码会将用户引导至验证门户或显示嵌入的元数据，实现无需特殊软件的快速移动验证。

**何时使用 QR 码签名？**

- 快速移动验证（使用手机扫描）  
- 可能被打印的纸质副本  
- 嵌入指向验证门户的链接  
- 支持离线验证工作流  

## 实施指南：添加 QR 码签名

下面是代码的实际应用。我们将在 PDF 上签署 QR 码，并将其定位在页面的不同位置。

### 为什么定位很重要

正确的定位可确保 QR 码易于扫描，符合法律标准，并且不会遮挡重要文档内容。对于合同，通常放在右下角；对于发票，右上角效果最佳；对于证书，底部居中提供整洁外观。

### 步骤实现

#### 1. 配置文件路径

定义源文档所在位置以及签名后保存的位置：

``` 
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String fileName = Paths.get(filePath).getFileName().toString();
String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignWithAlignment/" + fileName).getPath();
```
```

**技巧提示：** 使用 `Paths.get()` 而不是字符串拼接来处理文件路径——它会自动处理操作系统特定的分隔符。

#### 2. 初始化 Signature 对象

将初始化代码放在 try‑catch 块中，以处理可能的文件访问问题：

``` 
```java
try {
    Signature signature = new Signature(filePath);
    // Signing logic goes here...
} catch (Exception e) {
    throw new RuntimeException("Error initializing signature: " + e.getMessage(), e);
}
```
```

`RuntimeException` 在调试时提供上下文信息，可在生产环境节省时间。

#### 3. 定义 QR 码大小和位置

`QrCodeSignOptions` 配置将放置在文档上的 QR 图像。它允许设置大小、边距和对齐方式。

``` 
```java
int qrWidth = 100;
int qrHeight = 100;
List<SignOptions> listOptions = new ArrayList<>();

for (int horizontalAlignment : HorizontalAlignment.getValues()) {
    for (int verticalAlignment : VerticalAlignment.getValues()) {
        if (verticalAlignment != VerticalAlignment.None && horizontalAlignment != HorizontalAlignment.None) {
            QrCodeSignOptions options = new QrCodeSignOptions("Left-Top");
            options.setWidth(qrWidth);
            options.setHeight(qrHeight);
            options.setHorizontalAlignment(horizontalAlignment);
            options.setVerticalAlignment(verticalAlignment);
            options.setMargin(new Padding(5));
            listOptions.add(options);
        }
    }
}
```
```

该循环为每个水平（左、居中、右）和垂直（上、居中、下）对齐创建 QR 码选项，并添加 5 像素的边距，确保代码永不触及页面边缘。

对于大多数生产场景，您会选择单一位置，例如合同的右下角：

``` 
```java
QrCodeSignOptions options = new QrCodeSignOptions("Signature");
options.setWidth(100);
options.setHeight(100);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setMargin(new Padding(10));
```
```

#### 4. 对文档进行签名

现在我们一次性应用所有配置好的签名：

``` 
```java
SignResult signResult = signature.sign(outputFilePath, listOptions);
```
```

`sign()` 方法会处理列表中的每个 QR 码并将结果保存到输出路径。它返回一个 `SignResult` 对象，告知成功添加的签名数量——非常适合日志记录。

**性能提示：** 签名是同步的。对于高负载工作（每小时数百份文档），请将其放在后台作业队列中运行，而不是在用户请求中直接执行。

## 常见陷阱及解决方案

### 问题 1：“文件未找到”错误

**症状：** 即使文件存在仍抛出文件未找到异常。  

**解决方案：** 检查以下三点：  
1. 使用绝对路径或确保工作目录正确。  
2. 确认源文件的读取权限以及输出文件夹的写入权限。  
3. 对路径中的特殊字符进行转义。

``` 
```java
// Better approach: Use absolute paths
String absolutePath = new File(filePath).getAbsolutePath();
Signature signature = new Signature(absolutePath);
```
```

### 问题 2：QR 码覆盖文档内容

**症状：** QR 码覆盖重要文字或在页面边缘被截断。  

**解决方案：** 增大边距值，并选择将代码放在空白区域的对齐方式：

``` 
```java
options.setMargin(new Padding(20)); // Increase from 5 to 20 pixels
```
```

### 问题 3：大文档的内存问题

**症状：** 处理超过 10 MB 的 PDF 时出现 `OutOfMemoryError`。  

**解决方案：** 及时释放 `Signature` 对象，并批量处理大文件：

``` 
```java
try (Signature signature = new Signature(filePath)) {
    // Your signing code
} // Automatically closes and releases resources
```
```

try‑with‑resources 语句即使在异常情况下也能保证资源清理。

### 问题 4：QR 码内容未更新

**症状：** 所有 QR 码显示相同文本，即使尝试自定义。  

**解决方案：** 为每个位置创建 **新** 的 `QrCodeSignOptions` 实例，而不是复用同一个对象：

``` 
```java
// Wrong - reuses same object
QrCodeSignOptions options = new QrCodeSignOptions("Text");
options.setHorizontalAlignment(HorizontalAlignment.Left);
listOptions.add(options);
options.setHorizontalAlignment(HorizontalAlignment.Right); // Modifies existing!
listOptions.add(options);

// Correct - creates new object each time
listOptions.add(new QrCodeSignOptions("Left"));
listOptions.add(new QrCodeSignOptions("Right"));
```
```

## 实际应用

### 1. 合同管理系统

工作流：生成合同 PDF → 添加包含合同 ID、时间戳、签署者哈希的 QR 码 → 安全存储 → 用户扫描 QR → 门户显示合同详情。这样法律团队即可即时从纸质副本验证真实性。

### 2. 发票处理自动化

在每张处理过的发票右上角添加 QR 码，编码发票号、供应商 ID 和处理时间戳。统一位置使自动扫描仪能够快速定位代码，提高审计速度。

### 3. 文档认证

在证书底部居中放置 QR 码，包含验证 URL 和证书 ID。接收者可扫描确认凭证，同时为非移动用户提供打印的 URL。

### 4. 内部文档追踪

在多阶段审批过程中，在每次签署后嵌入 QR 码，包含审批人 ID、时间戳和版本。扫描后可显示完整审批历史，满足合规审计需求。

## 生产最佳实践

### 资源管理

始终关闭 `Signature` 对象以防止内存泄漏：

``` 
```java
try (Signature signature = new Signature(filePath)) {
    // Your code
} // Auto‑closes
```
```

对于 Web 应用，考虑使用处理池来限制并发操作。

### 错误处理策略

提供可操作的错误信息，而不是静默捕获：

``` 
```java
try {
    SignResult result = signature.sign(outputFilePath, listOptions);
    if (result.getSucceeded().size() < listOptions.size()) {
        logger.warn("Only {} of {} signatures applied",
                    result.getSucceeded().size(),
                    listOptions.size());
    }
} catch (Exception e) {
    logger.error("Signature failed for document: {}", filePath, e);
    // Implement retry logic or alert mechanism
}
```
```

### 性能优化

针对高吞吐量环境：  

1. **批处理** – 并行处理文档，但根据内存限制并发数。  
2. **缓存** – 在文档之间复用相同的 `QrCodeSignOptions` 对象。  
3. **异步操作** – 将签名移至后台工作者，以实现响应式 API。  
4. **内存监控** – 对峰值设置警报，并相应调整批量大小。

### 安全注意事项

- 将签名文档与原始文档分开存储。  
- 记录每一次签名操作以便审计追踪。  
- 对签名端点实施严格的访问控制。  
- 在需要时加密敏感的 QR 负载。

## 何时使用 QR 码签名（以及何时不使用）

**使用 QR 码签名的场景：**  

- 需要移动友好的验证。  
- 文档可能被打印并重新扫描。  
- 需要嵌入验证 URL 或 ID。  
- 过程包含离线验证工作流。

**避免使用 QR 码签名的场景：**  

- 必须使用具有法律约束力的 PKI 签名（改用加密签名）。  
- 打印过程中 QR 码可能受损或被遮挡。  
- 验证系统完全离线。  
- 文档大小是关键限制（每个 QR 码约增加 5‑20 KB）。

**最佳实践：** 将加密签名与 QR 码结合，既获得法律效力，又实现快速移动验证。

## 故障排除指南

### 签名未出现

1. 验证输出文件是否真的已创建。  
2. 确认打开的是正确的输出文件。  
3. 检查 `SignResult` 的成功计数。  
4. 确保对齐和边距值没有将 QR 码推到页面之外。

### QR 码无法扫描

- 保持 QR 大小 ≥ 100 × 100 px。  
- 使用高对比度（深色码在浅色背景上）。  
- 将编码数据限制在 < 100 字符，以确保可靠扫描。  
- 对纸质副本以 ≥ 300 dpi 打印。

### 性能下降

- 减少每份文档的 QR 码数量。  
- 尽可能复用 `Signature` 实例。  
- 对内存使用进行分析；考虑以更小的批次处理。

## 常见问题

**问：** *我可以签署除 PDF 之外的文档吗？*  
**答：** 可以。GroupDocs.Signature 支持 Word（DOC/DOCX）、Excel（XLS/XLSX）、PowerPoint（PPT/PPTX）以及图像格式（JPG、PNG、TIFF）。API 在所有支持的类型中保持一致。

**问：** *如何自定义 QR 码外观？*  
**答：** 使用 `QrCodeSignOptions` 的属性，如 `setForeColor()`、`setBackgroundColor()` 和 `setBorder()`。保持自定义简洁，以维持可扫描性。

**问：** *我可以在多页文档的特定页面添加 QR 码吗？*  
**答：** 当然。使用 `options.setPageNumber(pageNumber);` 设置页码。例如：

``` 
```java
options.setPageNumber(1); // Add to first page only
```
```

**问：** *我可以在 QR 码中编码哪些数据？*  
**答：** 任意文本、URL、JSON 或 XML——最好控制在 200 字符以内以确保可靠扫描。对于更大的负载，可编码指向服务器上完整数据的短 URL。

**问：** *如何以编程方式验证 QR 码签名？*  
**答：** GroupDocs.Signature 提供 `verify` 方法。例如：

``` 
```java
VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    // Signature is authentic
}
```
```

`Signature` 类是对文档应用签名的主要入口点。

**问：** *我可以在多线程环境中使用吗？*  
**答：** 可以，但每个线程需要实例化单独的 `Signature` 对象——实例不是线程安全的。对于高并发场景，请使用处理队列。

**问：** *添加 QR 码对文件大小的影响如何？*  
**答：** 很小——每个 QR 码通常增加 5‑20 KB，具体取决于大小和内容。对大多数 PDF 来说几乎可以忽略不计，但在批量签署成千上万页时需考虑此因素。

---

**最后更新：** 2026-05-21  
**测试环境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs  

## 资源

- [GroupDocs.Signature for Java 发行版](https://releases.groupdocs.com/signature/java/)  
- [临时许可证](https://purchase.groupdocs.com/temporary-license/)  
- [购买许可证](https://purchase.groupdocs.com/buy)  
- [GroupDocs 文档](https://docs.groupdocs.com/signature/java/)  
- [GroupDocs.Signature Java 文档](https://docs.groupdocs.com/signature/java/)  
- [完整 API 参考](https://reference.groupdocs.com/signature/java/)  
- [最新 Java 发行版](https://releases.groupdocs.com/signature/java/)  
- [购买 GroupDocs.Signature](https://purchase.groupdocs.com/buy)  
- [开始免费试用](https://releases.groupdocs.com/signature/java/)  
- [获取临时许可证](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs 论坛](https://forum.groupdocs.com/c/signature/)

## 相关教程

- [Java QR 码签名库 - 完整 GroupDocs 教程](/signature/java/qr-code-signatures/)
- [在 Java 中提取 QR 码数据 - 完整指南（使用 GroupDocs）](/signature/java/qr-code-signatures/detect-qr-code-mecard-signatures-groupdocs-java/)
- [从 PDF 中移除 QR 码（Java） - 完整指南（使用 GroupDocs）](/signature/java/signature-management/delete-qr-code-signatures-groupdocs-java/)