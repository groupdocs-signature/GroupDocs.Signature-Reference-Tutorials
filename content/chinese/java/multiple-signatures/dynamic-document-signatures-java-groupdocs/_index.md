---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 创建动态文本和条形码图像签名，提高电子签名效率。"
"title": "Java 中的动态文档签名——掌握 GroupDocs.Signature 的电子签名"
"url": "/zh/java/multiple-signatures/dynamic-document-signatures-java-groupdocs/"
"weight": 1
---

# 使用 GroupDocs 在 Java 中创建动态文档签名

在当今快节奏的数字世界中，高效地以电子方式签署文档的需求比以往任何时候都更加重要。无论您是希望简化合同审批流程的商务人士，还是管理个人文档的个人，电子签名都能提供快速便捷的服务。本教程将指导您使用 GroupDocs.Signature for Java 创建动态文本和条形码图像签名。通过利用拉伸模式，您的签名可以无缝适应整个页面，从而确保一致性和可读性。

**您将学到什么：**
- 如何将 GroupDocs.Signature for Java 集成到您的项目中。
- 创建具有全页宽度拉伸的文本签名的步骤。
- 实现跨越页面高度的条形码图像签名的技术。
- 电子签名在各种商业场景中的实际应用。

在开始编码之前，让我们深入了解先决条件。

## 先决条件
在踏上这段旅程之前，请确保您已准备好以下物品：

1. **所需的库和版本：**
   - 您需要 Java 版本 23.12 或更高版本的 GroupDocs.Signature。

2. **环境设置要求：**
   - 您的系统上安装了可运行的 Java 开发工具包 (JDK)。
   - 集成开发环境 (IDE)，例如 IntelliJ IDEA、Eclipse 或 NetBeans。

3. **知识前提：**
   - 对 Java 编程和 IDE 使用有基本的了解。
   - 熟悉 Maven 或 Gradle 的依赖管理将会很有帮助。

有了这些先决条件，让我们为您的 Java 项目设置 GroupDocs.Signature。

## 为 Java 设置 GroupDocs.Signature
要开始使用 GroupDocs.Signature for Java，您需要将其添加为依赖项。以下是使用不同构建工具执行此操作的方法：

**Maven：**

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle：**

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**直接下载：**  
如果您愿意，请直接从 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 许可证获取
在继续之前，请考虑获取许可证：
- **免费试用：** 从免费试用开始探索功能。
- **临时执照：** 如果您需要更多不受限制的时间，请提出请求。
- **购买：** 购买许可证以供长期使用。

通过创建以下实例来初始化 GroupDocs.Signature `Signature` 类。这将设置您的环境，为实施数字签名做好准备。

## 实施指南
现在我们的设置已经完成，让我们探索如何使用 GroupDocs.Signature 实现每个签名功能。

### 带拉伸模式的文本签名
此功能允许您添加横跨整个页面宽度的文本签名，确保可见性和一致性。

#### 概述
文本签名提供了一种简单的数字签名文档方法。通过将拉伸模式设置为 `PageWidth`，它可以动态适应不同的文档大小。

#### 实施步骤
**1.导入所需的类**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.StretchMode;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.TextSignOptions;
```

**2. 初始化签名实例**
创建一个 `Signature` 对象，指定文档的路径。

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Signature signature = new Signature(filePath);
```

**3. 配置文本签名选项**
使用所需的配置（例如对齐方式和边距）设置文本符号选项。

```java
TextSignOptions textOptions = new TextSignOptions("This is a test message");
textOptions.setAllPages(true);  // 应用于所有页面
textOptions.setVerticalAlignment(VerticalAlignment.Top);
textOptions.setMargin(new Padding(50));
textOptions.setStretch(StretchMode.PageWidth);
```

**4. 签署并保存文件**
最后，使用配置的选项对文档进行签名并保存。

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/TextSignatureWithStretch_signed.docx";
signature.sign(outputFilePath, textOptions);
```

### 带拉伸模式的条形码签名
此功能添加了跨越整个页面高度的条形码签名，以提高可视性。

#### 概述
条形码签名对于验证真伪和追踪文件至关重要。将拉伸模式设置为 `PageHeight`，它们在不同的文档尺寸上都保持清晰度。

#### 实施步骤
**1.导入所需的类**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.StretchMode;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;
```

**2. 初始化签名实例**

```java
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

**3.配置条形码签名选项**
调整条形码设置，包括类型和对齐。

```java
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456");
barcodeOptions.setAllPages(true);
barcodeOptions.setEncodeType(BarcodeTypes.Code128);
barcodeOptions.setVerticalAlignment(VerticalAlignment.Bottom);
barcodeOptions.setMargin(new Padding(50));
barcodeOptions.setStretch(StretchMode.PageWidth);
```

**4. 签署并保存文件**

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/BarcodeSignatureWithStretch_signed.docx";
signature.sign(outputFilePath, barcodeOptions);
```

### 具有拉伸模式的图像签名
此功能引入了垂直拉伸以覆盖页面高度的图像签名。

#### 概述
图像签名增添了个性化的触感。通过将拉伸模式设置为 `PageHeight`，它们可以有效地适应不同的文档大小。

#### 实施步骤
**1.导入所需的类**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.StretchMode;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.options.sign.ImageSignOptions;
```

**2. 初始化签名实例**

```java
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

**3. 配置图像签名选项**
定义图像设置，包括对齐和拉伸模式。

```java
ImageSignOptions imageOptions = new ImageSignOptions();
imageOptions.setAllPages(true);
imageOptions.setStretch(StretchMode.PageHeight);
imageOptions.setHorizontalAlignment(HorizontalAlignment.Right);
imageOptions.setImageFilePath("YOUR_DOCUMENT_DIRECTORY/image.png");
```

**4. 签署并保存文件**

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/ImageSignatureWithStretch_signed.docx";
signature.sign(outputFilePath, imageOptions);
```

## 实际应用
电子签名彻底改变了各行各业的文档管理。以下是一些实际应用：

1. **合同管理：** 简化法律和商业环境中的合同审批。
2. **教育机构：** 方便成绩单、证书等学生文件的签署。
3. **卫生保健：** 使用签署的同意书管理患者记录。
4. **房地产：** 通过数字签署协议来加快财产交易。

集成的可能性非常大，允许 CRM 或 ERP 等系统无缝地整合数字签名，以增强工作流程自动化。

## 性能考虑
使用 GroupDocs.Signature 时，请考虑以下优化性能的提示：
- **内存管理：** 有效管理文档处理过程中的内存使用情况，以确保顺利运行。