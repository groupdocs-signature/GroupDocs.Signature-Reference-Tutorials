---
categories:
- Java PDF Processing
date: '2026-08-04'
description: 了解如何使用 GroupDocs.Signature 在 Java 中向 PDF 文件添加 Barcode。此 step‑by‑step
  教程展示了如何高效且可靠地 generate Barcode PDFs。
keywords:
- add barcode to pdf
- how to add barcode
- groupdocs signature java
lastmod: '2026-08-04'
linktitle: 在 Java 中添加 Barcode 到 PDF
og_description: 使用 GroupDocs.Signature for Java 将 barcode 添加到 PDF。Learn step‑by‑step
  如何 generate barcode PDFs、handle errors，并 optimize performance。
og_image_alt: Guide showing Java code that adds a barcode to a PDF with GroupDocs.Signature
og_title: 在 Java 中添加 barcode 到 PDF – 完整 GroupDocs 指南
schemas:
- author: GroupDocs
  dateModified: '2026-08-04'
  description: Learn how to add barcode to PDF files in Java using GroupDocs.Signature.
    This step‑by‑step tutorial shows how to generate barcode PDFs efficiently and
    reliably.
  headline: How to Add Barcode to PDF in Java – GroupDocs Guide
  type: TechArticle
- description: Learn how to add barcode to PDF files in Java using GroupDocs.Signature.
    This step‑by‑step tutorial shows how to generate barcode PDFs efficiently and
    reliably.
  name: How to Add Barcode to PDF in Java – GroupDocs Guide
  steps:
  - name: setting up document paths
    text: 'First, tell Java where to find your PDF and where to save the signed version:
      What’s happening: You’re defining the input file path and extracting just the
      filename. This keeps your output organized (especially useful when batch‑processing
      multiple files). **Real‑world tip**: In production, these pa'
  - name: configuring output and barcode options
    text: '`BarcodeSignOptions` defines the barcode signature parameters such as data,
      type, size, and location. Breaking this down: - `outputFilePath` – Where your
      finished PDF gets saved. Notice the subfolder structure? This helps keep different
      signing methods organized. - `BarcodeSignOptions("12345678")` –'
  - name: positioning the barcode with precision
    text: '`BarcodeSignOptions` also lets you place the barcode with millimeter precision,
      which is ideal for printed output. Why millimeters matter: When you’re printing
      documents, millimeters give you consistent sizing across different paper sizes
      and resolutions. (You can also use pixels or percentages if t'
  - name: adding margins for polish
    text: 'Margins prevent your barcode from crowding other content: What this does:
      Creates a 5 mm buffer zone around your barcode. This breathing room improves
      scannability and looks more professional. **When to increase margins**: If you’re
      placing barcodes near the edge of a page, bump the margins to 10 mm'
  - name: signing and saving the document
    text: 'Now for the moment of truth—actually adding the barcode: What happens under
      the hood: GroupDocs opens your PDF, renders the barcode based on your options,
      embeds it at the specified position, and saves the modified file. The original
      PDF stays untouched. **Return value**: The `SignResult` object con'
  - name: handling errors gracefully
    text: 'Things can go wrong (wrong file paths, corrupted PDFs, insufficient permissions).
      Handle errors properly: Best practices for exception handling: - Log the full
      stack trace for debugging (not just the message) - Provide user‑friendly error
      messages (avoid technical jargon) - Clean up resources even w'
  type: HowTo
- questions:
  - answer: Change the `setEncodeType()` parameter. For QR codes, use `BarcodeTypes.QR`.
      For EAN‑13, use `BarcodeTypes.EAN13`. GroupDocs supports over 60 barcode types
      out of the box.
    question: How do I create barcode signature PDF in Java for different barcode
      types?
  - answer: Absolutely. Call `signature.sign()` multiple times with different `BarcodeSignOptions`,
      or pass a list of signature options in a single call.
    question: Can I add multiple barcodes to the same PDF?
  - answer: GroupDocs is non‑destructive by default—it adds barcodes as a new layer
      without modifying existing content. Your original text, images, and formatting
      remain intact.
    question: How do I add barcode to existing PDF without losing content?
  - answer: It depends on the type. Code128 handles about 128 characters comfortably.
      QR codes can store up to 4 000 characters. If you need more, consider encoding
      a URL that points to your data instead.
    question: What’s the maximum data I can encode in a barcode?
  - answer: Yes. The free trial adds watermarks. For production deployments, you’ll
      need either a temporary license (for extended testing) or a purchased license.
      Check the [GroupDocs pricing page](https://purchase.groupdocs.com/buy) for current
      options.
    question: Do I need a license for production use?
  type: FAQPage
tags:
- barcode-generation
- pdf-signing
- document-automation
- groupdocs
- add barcode to pdf
title: 如何在 Java 中向 PDF 添加 Barcode – GroupDocs 指南
type: docs
url: /zh/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/
weight: 1
---

# 如何在 Java 中向 PDF 添加条形码

是否曾经需要自动跟踪发票、验证合同真实性，或大规模管理库存文档？**学习如何向 PDF 添加条形码**的编程方法可以解决这些问题——如果你使用 Java，则拥有一个可靠且经过实战检验的选项。

手动添加条形码无法扩展。无论是处理十张发票还是一万张发票，都需要一种可靠的方式来**向 PDF 添加条形码**。这时，一个优秀的 Java PDF 条形码库就派上用场。

在本指南中，我将向您展示如何使用 GroupDocs.Signature 将条形码添加到 PDF Java 文件——该库负责繁重的工作，同时让您对位置、尺寸和条形码类型进行细粒度控制。阅读完本指南后，您将了解如何使用 Java 代码为 PDF 添加条形码签名、处理边缘情况，并避免常见的陷阱。

**您将学习：**
- 为什么 PDF 中的条形码对您的工作流重要  
- 在 Java 中正确设置 GroupDocs.Signature  
- 精确创建和定位条形码签名  
- 处理错误并优化性能  
- 不同行业的真实案例应用  

## 快速回答
- **我应该使用哪个库？** GroupDocs.Signature for Java  
- **如何创建条形码签名 PDF？** 使用 `BarcodeSignOptions` 与 `Signature.sign()`  
- **哪种条形码类型最适合大多数情况？** Code128  
- **我可以在同一个 PDF 中添加多个条形码吗？** 可以，多次调用 `sign()` 或传入列表  
- **生产环境是否需要许可证？** 是的，有效的 GroupDocs 许可证会去除水印  

## 为什么向 PDF 添加条形码？

条形码将机器可读的数据直接嵌入 PDF，实现即时验证、自动数据采集以及与 ERP 或库存系统的无缝集成。通过添加条形码，您将静态文档转化为可操作的资产，可通过扫描获取 ID、跟踪状态并满足合规要求。

在进入代码之前，让我们先谈谈其重要性。PDF 中的条形码不仅仅是为了专业外观——它们解决了真实的业务问题：

**文档验证** – 条形码可以编码唯一标识符，使伪造几乎不可能。当有人扫描条形码时，系统可以即时验证文档是否合法。

**工作流自动化** – 与其手动输入文档 ID 或追踪号，员工（或客户）可以扫描条形码。这相比手动录入可降低约 95% 的人为错误。

**与现有系统集成** – 大多数 ERP、库存和文档管理系统已经支持“条形码”。将其添加到 PDF 中即可实现无缝集成，无需构建自定义 API。

**合规要求** – 许多行业（医疗、物流、法律）要求文档可追溯。条形码提供满足监管要求的审计轨迹。

以编程方式添加条形码的关键优势是什么？**一致性和规模化**。您只需定义一次规则，所有文档都会得到相同处理——无论是处理 5 个文件还是 5 万个文件。

## 前置条件

在开始编码之前，请确保已满足以下基础条件：

### 必需的软件和库
- **JDK 8 或更高** 已安装在您的机器上（建议使用 JDK 11+ 以获得更好性能）  
- IntelliJ IDEA、Eclipse 或带有 Java 扩展的 VS Code 等 IDE  
- **GroupDocs.Signature for Java 版本 23.12**（下面将演示如何添加）

### 基础知识要求
- 熟悉 Java 基础（类、对象、文件处理）  
- 了解 PDF 文档结构（有帮助但非必需）  
- 熟悉依赖管理（Maven 或 Gradle）

**专业提示**：如果您是 GroupDocs 新手，请先获取免费试用。它提供 30 天的试用期，无需购买许可证，适合概念验证工作。

## 为 Java 设置 GroupDocs.Signature

将 GroupDocs.Signature 引入项目非常简单。请选择与您环境匹配的依赖管理系统：

### Maven 设置
将以下内容添加到您的 `pom.xml` 文件中：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 设置
对于 Gradle 用户，将此行添加到您的 `build.gradle` 中：

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下载选项
不想使用构建工具？直接从[GroupDocs.Signature for Java 发布页面](https://releases.groupdocs.com/signature/java/)下载 JAR，并手动将其添加到项目的类路径中。

### 许可证配置
以下是大多数开发者采用的实际许可证获取路径：

1. **从免费试用开始** – 无需信用卡，无需承诺。适合测试。  
2. **获取临时许可证** – 如果 30 天不足，可申请临时许可证以延长开发时间。  
3. **购买生产许可证** – 准备部署时，购买符合使用量的许可证。

**重要**：免费试用会在输出文档中添加水印。面向客户的工作至少需要临时许可证。

### 初始设置代码

`Signature` 是 GroupDocs.Signature 中的主要类，提供加载、签名和保存 PDF 文档的方法。

这里发生了什么：`Signature` 类是您的入口点。您传入文件路径，它会将 PDF 加载到内存中进行处理。很简单，对吧？

**常见错误避免**：完成后不要忘记关闭 `Signature` 对象（或使用 try‑with‑resources）。保持打开会导致长时间运行的应用出现内存泄漏。

```java
import com.groupdocs.signature.Signature;

// Initialize Signature object with your document path
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
```

## 选择合适的条形码类型

并非所有条形码都相同。选择的类型取决于您需要编码的内容以及条形码的扫描场景。

### 支持的常用条形码类型

- **Code128** – 适用于字母数字数据；常用于运输标签。  
- **QR 码** – 当需要存储更多数据（URL、JSON，最多 4000 字符）时的理想选择。  
- **Code39** – 比 Code128 更简单但空间利用率低；适合内部追踪。  
- **EAN/UPC** – 零售产品的行业标准。

**何时使用哪种？**
- 需要编码超过 50 个字符？ → QR 码  
- 标准产品标识？ → EAN/UPC  
- 通用文档追踪？ → Code128  
- 需要与旧版扫描仪最大兼容性？ → Code39

**专业提示**：Code128 是文档管理最安全的默认选择。它在可读性、数据容量和扫描仪兼容性之间取得平衡。

## 实施指南：创建条形码签名

下面进入实质内容——实际创建并将条形码添加到 PDF 中。我会把过程拆分为可管理的步骤，方便您跟随（或跳到需要的部分）。

### 步骤 1：设置文档路径

首先，告诉 Java 您的 PDF 位于何处以及签名后保存到哪里：

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String fileName = new File(filePath).getName();
```

这里发生了什么：您定义了输入文件路径并提取文件名。这有助于组织输出（在批量处理多个文件时尤其有用）。

**实际提示**：在生产环境中，这些路径通常来自配置文件或环境变量，而不是硬编码字符串。考虑使用 `System.getenv()` 或属性文件以获得灵活性。

### 步骤 2：配置输出和条形码选项

`BarcodeSignOptions` 定义条形码签名的参数，如数据、类型、尺寸和位置。

细分如下：

- `outputFilePath` – 完成的 PDF 保存位置。注意子文件夹结构？这有助于组织不同的签名方式。  
- `BarcodeSignOptions("12345678")` – 条形码中编码的数据。可以是发票号、追踪 ID、文档哈希等。  
- `setEncodeType(BarcodeTypes.Code128)` – 告诉 GroupDocs 使用哪种条形码格式。

**常见问题**：“我可以在条形码数据中使用特殊字符吗？”使用 Code128 可以——可以包含字母、数字和大多数标点符号。QR 码更为灵活。

```java
// Define output file path
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithMillimeters/" + fileName;

BarcodeSignOptions options = new BarcodeSignOptions("12345678");
options.setEncodeType(BarcodeTypes.Code128);
```

### 步骤 3：精确定位条形码

`BarcodeSignOptions` 还允许您以毫米精度放置条形码，这对于打印输出非常理想。

为何使用毫米：在打印文档时，毫米可在不同纸张尺寸和分辨率之间保持一致的尺寸。（如果更适合您的使用场景，也可以使用像素或百分比。）

定位策略：

- **右上角**（如运输标签）：`setLeft(150)`, `setTop(10)`  
- **底部居中**（如票据）：根据页面宽度计算中心  
- **紧邻现有内容**：测量 PDF 布局并相应定位

**专业提示**：在批量处理前，用少量示例 PDF 测试定位。不同的 PDF 布局可能需要微调。

```java
// Set position and size in millimeters
options.setLocationMeasureType(MeasureType.Millimeters);
options.setLeft(40);  // X‑coordinate from left edge
options.setTop(50);   // Y‑coordinate from top edge

options.setSizeMeasureType(MeasureType.Millimeters);
options.setWidth(20);  // Width of the barcode
options.setHeight(10); // Height of the barcode
```

### 步骤 4：添加边距以提升品质

边距可防止条形码与其他内容拥挤：

```java
// Define margin settings
Padding padding = new Padding();
padding.setLeft(5);   // Left margin in mm
padding.setTop(5);    // Top margin in mm
padding.setRight(5);  // Right margin in mm
padding.setBottom(5); // Bottom margin in mm
options.setMargin(padding);
```

作用：在条形码周围创建 5 mm 的缓冲区。此间距提升可扫描性并显得更专业。

**何时增大边距**：如果条形码靠近页面边缘，请将边距提升至 10 mm。打印机常对靠近边缘的内容有困难。

### 步骤 5：签名并保存文档

现在是关键时刻——实际添加条形码：

```java
// Sign and save the document
SignResult signResult = signature.sign(outputFilePath, options);
```

内部工作原理：GroupDocs 打开 PDF，根据您的选项渲染条形码，将其嵌入指定位置并保存修改后的文件。原始 PDF 保持不变。

**返回值**：`SignResult` 对象包含成功/失败状态以及已签名内容的元数据。您可以检查它以验证操作是否成功。

### 步骤 6：优雅地处理错误

可能会出现问题（错误的文件路径、损坏的 PDF、权限不足）。请妥善处理错误：

```java
try {
    Signature signature = new Signature(filePath);
    SignResult signResult = signature.sign(outputFilePath, options);
    
    System.out.println("Barcode added successfully!");
    System.out.println("Output saved to: " + outputFilePath);
    
} catch (Exception e) {
    System.err.println("Error signing document: " + e.getMessage());
    throw new GroupDocsSignatureException(e.getMessage());
}
```

异常处理的最佳实践：

- 记录完整的堆栈跟踪以便调试（而非仅记录消息）  
- 提供用户友好的错误信息（避免技术术语）  
- 即使出现错误也要清理资源（使用 try‑with‑resources）  
- 对瞬时失败（网络问题、文件锁定）考虑重试逻辑

**常见错误**：

- `FileNotFoundException` – 输入 PDF 路径错误  
- `GroupDocsSignatureException` – 条形码数据无效或 PDF 版本不受支持  
- `OutOfMemoryError` – 同时处理过多大型 PDF 导致内存不足

## 如何在 Java 中创建条形码签名 PDF

使用 `new Signature("source.pdf")` 加载 PDF，配置带有所需数据和条形码类型的 `BarcodeSignOptions` 对象，设置其位置和尺寸，然后调用 `sign(outputPath, options)`。该方法返回一个 `SignResult`，指示操作是否成功并提供已创建签名的详细信息。

如果您更喜欢简明的步骤清单，请参考以下内容：

1. **添加 GroupDocs.Signature 依赖**（Maven、Gradle 或手动 JAR）。  
2. **使用源 PDF 路径初始化 `Signature`**。  
3. **配置 `BarcodeSignOptions`** – 设置数据、类型、尺寸和位置。  
4. **可选设置边距** 以提升可读性。  
5. **调用 `signature.sign(outputPath, options)`** 嵌入条形码。  
6. **处理异常** 并关闭资源。

遵循这六个步骤，您即可在任何 Java 应用中可靠地**向 PDF Java 文档添加条形码**。

## 常见问题与解决方案

让我们来解决开发者实际遇到的问题（因为文档很少涉及这些）：

### 问题 1：条形码无法正确扫描

**症状**：扫描仪无法读取条形码或返回错误数据。

**解决方案**：
- 增大条形码尺寸（大多数扫描仪的最小宽度为 15 mm）  
- 检查条形码数据是否包含该类型不支持的字符  
- 确保条形码与背景之间有足够的对比度  
- 使用多个扫描应用进行测试——有些比其他的更好  

### 问题 2：条形码在不同文档间位置偏移

**症状**：相同的定位代码在不同页面尺寸的 PDF 上产生不同结果。

**解决方案**：
- 不同页面尺寸的 PDF 需要进行位置计算，而非硬编码值  
- 检查源 PDF 是否有旋转（这会导致坐标偏差）  
- 使用基于百分比的定位以获得更好的一致性  
- 尽可能将所有输入 PDF 规范化为统一页面尺寸  

### 问题 3：大批量处理时性能下降

**症状**：前 100 个 PDF 处理快速，随后速度变慢。

**解决方案**：
- 及时关闭 `Signature` 对象（或使用 try‑with‑resources）  
- 分成更小的批次处理，并在批次之间进行内存清理  
- 考虑对 CPU 密集型操作进行并行处理  
- 监控堆内存使用——可能需要调优 JVM  

```java
// Good: Process in chunks
List<String> allFiles = getAllPdfFiles();
int batchSize = 100;

for (int i = 0; i < allFiles.size(); i += batchSize) {
    List<String> batch = allFiles.subList(i, Math.min(i + batchSize, allFiles.size()));
    processBatch(batch);
    System.gc(); // Suggest garbage collection between batches
}
```

### 问题 4：输出文件大小膨胀

**症状**：签名后的 PDF 大小远大于原始文件。

**解决方案**：
- GroupDocs 不会自动压缩——如有需要需自行处理压缩  
- 避免在矢量图可用时添加高分辨率条形码图像  
- 检查是否意外嵌入了字体或额外的元数据  

**何时联系支持**：如果尝试上述解决方案后仍有问题，可访问[GroupDocs 论坛](https://forum.groupdocs.com/c/signature/)获取响应迅速的支持人员帮助。

## 实际案例

以下是各行业实际使用此功能的方式：

### 法律行业：合同管理

律师事务所为合同添加条形码，以将纸质文件链接到案件管理系统。扫描条形码即可立即调出完整案件历史，将处理时间从分钟缩短到秒级。

**实现技巧**：在条形码中编码文档哈希，以便验证纸质文档未被篡改。

### 医疗保健：患者记录

医院在出院小结和处方 PDF 上附加条形码。患者登记时，工作人员扫描条形码即可即时填充其档案的既往就诊记录。

**合规说明**：确保条形码实现符合 HIPAA 对数据编码的要求。

### 物流：运输标签

电子商务平台自动在装箱单上添加追踪条形码。仓库人员扫描即可更新发货状态，无需手动录入数据。

**性能考虑**：这些系统通常每小时处理数千份文档——批处理和并行执行至关重要。

### 金融：发票处理

会计部门在发票上添加条形码，编码付款条款和供应商 ID。扫描后可自动将其路由至正确的审批工作流。

**专业提示**：将条形码与 OCR 结合，实现最大化自动化——使用条形码获取元数据，使用 OCR 读取明细行。

## 性能最佳实践

在大规模处理文档时，这些优化会产生显著效果：

### 内存管理
- **使用 try‑with‑resources**：确保 `Signature` 对象正确关闭。  
- **分批处理**：不要一次性加载 10 000 个 PDF 到内存。  
- **监控堆内存使用**：设置合适的 JVM 参数（`-Xmx`, `-Xms`）。

### 批处理策略
```java
List<String> files = getAllPdfFiles();
files.parallelStream().forEach(file -> {
    try {
        addBarcodeToFile(file);
    } catch (Exception e) {
        // Handle per‑file errors
    }
});
```

**注意**：并行处理会占用更多内存。请监控并相应调优。

### 缓存签名对象
如果重复处理相似文档，考虑复用配置：

```java
// Create options once
BarcodeSignOptions templateOptions = createStandardOptions();

// Reuse for multiple files
for (String file : files) {
    BarcodeSignOptions options = templateOptions.clone();
    // Customize per file if needed
    processFile(file, options);
}
```

## 常见问答

**问：如何在 Java 中为不同条形码类型创建条形码签名 PDF？**  
**答**：更改 `setEncodeType()` 参数。对于 QR 码，使用 `BarcodeTypes.QR`。对于 EAN‑13，使用 `BarcodeTypes.EAN13`。GroupDocs 开箱即支持超过 60 种条形码类型。

**问：我可以在同一个 PDF 中添加多个条形码吗？**  
**答**：完全可以。多次调用 `signature.sign()` 并传入不同的 `BarcodeSignOptions`，或在一次调用中传入签名选项列表。

**问：如何在不丢失内容的情况下向现有 PDF 添加条形码？**  
**答**：GroupDocs 默认是非破坏性的——它将条形码作为新层添加，不会修改已有内容。原始文本、图像和格式保持完整。

**问：条形码最多能编码多少数据？**  
**答**：取决于类型。Code128 能舒适地容纳约 128 个字符。QR 码最多可存储 4 000 个字符。如果需要更多，可考虑编码指向数据的 URL。

**问：生产环境是否需要许可证？**  
**答**：是的。免费试用会添加水印。生产部署时，需要临时许可证（用于延长测试）或购买许可证。请查看[GroupDocs 定价页面](https://purchase.groupdocs.com/buy)了解当前选项。

**问：批处理期间如何处理异常？**  
**答**：为每个文件操作单独使用 try‑catch 块，这样单个 PDF 失败不会导致整个批次崩溃。记录带文件名的错误，以便后续重新处理失败文件。

**问：GroupDocs 能生成像 Data Matrix 这样的 2D 条形码吗？**  
**答**：可以！使用 `BarcodeTypes.DataMatrix`。Data Matrix 条形码在制造业很受欢迎，因为即使部分损坏或角度异常也能读取。

**问：GroupDocs 支持哪些 PDF 版本？**  
**答**：GroupDocs.Signature 支持 1.3 到 2.0 版本的 PDF（覆盖您遇到的 99% PDF）。如果有古老的 PDF，建议先进行转换。

## 结论

现在，您已经了解如何使用 GroupDocs.Signature 以编程方式**向 PDF Java 文档添加条形码**。我们覆盖了从基础设置到生产就绪的错误处理和性能优化的全部内容。

**关键要点**
- 条形码嵌入可操作数据，实现验证、自动化和合规。  
- GroupDocs 提供对位置和条形码类型的精确控制。  
- 妥善的错误处理和资源管理可避免生产中的麻烦。  
- 在大规模处理文档时，性能调优至关重要。

**下一步**：使用免费试用先做小规模概念验证。使用实际文档测试不同条形码类型。验证后，转向批量处理并最终投入生产部署。

有疑问或遇到问题？请在[GroupDocs 支持论坛](https://forum.groupdocs.com/c/signature/)提出——社区热心，响应及时。

## 资源

### 文档与下载
- [GroupDocs.Signature for Java 文档](https://docs.groupdocs.com/signature/java/)  
- [完整 API 参考](https://reference.groupdocs.com/signature/java/)  
- [下载最新版本](https://releases.groupdocs.com/signature/java/)

### 许可证与支持
- [购买许可证](https://purchase.groupdocs.com/buy)  
- [开始免费试用](https://releases.groupdocs.com/signature/java/)  
- [请求临时许可证](https://purchase.groupdocs.com/temporary-license/)  
- [社区支持论坛](https://forum.groupdocs.com/c/signature/)

---

**最后更新：** 2026-08-04  
**测试环境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs

## 相关教程

- [如何使用 GroupDocs.Signature 在 Java 中验证条形码签名](/signature/java/barcode-signatures/verify-barcode-signatures-groupdocs-signature-java/)  
- [在 Java 中创建条形码签名 – 更新 PDF 条形码](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)  
- [在 PDF Java 中添加 QR 码 - 使用 GroupDocs.Signature 的完整指南](/signature/java/qr-code-signatures/qr-code-signatures-java-groupdocs/)