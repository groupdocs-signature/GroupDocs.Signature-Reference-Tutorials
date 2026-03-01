---
categories:
- Java Development
- Document Processing
date: '2026-03-01'
description: 学习如何使用 Java 和 GroupDocs.Signature 读取带二维码的 PDF 文件。一步步指南、代码示例、故障排除及实际案例。
keywords: read qr code pdf, Java barcode verification PDF, GroupDocs barcode search
  tutorial, extract barcode data from PDF Java, Java PDF barcode scanner
lastmod: '2026-03-01'
linktitle: Search PDF Barcodes Java
tags:
- barcode-search
- pdf-processing
- groupdocs
- java-tutorial
- document-verification
title: 如何使用 Java 和 GroupDocs.Signature 读取 QR 码 PDF
type: docs
url: /zh/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/
weight: 1
---

# 如何使用 Java 读取 QR 码 PDF

## 介绍

是否曾需要从数百份 PDF 发票、运单标签或库存文档中提取条形码信息？手动浏览页面既繁琐又容易出错。无论是构建自动化文档处理系统，还是验证产品真伪，在 PDF 中高效查找条形码都是一项挑战。

在本指南中，您将学习如何使用 **GroupDocs.Signature** API 高效 **读取 QR 码 PDF** 文档。该强大的 API 能将可能需要数小时的手工工作转化为几行代码。您可以扫描整个文档，定位特定的条形码类型（如 QR 码或 Code128），并自动提取其数据。

**您将学习：**
- 在几分钟内为 Java 设置 GroupDocs.Signature  
- 在 PDF 文档中搜索条形码签名  
- 配置搜索选项以获得精确、针对性的结果  
- 处理不同的条形码类型（QR 码、EAN、Code128 等）  
- 排查常见问题并优化性能  

让我们开始吧！

## 快速答案
- **GroupDocs.Signature 能从 PDF 中读取 QR 码吗？** 是的，它可以检测 QR、Data Matrix、PDF417 以及许多 1D 条形码。  
- **生产环境需要许可证吗？** 需要商业许可证；可使用免费试用版进行评估。  
- **需要哪个 Java 版本？** Java 8 及以上（推荐使用 Java 11 及以上）。  
- **如何将搜索限制在特定页面？** 使用 `BarcodeSearchOptions.setAllPages(false)` 并设置 `setPageNumber()`。  
- **API 在批处理时是线程安全的吗？** 是的，只要为每个线程创建单独的 `Signature` 实例即可。

## 为什么在 PDF 中搜索条形码？

在进入技术细节之前，先看看这在实际应用中为何重要：

**常见业务场景**
- **发票处理** – 自动从供应商发票中提取订单号或跟踪码。  
- **库存管理** – 扫描产品目录并提取 SKU 条形码以更新数据库。  
- **运输与物流** – 验证装运清单中的包裹跟踪码。  
- **文档认证** – 通过检查嵌入的安全条形码来验证签署的文档。  
- **医疗记录** – 从医疗文档中提取患者 ID 或处方码。  

GroupDocs.Signature API 负责繁重的工作——您无需担心图像处理、条形码解码算法或 PDF 渲染的复杂性。一切都已内置。

## 前置条件

在开始本教程之前，请确保已准备好以下内容：

### 必需的库和依赖

您需要在 Java 项目中引入 GroupDocs.Signature 库。以下是使用 Maven 或 Gradle 添加的方法：

**Maven:**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle:**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**注意：** 请始终在 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) 检查最新版本。使用最新版本可确保获得错误修复和新功能。

### 环境设置

- **JDK 8 或更高** – GroupDocs.Signature 至少需要 Java 8（为获得更好性能，推荐使用 Java 11 及以上）。  
- **IDE** – 任意文本编辑器均可，但 IntelliJ IDEA 或 Eclipse 能通过自动完成和调试让您事半功倍。  
- **PDF 文档** – 准备好包含条形码的测试 PDF（发票、运单标签或产品目录均可）。

### 知识前提

您应熟悉以下内容：

- 基本的 Java 语法和面向对象概念  
- 使用 `try‑catch` 块处理异常  
- 在 IDE 中使用外部库  

如果您是第三方 Java 库的新手，也无需担心——我们将一步步演示全部过程。

## 为 Java 设置 GroupDocs.Signature

开始使用 GroupDocs.Signature 只需几分钟。以下是完整的设置流程：

### 步骤 1：添加依赖

使用 Maven 或 Gradle 引入库（参见上面的代码）。添加依赖后，刷新项目以下载 JAR 文件。

### 步骤 2：获取许可证

GroupDocs 提供多种许可证选项：

- **免费试用** – 适合测试。从 [GroupDocs releases](https://releases.groupdocs.com/signature/java/) 下载。  
- **临时许可证** – 通过 [Temporary License Page](https://purchase.groupdocs.com/temporary-license/) 获得 30 天的完整访问权限。  
- **商业许可证** – 生产环境使用，请在 [GroupDocs Purchase](https://purchase.groupdocs.com/) 购买许可证。  

**专业提示：** 先使用免费试用构建概念验证，如果 API 符合需求，再升级许可证。

### 步骤 3：基本初始化

以下示例展示如何创建 `Signature` 对象以处理 PDF：

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed.pdf"; // Replace with your PDF path
Signature signature = new Signature(filePath);
```

`Signature` 类是主要入口。它将 PDF 加载到内存，并提供搜索、验证以及提取签名数据（包括条形码）的方法。

**重要提示**：确保文件路径正确且 PDF 存在。常见新手错误？在 Windows 上使用反斜杠而未进行转义（应写成 `C:\\Documents\\file.pdf` 而不是 `C:\Documents\file.pdf`）。

## 实现指南

现在进入有趣的部分——编写代码在 PDF 中搜索条形码。

### 在文档中搜索条形码签名

本节展示如何扫描 PDF 并定位所有条形码签名。我们将把过程拆分为易于理解的步骤，并对每一步进行说明。

#### 步骤 1：初始化 Signature 对象

首先加载 PDF 文档：

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed.pdf"; // Replace with actual file path
Signature signature = new Signature(filePath);
```

**此处发生的事情**  
`Signature` 类打开 PDF 并为处理做好准备。可以把它想象成在文本编辑器中打开文件——将文档加载到内存以便操作。

**实际注意事项**  
如果处理用户上传的 PDF，请始终验证文件路径并在创建 `Signature` 对象前检查文件是否存在。这可以防止后期出现难以理解的错误。

#### 步骤 2：创建 BarcodeSearchOptions

配置条形码搜索方式：

```java
import com.groupdocs.signature.options.search.BarcodeSearchOptions;

// Configure options for searching barcodes
BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setAllPages(true); // Search every page in the document
```

**关键配置选项**

- `setAllPages(true)`: 扫描所有页面。如果只想检查特定页面，请设为 `false` 并使用 `setPageNumber()` 配置。  
- **为何重要**：如果处理的发票条形码始终位于第 1 页，搜索所有页面会浪费资源。对于多页的装运清单，则需要 `setAllPages(true)`。

**专业提示**：您还可以按条形码类型进行过滤（详见下文 **支持的条形码类型** 部分）。当您明确所需格式时，这可以加快搜索速度。

#### 步骤 3：执行搜索并处理结果

现在执行搜索并处理结果：

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.util.List;

try {
    // Execute the barcode search
    List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);
    
    // Check if any barcodes were found
    if (signatures.isEmpty()) {
        System.out.println("No barcode signatures found in the document.");
    } else {
        System.out.println("Found " + signatures.size() + " barcode signature(s):\n");
        
        // Loop through each barcode and display details
        for (BarcodeSignature barcodeSignature : signatures) {
            System.out.println("----------------------------------------");
            System.out.println("Barcode Type: " + barcodeSignature.getEncodeType().getTypeName());
            System.out.println("Barcode Text: " + barcodeSignature.getText());
            System.out.println("Page Number: " + barcodeSignature.getPageNumber());
            System.out.println("Position: X=" + barcodeSignature.getLeft() + 
                             ", Y=" + barcodeSignature.getTop());
            System.out.println("Size: Width=" + barcodeSignature.getWidth() + 
                             ", Height=" + barcodeSignature.getHeight());
            System.out.println("----------------------------------------\n");
        }
    }
} catch (Exception e) {
    System.err.println("Error searching for barcodes: " + e.getMessage());
    e.printStackTrace();
} finally {
    // Always dispose of the signature object to free resources
    if (signature != null) {
        signature.dispose();
    }
}
```

**此代码的工作原理**

1. **搜索执行** – `signature.search()` 扫描 PDF 并返回 `BarcodeSignature` 对象列表。  
2. **空检查** – 验证是否真的找到了条形码（防止空指针异常）。  
3. **数据提取** – 对每个条形码提取：  
   - **类型** – 条形码格式（QR Code、Code128、EAN13 等）  
   - **文本** – 解码后的数据（订单号、跟踪码、SKU 等）  
   - **位置** – 页面号和 X/Y 坐标  
   - **尺寸** – 宽度和高度（用于验证）。  
4. **错误处理** – `try‑catch` 防止在出现问题（损坏的 PDF、文件缺失等）时崩溃。  
5. **资源清理** – `finally` 块确保 `Signature` 对象被正确释放，释放内存。

**实际应用**  
假设您在处理运单标签。您会提取 `getText()` 的值（跟踪号）并存入数据库。页面号可帮助您在批量文档处理中对应标签与相应的发货。

### 按条形码类型过滤

通过指定要查找的条形码类型，可加快搜索速度：

```java
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setEncodeType(BarcodeTypes.QR); // Only search for QR codes
options.setAllPages(true);
```

**何时过滤**  
如果您知道发票仅包含 Code128 条形码，按类型过滤可在大型文档上将处理时间降低 30‑50 %。

## 支持的条形码类型

GroupDocs.Signature 能检测多种条形码格式。以下是可搜索的类型：

**1D 条形码（线性）**
- **Code128** – 常用于运输和包装  
- **Code39** – 用于汽车和国防行业  
- **EAN13/EAN8** – 零售产品条形码（每个商品上都有）  
- **UPC‑A/UPC‑E** – 北美零售标准  
- **Interleaved2of5** – 仓储和配送  

**2D 条形码（矩阵）**
- **QR Code** – 最流行的，用于 URL、Wi‑Fi 密码、支付信息等  
- **Data Matrix** – 适用于小件（电子元件）的紧凑格式  
- **PDF417** – 政府身份证、登机牌、驾照等  
- **Aztec Code** – 交通票据  

**按类型过滤**（如前例所示）可帮助您专注于所需的确切格式。

## 实际使用案例

以下是开发者在生产环境中使用条形码搜索的方式：

### 1. 自动化发票处理

**场景** – 会计部门每天收到 500 多份供应商 PDF 发票。  
**解决方案** – 扫描每个 PDF，查找包含发票号的 Code39 条形码，自动将其与 ERP 系统中的采购订单匹配。此举消除手动录入并降低错误率。

```java
// Pseudo-code workflow
for (PDF invoice : invoiceBatch) {
    List<BarcodeSignature> barcodes = searchBarcodes(invoice);
    String invoiceNumber = barcodes.get(0).getText();
    updateERPSystem(invoiceNumber, invoice);
}
```

### 2. 仓库库存更新

**场景** – 仓库收到的装运包含 PDF 装箱单，产品 SKU 以 EAN13 条形码形式呈现。  
**解决方案** – 从装箱单中提取所有条形码，自动更新库存计数，并标记差异以供审查。

### 3. 文档认证

**场景** – 法律文件包含用于真实性验证的带有加密签名的 QR 码。  
**解决方案** – 在已签署的合同中搜索 QR 码，解码签名数据，并与受信任的证书机构进行验证。此举确保文件未被篡改。

### 4. 医疗记录管理

**场景** – 医院的患者文件中，PDF 实验报告包含用于标本 ID 的 Code128 条形码。  
**解决方案** – 自动提取标本 ID，并将实验结果链接到医院信息系统（HIS）中的患者记录。

## 常见问题及解决方案

以下是您可能遇到的问题以及解决办法：

### 问题 1：“未找到条形码”（但您确认存在）

**可能原因**
- 条形码图像质量太低（模糊、像素化扫描）  
- PDF 为图像型，但条形码太小  
- 搜索的条形码类型不正确  

**解决方案**
1. **检查图像分辨率** – 条形码至少需要 200 DPI 才能可靠检测。扫描文档时请使用 300 DPI 或更高。  
2. **取消类型过滤** – 先搜索所有条形码类型（不要设置 `setEncodeType()`），确认文档中实际存在的类型后再进行过滤。  
3. **验证条形码质量** – 在 Adobe Acrobat 中打开 PDF 并放大查看。如果条形码看起来模糊，API 也难以识别。

### 问题 2：大 PDF 导致 `OutOfMemoryError`

**原因** – 加载包含高分辨率图像的 500 页 PDF 会消耗大量内存。  

**解决方案**
1. **批量处理页面** – 不使用 `setAllPages(true)`，而是一次处理 50 页：

```java
for (int startPage = 1; startPage <= totalPages; startPage += 50) {
    BarcodeSearchOptions options = new BarcodeSearchOptions();
    options.setPageNumber(startPage);
    options.setPagesSetup(new PagesSetup());
    options.getPagesSetup().setLastPage(Math.min(startPage + 49, totalPages));
    
    List<BarcodeSignature> batchResults = signature.search(BarcodeSignature.class, options);
    // Process results...
}
```

2. **增加 JVM 堆大小** – 在 Java 命令中添加 `-Xmx4g` 以分配 4 GB 内存（根据需求调整）。

### 问题 3：多页文档性能慢

**原因** – 顺序搜索所有页面需要时间，尤其是像 PDF417 这种复杂条形码。  

**解决方案**
1. **并行处理** – 如果条形码始终位于特定页面（例如发票的第 1 页），仅搜索这些页面。  
2. **缓存结果** – 若多次处理同一文档，可缓存条形码数据以避免重复扫描。  
3. **使用 SSD** – 加载大 PDF 时 I/O 速度至关重要。SSD 相比 HDD 可将加载时间降低 60‑70 %。

### 问题 4：误报（将随机图案识别为条形码）

**原因** – 表格、网格或线条图案可能被误识别为条形码。  

**解决方案** – 通过检查解码文本的长度和格式来验证结果：

```java
for (BarcodeSignature barcode : signatures) {
    String text = barcode.getText();
    
    // Example: Invoice numbers are always 10 digits
    if (text.matches("\\d{10}")) {
        // Valid invoice number
        processBarcode(barcode);
    } else {
        System.out.println("Skipping invalid barcode: " + text);
    }
}
```

## 大文档性能优化技巧

需要处理成千上万的 PDF？以下是优化方法：

### 1. 批处理策略

不要逐个处理文件，使用线程池同时处理多个 PDF：

```java
ExecutorService executor = Executors.newFixedThreadPool(4); // 4 parallel threads

for (String pdfPath : pdfFiles) {
    executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            List<BarcodeSignature> results = sig.search(BarcodeSignature.class, options);
            // Process results...
        } catch (Exception e) {
            e.printStackTrace();
        }
    });
}

executor.shutdown();
executor.awaitTermination(1, TimeUnit.HOURS);
```

**性能提升** – 在四核机器上，处理 1 000 个文件的时间从约 2 小时降至约 30 分钟。

### 2. 缩小搜索范围

如果业务逻辑允许，可限制搜索区域：

```java
// Only search the top‑right corner where barcodes are typically placed
options.setRectangle(new Rectangle(400, 50, 150, 150)); // X, Y, Width, Height
```

**性能提升** – 在条形码位置固定的文档上提升 40‑60 %。

### 3. 监控内存使用

对于长时间运行的批处理，监控堆使用情况，并在需要时显式触发垃圾回收：

```java
Runtime runtime = Runtime.getRuntime();
long usedMemory = runtime.totalMemory() - runtime.freeMemory();

if (usedMemory > (runtime.maxMemory() * 0.8)) {
    System.gc(); // Suggest garbage collection
}
```

## 最佳实践

遵循以下指南编写生产就绪代码：

### 1. 始终释放 Signature 对象

使用 try‑with‑resources（Java 7+）包装代码，以自动关闭资源：

```java
try (Signature signature = new Signature(filePath)) {
    // Your search code here...
} // Automatically disposed
```

### 2. 验证输入文件

处理前，检查文件是否存在且为有效的 PDF：

```java
File pdfFile = new File(filePath);
if (!pdfFile.exists() || !pdfFile.canRead()) {
    throw new FileNotFoundException("PDF not found or not readable: " + filePath);
}

// Optional: Verify it's actually a PDF (check magic bytes)
```

### 3. 记录条形码检测结果

为调试和审计，记录检测到的内容：

```java
Logger logger = Logger.getLogger(BarcodeSearcher.class.getName());

for (BarcodeSignature barcode : signatures) {
    logger.info(String.format("Detected %s barcode '%s' on page %d at (%.2f, %.2f)",
        barcode.getEncodeType().getTypeName(),
        barcode.getText(),
        barcode.getPageNumber(),
        barcode.getLeft(),
        barcode.getTop()));
}
```

### 4. 处理不同的条形码格式

不同行业使用不同标准。让代码保持灵活性：

```java
switch (barcode.getEncodeType().getTypeName()) {
    case "QR":
        // QR codes might contain URLs or JSON data
        processQRCode(barcode.getText());
        break;
    case "Code128":
        // Code128 typically contains alphanumeric order/tracking numbers
        processTrackingNumber(barcode.getText());
        break;
    default:
        logger.warning("Unexpected barcode type: " + barcode.getEncodeType());
}
```

### 5. 使用真实文档进行测试

不要仅使用完美的示例 PDF 进行测试。请使用生产环境中的真实文档：

- 带有咖啡渍的扫描发票  
- 带噪声的传真运单标签  
- 转换为 PDF 的低分辨率手机照片  

这会暴露演示中未出现的边缘情况。

## 常见问题

**Q: 是否可以在没有许可证的情况下读取 QR 码 PDF 文件？**  
A: 免费试用版可用于评估读取 QR 码 PDF 文件，但生产部署需要商业许可证。

**Q: API 是否支持受密码保护的 PDF？**  
A: 支持。创建 `Signature` 对象时可以传入密码，例如 `new Signature(filePath, "password")`。

**Q: 如何提升对低分辨率扫描的检测率？**  
A: 提高源扫描的 DPI（最低 200 DPI），并考虑按条形码类型过滤以减少误报。

**Q: 搜索在并行处理时是线程安全的吗？**  
A: 每个线程应使用各自的 `Signature` 实例。以这种方式使用时，API 本身是线程安全的。

**Q: 本教程使用的 GroupDocs.Signature 版本是什么？**  
A: 代码已在 GroupDocs.Signature 23.12 上验证通过。

## 结论

您已经学习了如何使用 Java 和 GroupDocs.Signature API **读取 QR 码 PDF** 文档。以下是我们覆盖的内容：

✅ **设置** – 将 GroupDocs.Signature 添加到项目并获取许可证选项  
✅ **实现** – 完整代码用于搜索、提取和处理条形码数据  
✅ **条形码类型** – 了解支持的格式（1D 与 2D）  
✅ **实际使用案例** – 发票处理、库存管理、文档认证、医疗记录  
✅ **故障排除** – 解决内存错误、误报等常见问题  
✅ **性能** – 为大规模文档处理优化搜索  

GroupDocs.Signature API 处理 PDF 解析和条形码检测的复杂性，让您专注于业务逻辑的构建。无论是自动化发票处理、验证运单标签，还是提取库存数据，您现在都有了可靠的解决方案。

---

**最后更新：** 2026-03-01  
**测试版本：** GroupDocs.Signature 23.12  
**作者：** GroupDocs