---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: 了解如何使用 GroupDocs.Signature for Java 创建 Data Matrix PDF 并添加 QR code PDF。针对医疗文档签署的分步指南。
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: HIBC PDF 签署 Java 指南
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: 在 Java 中使用 HIBC 条码创建 Data Matrix PDF
type: docs
url: /zh/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# 使用 Java 创建带 HIBC 条码的数据矩阵 PDF

如果您正在构建制药或医疗保健物流软件，可能已经遇到纸质跟踪、签名丢失和审计噩梦的难题。**创建一个嵌入 HIBC LIC 条码的数据矩阵 PDF** 能够通过提供防篡改、机器可读的痕迹来解决这些问题，该痕迹能够在打印、扫描和监管审查中保持完整。在本教程中，您将看到如何使用 GroupDocs.Signature for Java **添加 QR code PDF** 支持，以及 Aztec 和 Data Matrix 格式。

## 快速答案
- **什么库在 Java 中处理 HIBC 条码？** GroupDocs.Signature for Java。  
- **哪种条码格式最紧凑？** Data Matrix – 适用于小标签。  
- **我可以在同一个 PDF 中同时添加 QR 和 Data Matrix 吗？** 是的，只需创建单独的 `QrCodeSignOptions`。  
- **运行时需要互联网连接吗？** 不需要，库在安装后可以完全离线工作。  
- **推荐使用哪个 Java 版本？** Java 11+ 以获得生产级性能。

## 什么是 HIBC 条码 PDF 签名？
`Signature` 类在 GroupDocs.Signature for Java 中表示 PDF 文档，并提供将 HIBC 条码嵌入为数字签名的方法。通过使用 HIBC 条码对 PDF 进行签名，您可以创建可验证的、防篡改的记录，供供应链的任何环节扫描。

## 为什么要同时使用 Data Matrix 和 QR 码？
GroupDocs.Signature 支持 **50+ 输入和输出格式**，并且能够在不将整个文件加载到内存中的情况下处理数百页的 PDF。将 Data Matrix 用于密集、小面积标签，使用 QR 码用于更宽敞的文档，可为您提供可读性、数据容量（QR 最多 4,296 个字符）和打印空间效率的最佳平衡。

## 前置条件
- **JDK 11 或更高**（Java 8 也可使用，但推荐使用 Java 11+ 以获得最佳性能）。  
- **IDE** 如 IntelliJ IDEA、Eclipse 或带有 Java 扩展的 VS Code。  
- **Maven 或 Gradle** 用于依赖管理（示例见下文）。  
- **示例 PDF**（例如 `sample.pdf`）用于测试实现。  
- **有效的 GroupDocs.Signature 许可证**（开发免费试用，生产环境付费许可证）。

## 为 Java 设置 GroupDocs.Signature

### Maven 配置
将依赖添加到您的 `pom.xml` 中：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 配置
对于 Gradle 项目，将以下内容添加到您的 `build.gradle` 中：

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下载选项
您也可以直接从 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) 下载 JAR 文件，并手动将其添加到项目的 classpath 中。此方法在受限网络环境中效果良好。

### 获取许可证
向 GroupDocs 申请免费试用或临时许可证，以去除水印并解锁所有功能。生产部署需要购买许可证。

### 基本初始化
`Signature` 类是所有签名操作的入口。它加载 PDF，应用条码，并写入签名后的文件。

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## 如何使用 HIBC 条码创建 Data Matrix PDF？
加载源 PDF，配置用于 Data Matrix 格式的 `QrCodeSignOptions` 对象，然后调用 `sign()` —— 这就是嵌入符合 HIBC 标准的 Data Matrix 条码所需的全部步骤。以下步骤将逐步演示所需的完整代码。`QrCodeSignOptions` 定义条码签名的设置，例如类型、内容、大小和位置。

1. **导入所需的类** —— 这些类让您能够访问签名引擎和 Data Matrix 选项。  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **实例化 `Signature` 对象**，并使用源文件和目标文件的绝对路径。  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **配置 Data Matrix 选项** —— 设置 HIBC 字符串，选择 `QrCodeTypes.HIBCLICDataMatrix`，并定义放置坐标。`QrCodeTypes` 列举了 HIBC 签名支持的条码格式。  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **将签名应用** 到 PDF。  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **释放资源**，以关闭文件句柄并避免内存泄漏。  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### 完整工作示例
以下是单块完整流程（占位符代表您将从前面的代码片段中粘贴的实际代码）：

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### 直接答案（40–70 字）
要 **创建 Data Matrix PDF**，实例化 `Signature` 并传入源 PDF，将 `QrCodeSignOptions` 设置为 `QrCodeTypes.HIBCLICDataMatrix` 并提供正确格式的 HIBC 字符串，然后调用 `signature.sign(outputPath, options)`。库会将签名后的 PDF 写入目标位置，保留布局并将条码嵌入为防篡改签名。

## 如何使用 GroupDocs.Signature 添加 QR code PDF？
加载 PDF，配置用于 QR 格式的 `QrCodeSignOptions`，并调用 `sign()`。这种两行模式适用于任何尺寸的 PDF，并会自动缩放 QR 图像以获得最佳可读性。`QrCodeSignOptions` 配置 QR 条码签名，包括其内容和视觉属性。它根据您设置的坐标定位代码，确保不与现有内容重叠，并在打印后仍可扫描。

1. **导入 QR 专用类**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **创建并配置 QR 选项** —— 注意使用 `QrCodeTypes.HIBCLICQR`。  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **签署文档**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **直接答案：** 在 `QrCodeSignOptions` 中使用 `QrCodeTypes.HIBCLICQR`，设置 HIBC 内容字符串，使用 `setLeft()` 和 `setTop()` 定位代码，然后调用 `signature.sign(outputPath, options)`。QR 条码会立即嵌入，随时可供智能手机或扫描仪捕获。

## 常见错误需避免

### 1. 忘记释放资源
**错误：**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**修复：** 将 `Signature` 的使用包装在 try‑with‑resources 块中，或在 finally 子句中显式调用 `close()`。

### 2. 使用不正确的 HIBC 格式字符串
**错误：** 使用诸如 “12345” 的通用字符串。  
**修复：** 遵循 HIBCC 标准（例如 `A123PROD30917/75#422011907#GP293`）。使用 [HIBCC online validator](https://www.hibcc.org/) 进行验证。

### 3. 硬编码文件路径
**错误：**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  
**修复：** 将路径存储在配置文件或环境变量中，并在运行时读取。

### 4. 忽视条码位置冲突
将条码放置在现有文本或签名之外。使用 PDF 坐标系（原点在左下角），并使用打印样本进行测试。

### 5. 未使用真实扫描仪进行测试
打印签名后的 PDF，并使用工作流中实际使用的硬件进行扫描。验证在不同打印质量下的可读性。

## 医疗保健中的实际应用

| 场景 | 推荐条码 | 适用原因 |
|----------|--------------------|--------------|
| **药品分销** | QR Code | 高数据容量，智能手机广泛扫描。 |
| **库存管理** | Data Matrix | 占位小，适用于密集的货架标签。 |
| **合规监管（FDA 21 CFR Part 11）** | QR + Data Matrix | 双格式提供冗余和可审计性。 |
| **医疗器械追踪** | Aztec Code | 紧凑尺寸适用于空间受限的包装。 |

## 性能考虑与最佳实践

### 批处理模式
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- 为每个文件创建新的 `Signature` 实例，以保持内存使用低。  
- 使用固定线程池（`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`）进行并行处理，但要监控堆大小，因为每个 `Signature` 会将完整的 PDF 保存在内存中。  

### 保持库更新
GroupDocs 的更新可将处理速度提升至 **20 %**，并添加新的 HIBC 合规功能。建议每季度进行一次依赖检查。

### 缓存模板
一次加载 PDF 模板，对每种条码变体进行克隆，然后对克隆进行签名。此方式可减少 I/O 并加快大批量工作流的速度。

## 常见问题解答

**问：GroupDocs.Signature 能签署除 PDF 之外的文件类型吗？**  
答：是的，它同样支持 DOCX、XLSX、PPTX、PNG、JPEG 和 TIFF，使用相同的条码签名 API。

**问：如何排查 “Invalid barcode content” 错误？**  
答：确认您的 HIBC 字符串严格遵循 HIBCC 语法，使用在线验证器，并确保为所选格式使用了正确的 `QrCodeTypes` 常量。

**问：每种 HIBC 格式的最大数据容量是多少？**  
答：QR ≈ 4,296 个字母数字字符，Aztec ≈ 3,832 个数字 / 3,067 个字母数字，Data Matrix ≈ 3,116 个数字 / 2,335 个字母数字。为获得最佳扫描可靠性，建议将码长保持在 200 字符以下。

**问：是否可以在同一个 PDF 中嵌入多种条码类型？**  
答：完全可以。为不同位置创建单独的 `QrCodeSignOptions` 对象，并对每个对象调用 `signature.sign()`。只需确保它们不重叠即可。

**问：运行时签署是否需要互联网连接？**  
答：不需要。JAR 放入 classpath 并激活许可证后，所有操作均在本地完成。

## 其他资源

- [GroupDocs.Signature for Java 文档](https://docs.groupdocs.com/signature/java/)  
- [API 参考指南](https://reference.groupdocs.com/signature/java/)  
- [最新发布下载](https://releases.groupdocs.com/signature/java/)  
- [购买许可证](https://purchase.groupdocs.com/buy)  
- [获取免费试用](https://releases.groupdocs.com/signature/java/)  
- [请求临时许可证](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs 论坛](https://forum.groupdocs.com/c/signature/)

---

**最后更新：** 2026-05-16  
**测试环境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## 相关教程

- [在 Java 中创建条码签名 PDF – GroupDocs 指南](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [在 Java 中创建条码签名 – 更新 PDF 条码](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [如何使用 Java 和 GroupDocs.Signature 读取 QR code PDF](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)