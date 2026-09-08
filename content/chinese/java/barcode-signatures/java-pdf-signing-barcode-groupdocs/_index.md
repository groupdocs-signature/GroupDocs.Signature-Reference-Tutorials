---
categories:
- Java PDF Processing
date: '2026-07-20'
description: 了解如何使用 Java 和 GroupDocs.Signature 在 PDF 文档中创建 Barcode 签名。提供代码示例和最佳实践的分步教程。
keywords:
- create barcode signature
- how to add barcode
- generate code128 barcode
- add barcode pdf
- tamper evident barcode
lastmod: '2026-07-20'
linktitle: 创建 Barcode 签名 Java
og_description: 使用 Java 和 GroupDocs.Signature 在 PDF 中创建 Barcode 签名。分步学习如何添加 Code128
  条形码、设置位置并保护文档。
og_image_alt: 'Developer guide: Create barcode signature in PDF using Java and GroupDocs'
og_title: 使用 Java 在 PDF 中创建 Barcode 签名 – 完整指南
schemas:
- author: GroupDocs
  dateModified: '2026-07-20'
  description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  headline: How to Create Barcode Signature in PDF using Java
  type: TechArticle
- description: Learn how to create barcode signature in PDF documents using Java and
    GroupDocs.Signature. Step-by-step tutorial with code examples and best practices.
  name: How to Create Barcode Signature in PDF using Java
  steps:
  - name: Initialize the Signature object
    text: '**Definition anchor:** The `Signature` class is GroupDocs.Signature''s
      entry point for loading, modifying, and saving PDF documents. First, you need
      to tell GroupDocs which PDF you''re working with: **What''s happening here:**
      The `Signature` object loads your PDF into memory and prepares it for modifi'
  - name: Configure your barcode options (How to add barcode)
    text: '**Definition anchor:** `BarcodeSignOptions` encapsulates all settings required
      to render a barcode inside a PDF. Now let''s create the barcode signature with
      your data: - `"12345678"` is your barcode data — this could be an order ID,
      certificate number, or any identifier you need. - `Code128` is the '
  - name: Position your barcode (How to sign PDF with barcode)
    text: '**Definition anchor:** `SignatureOptions` provides layout properties such
      as page number, size, and alignment. Here''s where GroupDocs really shines —
      percentage‑based positioning means your barcode looks good on any PDF size:
      **Why percentages matter:** Imagine you''re signing both A4 documents and l'
  - name: Sign and save your document (How to add barcode pdf)
    text: 'Time to actually apply the signature and save your work: **Important note:**
      The output directory must exist before you run this code. GroupDocs won''t create
      nested directories for you, so create them first or handle that in your code:
      **What if something goes wrong?** Wrap this in a try‑catch block'
  type: HowTo
- questions:
  - answer: Yes! Call `signature.sign()` multiple times with different `BarcodeSignOptions`
      for each barcode type. Just ensure they don’t overlap.
    question: Can I use different barcode types in the same PDF?
  - answer: Code128 handles most ASCII characters fine. For Unicode or complex data,
      switch to QR codes—they support UTF‑8 encoding.
    question: How do I handle barcodes that contain special characters?
  - answer: Technically up to 128 characters, but readability drops significantly
      above 30‑40 characters. For larger payloads, use QR codes.
    question: What's the maximum data I can store in a Code128 barcode?
  - answer: Not noticeably—barcodes are vector graphics, typically adding only 5‑20
      KB per barcode depending on size and complexity.
    question: Will adding barcodes significantly increase my PDF file size?
  - answer: Yes! Use `options.setRotationAngle(90)` to rotate your barcode, which
      is handy for margin placement.
    question: Can I rotate barcodes or place them vertically?
  type: FAQPage
tags:
- pdf-signing
- barcode-signature
- document-security
- groupdocs
- java
- pdf
title: 如何使用 Java 在 PDF 中创建 Barcode 签名
type: docs
url: /zh/java/barcode-signatures/java-pdf-signing-barcode-groupdocs/
weight: 1
---

# 如何使用 Java 在 PDF 中创建条形码签名

在本教程中，您将学习如何使用 Java 和 GroupDocs.Signature 在 PDF 文件中 **创建条形码签名**。条形码签名嵌入机器可读的标识符，既防篡改又易于扫描——非常适合合同、证书、发票以及任何需要可靠验证的文档。

## 快速回答
- **条形码签名是什么？** 嵌入 PDF 的条形码，存储结构化数据，可被扫描仪或软件读取。  
- **推荐使用哪种条形码类型？** Code128，因为它能够紧凑地处理字母数字数据。  
- **我需要许可证吗？** 免费试用可用于测试；生产环境需要完整许可证。  
- **我可以在任何页面尺寸上定位条形码吗？** 可以——使用基于百分比的定位实现自动缩放。  
- **条形码是矢量化的吗？** 是的，只会向 PDF 添加几千字节，并在任何分辨率下保持清晰。  

## 什么是条形码签名？
条形码签名是一种基于矢量的条形码，直接嵌入 PDF 页面，既充当可视元素，又充当可在以后验证的加密签名。它存储结构化数据，如 ID 或时间戳，并在提供机器可读引用的同时确保文档完整性。

## 为什么条形码签名对您的 PDF 很重要
条形码签名为 PDF 提供了紧凑的机器可读标识符，可即时扫描，消除手动数据录入并降低错误。由于它们以矢量图形嵌入，任何分辨率下都保持锐利，仅增加几千字节的文件大小。这种可读性、防篡改性和最小体积的组合，使其非常适合合同、发票、证书以及任何需要可靠验证的文档。

以下是您可能遇到的挑战：需要向 PDF 添加既机器可读又防篡改的唯一标识符。也许您正在构建文档管理系统、处理证书，或处理需要后期验证的合同。

这正是条形码签名的用武之地。与简单的文字水印不同，条形码允许您嵌入结构化数据，扫描仪（以及您的软件）可以即时读取。此外，将其与 GroupDocs.Signature for Java 的 PDF 签名功能结合使用，您即可在无需复杂数据库查询的情况下实现文档追踪和验证。

在本指南中，您将学习如何在 Java PDF 中实现条形码签名——从基础设置到生产就绪代码以及灵活的定位方式。无论您是构建发票系统、证书生成器，还是合同管理平台，阅读完本教程后都能掌握所需全部内容。

**您将掌握的内容：**
- 在几分钟内设置 GroupDocs.Signature for Java  
- 创建 Code128 条形码签名（以及为何它通常是最佳选择）  
- 使用基于百分比的布局在任何 PDF 大小上定位条形码  
- 避免开发者常见的陷阱  
- 正确测试您的实现  

## 如何在 Java 中创建条形码签名
在 Java 中创建条形码签名的过程包括加载目标 PDF、配置条形码选项（如数据、类型、大小和位置），然后应用签名生成新文档。GroupDocs.Signature 负责渲染和加密绑定，您只需提供所需参数并管理文件路径。

## 前置条件和环境检查清单

在开始之前，请确保您已准备好以下项目：

- **Java Development Kit (JDK) 8 或更高** – 所有 GroupDocs Java 库的必备条件。  
- **Maven 或 Gradle** – 用于管理 GroupDocs.Signature 依赖。  
- **IDE** 如 IntelliJ IDEA、Eclipse 或带有 Java 扩展的 VS Code。  
- **GroupDocs.Signature for Java**（建议使用 23.12 或更高版本）。  
- **基本的 Java 知识** – 您应熟悉创建类、处理异常以及文件 I/O 操作。

## 在项目中设置 GroupDocs.Signature

将库引入项目非常简单。请选择您的构建工具：

**对于 Maven 用户**，在 `pom.xml` 中添加以下依赖：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**使用 Gradle？** 在 `build.gradle` 中添加此行：

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**倾向手动设置？** 从 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) 下载 JAR 并将其加入类路径。

### 获取许可证

在正式生产之前，您需要处理许可证：

- **免费试用：** 适合测试——从 GroupDocs 网站获取，以探索核心功能。  
- **临时许可证：** 需要更长的评估时间？申请 30 天临时许可证。  
- **完整许可证：** 生产环境使用，购买后可无限制使用。  

下面是一个快速检查，确保一切正常：

```java
Signature signature = new Signature("sample.pdf");
System.out.println("Signature object created successfully.");
```

如果运行没有错误，说明已准备就绪！

## 如何在 Java 中创建条形码签名

现在进入有趣的部分——让我们为 PDF 添加条形码签名。我们将把过程拆分为若干步骤，帮助您清晰了解每一步的作用。

### 步骤 1：初始化 Signature 对象

**定义锚点：** `Signature` 类是 GroupDocs.Signature 用于加载、修改和保存 PDF 文档的入口。

首先，需要告诉 GroupDocs 您要处理的 PDF：

```java
Signature signature = new Signature("input.pdf");
```

**发生了什么：** `Signature` 对象将您的 PDF 加载到内存中，并为后续修改做好准备。请确保文件路径正确——在 Windows 上使用反斜杠时需进行转义（使用 `\\` 或直接使用正斜杠，后者跨平台通用）。

### 步骤 2：配置条形码选项（如何添加条形码）

**定义锚点：** `BarcodeSignOptions` 包含在 PDF 中渲染条形码所需的所有设置。

现在创建条形码签名并设置数据：

```java
BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeEncodeType.Code128);
```

- `"12345678"` 是条形码数据——可以是订单号、证书编号或任何您需要的标识符。  
- `Code128` 是编码类型（下文会详细说明如何选择合适的类型）。  

**小贴士：** Code128 能同时处理数字和字母，适用于大多数场景。如果仅需数字，可考虑 `Code39`，但 Code128 提供更高的灵活性。

### 步骤 3：定位条形码（如何使用条形码签署 PDF）

**定义锚点：** `SignatureOptions` 提供页面编号、大小和对齐等布局属性。

这里正是 GroupDocs 的优势所在——基于百分比的定位让条形码在任何 PDF 大小上都保持良好外观：

```java
options.setLeft(10);   // 10% from the left edge
options.setTop(90);    // 90% from the bottom edge (near the footer)
options.setWidth(30);  // 30% of page width
options.setHeight(10); // 10% of page height
options.setPageNumber(1);
```

**为何使用百分比：** 想象一下您需要同时签署 A4 文档和法律纸张。使用百分比定位，条形码会自动按比例缩放，保持一致外观。若使用固定像素值，条形码在大文档上会显得太小，在小文档上则会过大。

**实际示例：**在 A4 页面（595 × 842 points）上，30% 宽度的条形码约为 180 points；在法律纸（612 × 1008 points）上约为 184 points——实现自动比例。

### 步骤 4：签署并保存文档（如何将条形码添加到 PDF）

现在真正应用签名并保存结果：

```java
signature.sign(outputPath, options);
```

**重要提示：** 输出目录必须事先存在，GroupDocs 不会自动创建嵌套目录，请先创建或在代码中处理：

```java
new File("output").mkdirs();
```

**如果出现异常怎么办？** 将代码包装在 try‑catch 块中：

```java
try {
    signature.sign("signed.pdf", options);
} catch (Exception e) {
    e.printStackTrace();
}
```

## 为您的需求选择合适的条形码类型（生成 Code128 条形码）

GroupDocs 支持多种条形码格式，选择合适的类型至关重要。以下是实用对比：

**Code128（我们的默认选择）：**
- **最佳场景：** 混合字母数字数据（如 “INV2024-001”）  
- **容量：** 最多 128 个 ASCII 字符  
- **优势：** 紧凑、广泛支持、兼容字母和数字  
- **适用：** 需要灵活性且不确定数据类型时  

**Code39：**
- **最佳场景：** 简单的字母数字码  
- **容量：** 43 个字符（A‑Z、0‑9 及部分符号）  
- **优势：** 老旧扫描仪兼容性更好  
- **适用：** 与遗留系统对接或对数据密度要求不高时  

**QR Code：**
- **最佳场景：** 大量数据（URL、JSON 等）  
- **容量：** 最多约 3 KB 数据  
- **优势：** 可存储复杂结构，内置纠错  
- **适用：** 需要嵌入结构化数据或链接时  

**EAN/UPC：**
- **最佳场景：** 商品标识  
- **容量：** 固定长度数字码（8‑13 位）  
- **适用：** 零售或库存系统  

**快速决策指南：**  
- 需要字母和数字？ → Code128  
- 仅数字且追求简洁？ → Code39  
- 数据量大或需链接？ → QR Code  
- 零售/商品码？ → EAN/UPC  

## 常见陷阱及规避方法（防篡改条形码）

以下是开发者最常遇到的问题（帮助您避免）：

### 问题 1：条形码定位不正确

**表现：** 条形码出现在意外位置或被裁剪。

**常见原因：**  
- 在不同页面尺寸上使用像素值  
- 忘记 PDF 坐标系原点在左下角，而非左上角  
- 边距导致内容超出可视区域  

**解决方案：** 始终使用百分比定位以保持一致：

```java
options.setLeft(5);
options.setTop(95);
options.setWidth(40);
options.setHeight(12);
```

### 问题 2：条形码文字不可读

**表现：** 条形码显示正常，但扫描仪读取失败。

**原因：**  
- 条形码尺寸过小，无法容纳数据量  
- 数据类型与编码不匹配  
- 条形码与背景对比度不足  

**解决方案：** 根据数据长度调整条形码大小。对于 10‑15 字符的 Code128，建议宽度占页面宽度的 8‑10%。

### 问题 3：文件路径异常

**表现：** `FileNotFoundException` 或类似错误。

**原因：**  
- 硬编码的 Windows 路径使用单个反斜杠  
- 输出目录不存在  
- 文件权限问题  

**解决方案：** 使用正斜杠（跨平台通用），并提前创建目录：

```java
Path output = Paths.get("output/signed.pdf");
Files.createDirectories(output.getParent());
```

### 问题 4：大 PDF 导致内存不足

**表现：** 处理大型文档时出现内存溢出。

**解决方案：** 完成后关闭 `Signature` 对象以释放资源：

```java
signature.close();
```

## 测试您的条形码实现

在部署之前，请确保条形码实际可用。以下是实用的测试清单：

### 1. 目视检查
打开已签名的 PDF，检查：
- 条形码是否可见且定位正确？  
- 是否清晰（无模糊或像素化）？  
- 周围是否有足够的留白？

### 2. 扫描测试
使用手机条形码扫描应用（如 “Barcode Scanner” 或 “QR & Barcode Reader”）验证：
- 扫描器能读取条形码吗？  
- 解码数据是否与您编码的相符？  
- 不同角度和距离下是否都能读取？

### 3. 跨平台测试
在不同设备上打开 PDF：
- Windows（Adobe Reader、Chrome）  
- macOS（Preview、Chrome）  
- 移动设备（iOS、Android）  

确保条形码在所有环境中均能正确渲染。

### 4. 自动化测试代码
下面提供一个简易测试示例：

```java
Signature testSignature = new Signature("signed.pdf");
List<BarcodeSignature> signatures = testSignature.search(BarcodeSignature.class);
if (signatures.size() > 0) {
    System.out.println("Barcode found: " + signatures.get(0).getText());
}
```

## 条形码签名的真实场景

以下是该技术在生产系统中的典型应用：

### 1. 证书生成与验证
**场景：** 您的培训平台颁发结业证书。  
**实现：** 生成唯一证书 ID（如 “CERT‑2024‑00123”），并在右下角嵌入 Code128 条形码。扫描条形码即可通过 API 快速检索证书详情，省去手工录入。

### 2. 发票追踪系统
**场景：** 公司每月处理成千上万张发票。  
**实现：** 将发票号和到期日以 QR 码形式嵌入，放置在易于扫描的区域。自动分拣系统即可无需人工干预完成路由，将处理时间从数小时缩短至数分钟。

### 3. 法律合同管理
**场景：** 律所需追踪合同版本及修订。  
**实现：** 每个合同版本分配唯一条形码标识，包含合同 ID、版本号和签署日期。审计时扫描即可自动调出完整版本历史。

### 4. 医疗记录安全
**场景：** 医院希望防止未授权的记录访问。  
**实现：** 在记录中嵌入患者 ID 与创建时间戳的条形码。仅经授权的设备能够解码并访问完整记录，且每次扫描都会生成审计日志以满足合规要求。

## 性能优化技巧（java 文档安全）

在批量签署大量 PDF 时，性能尤为关键。以下技巧帮助您保持高效：

### 批处理策略
一次处理多份文档，而不是逐个：

```java
for (String filePath : pdfList) {
    Signature batchSignature = new Signature(filePath);
    batchSignature.sign(outputPath, options);
    batchSignature.close();
}
```

**优势：** 重用选项对象并正确关闭资源，可防止内存泄漏。

### 大文件内存管理
针对超过 50 MB 的 PDF：
- 逐个顺序处理，而非一次性加载多个  
- 使用 try‑with‑resources 确保资源释放  
- 监控堆内存并根据需要调整 JVM 参数，例如 `-Xmx2g`

### 缓存常用条形码
如果大量文档使用相同条形码，可缓存 `BarcodeSignOptions` 实例：

```java
BarcodeSignOptions cachedOptions = new BarcodeSignOptions("STATIC_ID");
cachedOptions.setEncodeType(BarcodeEncodeType.Code128);
```

## 何时使用条形码签名（以及何时不适用）

**适用场景：**
- 需要机器可读的文档标识符  
- 文档将被自动扫描或处理  
- 想要防篡改追踪而不依赖数字证书  
- 已有条形码基础设施需集成  

**不适用场景：**
- 需要具备法律效力的数字签名（请使用数字证书）  
- 文档仅供人工阅读（文字水印即可）  
- 文档极小，条形码会占据过大版面  
- 安全要求必须加密——条形码是可见且可被任何人扫描的  

**可以组合使用吗？** 当然！许多系统同时使用条形码签名进行追踪，并使用数字签名确保法律有效性。

## 常见问题

**Q: 可以在同一个 PDF 中使用不同类型的条形码吗？**  
A: 可以！对每种条形码类型调用 `signature.sign()` 多次，并使用不同的 `BarcodeSignOptions`。只需确保它们不重叠。

**Q: 如何处理包含特殊字符的条形码？**  
A: Code128 能很好地处理大多数 ASCII 字符。若需 Unicode 或复杂数据，请改用 QR 码——它支持 UTF‑8 编码。

**Q: Code128 条形码的最大数据容量是多少？**  
A: 理论上最多 128 个字符，但超过 30‑40 个字符可读性会显著下降。若数据量更大，请使用 QR 码。

**Q: 添加条形码会显著增加 PDF 文件大小吗？**  
A: 不会——条形码是矢量图形，通常仅增加 5‑20 KB，具体取决于大小和复杂度。

**Q: 能旋转条形码或垂直放置吗？**  
A: 能！使用 `options.setRotationAngle(90)` 可将条形码旋转 90 度，适合边缘放置。

**Q: 如何让条形码出现在多页 PDF 的每一页？**  
A: 遍历页面并对每页调用签名。请参考 GroupDocs 文档中的 `PagesSetup` 类，以控制签名的页面范围。

**Q: 如果我的条形码扫描器无法读取生成的条形码怎么办？**  
A: 首先确认扫描器支持所选条形码类型。然后增大条形码尺寸——大多数读取问题源于条形码过小。建议宽度至少 1 英寸（2.54 cm）以确保可靠读取。

## 其他资源

**文档：**  
- [GroupDocs.Signature for Java Docs](https://docs.groupdocs.com/signature/java/)  
- [API Reference Guide](https://reference.groupdocs.com/signature/java/)  

**下载与授权：**  
- [Download Latest Version](https://releases.groupdocs.com/signature/java/)  
- [Free Trial Access](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [Purchase Full License](https://purchase.groupdocs.com/buy)  

**社区与支持：**  
- [Support Forum](https://forum.groupdocs.com/c/signature/) - 活跃社区，拥有 GroupDocs 工程师参与  

---

**最后更新：** 2026-07-20  
**测试环境：** GroupDocs.Signature 23.12（Java）  
**作者：** GroupDocs

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

```java
import com.groupdocs.signature.Signature;

public class QuickTest {
    public static void main(String[] args) {
        try {
            Signature signature = new Signature("test-document.pdf");
            System.out.println("GroupDocs.Signature is ready to go!");
        } catch (Exception e) {
            System.err.println("Setup issue: " + e.getMessage());
        }
    }
}
```

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

```java
import com.groupdocs.signature.domain.enums.MeasureType;
import com.groupdocs.signature.domain.Padding;

// Use percentages instead of fixed pixels
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from the left edge
options.setTop(5);   // 5% from the top

// Size it proportionally too
options.setSizeMeasureType(MeasureType.Percents);
options.setWidth(10);  // 10% of page width
options.setHeight(5);  // 5% of page height

// Add some breathing room with margins
Padding margins = new Padding();
margins.setLeft(1);
margins.setTop(1);
margins.setRight(1);
options.setMargin(margins);
```

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithPercents/sample_signed.pdf";
signature.sign(outputFilePath, options);
```

```java
Path outputPath = Paths.get(outputFilePath);
Files.createDirectories(outputPath.getParent());
signature.sign(outputFilePath, options);
```

```java
try {
    signature.sign(outputFilePath, options);
    System.out.println("PDF signed successfully at: " + outputFilePath);
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    e.printStackTrace();
}
```

```java
options.setLocationMeasureType(MeasureType.Percents);
options.setLeft(5);  // 5% from left works on any page width
```

```java
options.setWidth(10);  // Give it room to breathe
options.setHeight(5);  // Maintain proper aspect ratio
```

```java
String filePath = "documents/sample.pdf";  // Works on Windows, Mac, Linux
Files.createDirectories(Paths.get("output/signed"));
```

```java
try (Signature signature = new Signature(filePath)) {
    signature.sign(outputFilePath, options);
} // Automatically closes and releases memory
```

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class BarcodeSignatureTest {
    
    @Test
    public void testBarcodeSigning() {
        String testPdf = "test-data/sample.pdf";
        String output = "test-output/signed.pdf";
        
        try (Signature signature = new Signature(testPdf)) {
            BarcodeSignOptions options = new BarcodeSignOptions("TEST123");
            options.setEncodeType(BarcodeTypes.Code128);
            
            signature.sign(output, options);
            
            // Verify output file exists
            assertTrue(new File(output).exists());
            
            // Verify file size increased (signature was added)
            long originalSize = new File(testPdf).length();
            long signedSize = new File(output).length();
            assertTrue(signedSize > originalSize);
            
        } catch (Exception e) {
            fail("Signing should not throw exception: " + e.getMessage());
        }
    }
}
```

```java
List<String> pdfFiles = Arrays.asList("doc1.pdf", "doc2.pdf", "doc3.pdf");

for (String pdfFile : pdfFiles) {
    try (Signature signature = new Signature(pdfFile)) {
        BarcodeSignOptions options = createBarcodeOptions(); // Reuse options
        signature.sign(getOutputPath(pdfFile), options);
    }
}
```

```java
// Create options once, reuse many times
BarcodeSignOptions templateOptions = createStandardBarcodeOptions();

// For each document, clone and customize
BarcodeSignOptions documentOptions = templateOptions.clone();
documentOptions.setText(uniqueDocumentId);
```

## 相关教程

- [Java Barcode Signature Tutorial - Add, Verify & Manage Barcodes in PDFs](/signature/java/barcode-signatures/)
- [Create Barcode Signature in Java – Update PDF Barcodes](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [How to read QR code PDF using Java and GroupDocs.Signature](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)