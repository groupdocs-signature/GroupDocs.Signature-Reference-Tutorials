---
categories:
- Document Processing
date: '2026-07-25'
description: 使用 GroupDocs.Signature 在 Java 中创建渐变数字签名。了解如何应用渐变画笔、定制外观以及排除常见问题。
keywords:
- create gradient digital signature
- gradient brush Java
- GroupDocs signature styling
- digital signature gradient
lastmod: '2026-07-25'
linktitle: Java 渐变签名教程
og_description: 使用 GroupDocs.Signature 在 Java 中创建渐变数字签名。本指南逐步展示如何使用渐变画笔为签名设定样式、配置位置以及处理常见问题。
og_image_alt: 'Guide: Create gradient digital signature in Java using GroupDocs.Signature'
og_title: 使用 Java 创建渐变数字签名 – GroupDocs 指南
schemas:
- author: GroupDocs
  dateModified: '2026-07-25'
  description: Create gradient digital signature in Java using GroupDocs.Signature.
    Learn how to apply gradient brushes, customize appearance, and troubleshoot common
    issues.
  headline: Create Gradient Digital Signature in Java with GroupDocs
  type: TechArticle
- description: Create gradient digital signature in Java using GroupDocs.Signature.
    Learn how to apply gradient brushes, customize appearance, and troubleshoot common
    issues.
  name: Create Gradient Digital Signature in Java with GroupDocs
  steps:
  - name: Initialise Signature Options
    text: 'First, we define what the signature will contain. The `TextSignOptions`
      class handles text‑based signatures. **Definition anchor**: `TextSignOptions`
      represents the configuration for a textual signature, including text content,
      font, colour, and visual effects. The snippet creates a basic signature '
  - name: Customise Background with Gradient Brush
    text: 'Next, we apply a linear gradient brush to give the signature a polished
      look. **Definition anchor**: `LinearGradientBrush` describes a colour transition
      that fills a shape along a straight line, defined by start and end colours and
      an angle. Key points: - `setColor(Color.GREEN)` provides a fallback '
  - name: Set Signature Positioning
    text: 'Now we tell the engine where to place the signature on the page. **Definition
      anchor**: `SignatureOptions` (the base class for all option types) holds common
      properties such as alignment, margins, and size. Understanding alignment vs.
      margin: - **Alignment** anchors the signature (e.g., `HorizontalA'
  - name: Apply Signature and Save
    text: 'Finally, we sign the document and write the result to a new file. **Definition
      anchor**: `SignResult` provides detailed information about the outcome of a
      signing operation, including succeeded and failed signatures. The `sign()` method
      takes the source file, applies the configured options, and crea'
  type: HowTo
- questions:
  - answer: Yes. GroupDocs.Signature is pure Java and works in any Java‑based backend,
      including Spring Boot, Jakarta EE, or microservice frameworks.
    question: Can I use this in a web‑based Java service?
  - answer: Only marginally. The gradient is stored as a visual appearance stream,
      typically adding a few kilobytes to the file.
    question: Does the gradient affect the size of the signed PDF?
  - answer: 'Pass the password when creating the `Signature` object: `new Signature("file.pdf",
      "password")`.'
    question: How do I sign password‑protected PDFs?
  - answer: Absolutely. Use `ImageSignOptions` and set its `Background` with a `LinearGradientBrush`
      just like the text example.
    question: Is it possible to apply the gradient to an image‑based signature instead
      of text?
  - answer: GroupDocs currently supports `LinearGradientBrush` only. For radial effects,
      generate a radial‑gradient PNG and use it as a background image.
    question: What if I need a radial gradient instead of linear?
  type: FAQPage
tags:
- java
- digital-signature
- groupdocs
- pdf-signing
- document-styling
- gradient signature
title: 使用 GroupDocs 在 Java 中创建渐变数字签名
type: docs
url: /zh/java/advanced-options/sign-document-gradient-brush-java-groupdocs/
weight: 1
---

# 在 Java 中使用 GroupDocs 创建渐变数字签名

如果您需要 **create gradient digital signature** 对象，使其外观精致、符合品牌颜色，并且仍然满足加密标准，您来对地方了。在本教程中，我们将逐步讲解您需要的所有内容——从将 GroupDocs.Signature 库添加到项目中，到配置线性渐变画笔、定位签名以及处理最常见的陷阱。完成后，您只需几行 Java 代码即可在 PDF、Word 文件或图像中嵌入视觉上吸引人的渐变签名。

## 快速答案
- **什么是渐变数字签名？** 使用颜色渐变作为背景或文字填充的数字签名可视元素。  
- **哪个库在 Java 中支持此功能？** GroupDocs.Signature for Java 提供内置的渐变画笔支持。  
- **渐变会影响加密安全性吗？** 不会。渐变纯粹是视觉效果；底层数字签名保持不变。  
- **需要哪个 Java 版本？** JDK 8 或更高（推荐 JDK 11+）。  
- **生产环境需要许可证吗？** 是的——非评估使用必须拥有有效的 GroupDocs.Signature 许可证。

## 为什么在数字签名中使用渐变画笔？

渐变画笔可以为签名的背景添加符合品牌的颜色过渡，使已签署的文档显得更专业、更可信。渐变签名提升视觉层次感，帮助区分审批级别，并在不影响签名加密完整性的前提下强化企业形象。

## 本教程您将学习

在本教程中，您将学习如何配置 GroupDocs.Signature 库、创建带有渐变样式的文字签名、调整颜色、透明度和位置等视觉属性，并解决实现过程中常见的问题。指南还涵盖性能优化技巧以及保持签名代码整洁、可复用的最佳实践模式。

- 设置 GroupDocs.Signature for Java（Maven、Gradle 或手动）  
- 使用线性渐变画笔创建 **create gradient digital signature** 对象  
- 自定义外观、定位和透明度  
- 排查常见问题并优化性能  
- 应用最佳实践模式编写可维护的签名代码  

## 前置条件

在开始之前，请确保您具备以下条件：

- **Java Development Kit (JDK)** 8 或更高（推荐 JDK 11+）  
- **IDE** （IntelliJ IDEA、Eclipse 或带有 Java 扩展的 VS Code）  
- **GroupDocs.Signature for Java** 库（通过 Maven、Gradle 或手动 JAR 添加）  
- 对 Java 对象、方法和异常处理有基本了解  

### 必需的库

使用您偏好的构建工具将 GroupDocs.Signature 添加到项目中。

**针对 Maven**（添加到您的 `pom.xml`）：
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**针对 Gradle**（添加到您的 `build.gradle`）：
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**手动安装**：如果您不使用构建工具（虽然我们推荐使用），请从 [GroupDocs Signatures releases](https://releases.groupdocs.com/signature/java/) 下载 JAR 并将其加入类路径。

### 许可证获取

GroupDocs 提供免费试用供开发使用，但商业部署必须购买生产许可证。

1. **免费试用** – 从 [GroupDocs Free Trial](https://releases.groupdocs.com/) 下载  
2. **临时许可证** – 从 [GroupDocs Temporary License](https://purchase.groupdocs.com/temporary-license/) 获取 30 天密钥，以进行完整功能测试  
3. **正式许可证** – 通过定价门户购买，用于生产部署  

试用版会添加评估水印，请在向客户发布应用之前获取临时或正式许可证。

## 设置 GroupDocs.Signature（Java）

让我们准备好环境。此方法适用于新项目，也适用于集成到已有代码库中。

### 安装步骤

1. **添加依赖**（如上所述）。  
2. **通过创建一个简单的测试类来验证安装**：

```java
import com.groupdocs.signature.Signature;

public class SignatureTest {
    public static void main(String[] args) {
        System.out.println("GroupDocs.Signature loaded successfully!");
    }
}
```

如果此代码编译无误，您即可继续下一步。

3. **组织文档文件夹** – 干净的结构有助于处理大量文件：

```
project-root/
├── src/
├── resources/
│   ├── input/        // Source documents to sign
│   └── output/       // Signed documents
└── pom.xml (or build.gradle)
```

4. **基本初始化** – `Signature` 对象是所有签名操作的入口：

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

public class BasicSignatureSetup {
    public static void main(String[] args) {
        try {
            // Initialize with your source document path
            Signature signature = new Signature("resources/input/sample.pdf");
            
            // Your signing code will go here
            
            signature.dispose(); // Always clean up resources
        } catch (GroupDocsSignatureException e) {
            System.err.println("Signature error: " + e.getMessage());
            e.printStackTrace();
        } catch (Exception e) {
            System.err.println("General error: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

**专业提示**：将 `Signature` 实例放在 try‑with‑resources 块中，或手动调用 `dispose()`。忘记释放文件句柄会导致 “file in use” 错误。

## 实现指南：创建渐变签名

接下来，我们将一步步构建一个 **create gradient digital signature**。

### 步骤 1：初始化签名选项

首先，定义签名将包含的内容。`TextSignOptions` 类处理基于文本的签名。

**定义锚点**：`TextSignOptions` 表示文本签名的配置，包括文本内容、字体、颜色和视觉效果。

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.TextSignOptions;

TextSignOptions options = new TextSignOptions("John Smith");
```

该代码片段创建了一个基本签名，内容为 “John Smith”。默认情况下，它会以纯黑文字显示在透明背景上——并不吸引人。

### 步骤 2：使用渐变画笔自定义背景

接下来，应用线性渐变画笔为签名增添精致外观。

**定义锚点**：`LinearGradientBrush` 描述沿直线填充形状的颜色过渡，由起始颜色、结束颜色和角度定义。

```java
import com.groupdocs.signature.domain.Background;
import com.groupdocs.signature.domain.extensions.brushes.LinearGradientBrush;
import java.awt.Color;

// Create the background container
Background background = new Background();
background.setColor(Color.GREEN);        // Fallback color (rarely seen)
background.setTransparency(0.5f);         // 50% transparency (0.0 = opaque, 1.0 = invisible)

// Define the gradient: start color, end color, and angle
LinearGradientBrush brush = new LinearGradientBrush(
    Color.GREEN,    // Start color (left/top)
    Color.WHITE,    // End color (right/bottom)
    45              // Angle in degrees (45 = diagonal)
);

// Apply the brush to the background
background.setBrush(brush);
options.setBackground(background);
```

关键点：

- `setColor(Color.GREEN)` 在无法渲染渐变时提供后备的纯色。  
- `setTransparency(0.5f)` 使签名半透明，防止遮挡底层文字。接近 0 的值不透明，接近 1 的值几乎不可见。  
- 角度 `45` 产生从左上到右下的对角过渡。使用 `0` 表示水平，`90` 表示垂直，或任意介于两者之间的角度。

选择与品牌相匹配的颜色（例如，蓝‑白表示信任，绿‑白表示批准）可让签名瞬间被识别。

### 步骤 3：设置签名位置

现在告诉引擎在页面的何处放置签名。

**定义锚点**：`SignatureOptions`（所有选项类型的基类）保存对齐、边距和尺寸等通用属性。

```java
import com.groupdocs.signature.domain.Padding;

// Set signature dimensions (in pixels or points, depending on document)
options.setWidth(100);
options.setHeight(80);

// Center the signature both horizontally and vertically
options.setVerticalAlignment(VerticalAlignment.Center);
options.setHorizontalAlignment(HorizontalAlignment.Center);

// Add margins to fine‑tune positioning
Padding padding = new Padding();
padding.setTop(20);      // 20 units from the alignment point
padding.setRight(20);    // 20 units from the right edge
options.setMargin(padding);
```

对齐与边距的区别：

- **Alignment** 锚定签名（例如 `HorizontalAlignment.Right`）。  
- **Margin** 偏移锚定点（例如 `setMarginTop(-10)`）。  

常用模式：

| Desired location | HorizontalAlignment | VerticalAlignment | Typical margin values |
|------------------|--------------------|-------------------|-----------------------|
| Bottom‑right     | Right              | Bottom            | `setMarginTop(-20)`   |
| Header area      | Right              | Top               | `setMarginTop(20)`    |
| Center of page   | Center             | Center            | `setMarginLeft(0)`    |

根据文本长度和文档页面大小调整 `setWidth` 和 `setHeight`。

### 步骤 4：应用签名并保存

**定义锚点**：`SignResult` 提供签名操作结果的详细信息，包括成功和失败的签名。

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.SignResult;

try {
    // Initialize signature with source document
    Signature signature = new Signature("resources/input/sample.pdf");
    
    // Apply the signature options we configured above
    SignResult result = signature.sign("resources/output/SignedWithGradient.pdf", options);
    
    // Check the result
    if (result.getSucceeded().size() > 0) {
        System.out.println("Document signed successfully!");
        System.out.println("Signed with " + result.getSucceeded().size() + " signature(s)");
    } else {
        System.out.println("No signatures were applied.");
    }
    
    // Clean up
    signature.dispose();
    
} catch (Exception e) {
    System.err.println("Error signing document: " + e.getMessage());
    e.printStackTrace();
}
```

`sign()` 方法接受源文件，应用配置好的选项，并生成一个包含可视签名的新文件，同时保持原文件不变。务必检查 `signResult.getSucceeded()` 以确认成功。

## 完整工作示例

以下是全部代码合并成的可直接运行的类，您可以复制并立即测试：

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Background;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.SignResult;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.extensions.brushes.LinearGradientBrush;
import com.groupdocs.signature.domain.signatures.TextSignOptions;
import java.awt.Color;

public class GradientSignatureExample {
    public static void main(String[] args) {
        try {
            // Initialize signature object with source document
            Signature signature = new Signature("resources/input/sample.pdf");
            
            // Configure text signature options
            TextSignOptions options = new TextSignOptions("John Smith");
            
            // Create gradient background
            Background background = new Background();
            background.setColor(Color.GREEN);
            background.setTransparency(0.5f);
            
            LinearGradientBrush brush = new LinearGradientBrush(
                Color.GREEN,  // Start color
                Color.WHITE,  // End color
                45            // Angle
            );
            
            background.setBrush(brush);
            options.setBackground(background);
            
            // Set positioning
            options.setWidth(100);
            options.setHeight(80);
            options.setVerticalAlignment(VerticalAlignment.Center);
            options.setHorizontalAlignment(HorizontalAlignment.Center);
            
            Padding padding = new Padding();
            padding.setTop(20);
            padding.setRight(20);
            options.setMargin(padding);
            
            // Sign and save
            SignResult result = signature.sign(
                "resources/output/SignedWithGradient.pdf", 
                options
            );
            
            System.out.println("Success! Signatures applied: " + 
                result.getSucceeded().size());
            
            signature.dispose();
            
        } catch (Exception e) {
            System.err.println("Error: " + e.getMessage());
            e.printStackTrace();
        }
    }
}
```

将 PDF 放置在 `resources/input/` 目录下运行程序；输出文件将包含一个时尚的渐变签名。

## 常见使用场景

### 1. 企业合同管理

不同的审批层级可以使用不同的渐变颜色可视化——例如，经理使用蓝‑白，法务使用金‑白，执行层使用深蓝‑浅蓝。此视觉层次让审阅者瞬间辨认出签署人。

### 2. 自动发票处理

在发送给客户的发票上应用细微的品牌渐变色。效果专业且不影响文档可读性。

### 3. 证书生成

在证书上使用鲜艳的渐变（紫‑粉、金‑黄）使其显得正式且值得分享。视觉吸引力提升感知价值。

### 4. 文档水印

复用渐变技术并使用透明文字创建 “Draft”、 “Confidential” 或 “Approved” 水印，既不遮挡底层内容，又能传达状态。将透明度设为 0.7‑0.8 可获得柔和效果。

## 常见问题排查

下面列出我在使用渐变签名时遇到（并解决）的常见问题。

### 问题 1：“文件被另一个进程占用”

**直接回答（40‑70 字）**：该异常是因为 `Signature` 对象仍持有打开的文件句柄。签名后务必关闭或释放 `Signature` 实例。使用 try‑with‑resources 块可自动释放文件，避免后续操作出现 “file in use” 错误。

**解决方案**：
```java
// Always use try‑with‑resources (Java 7+)
try (Signature signature = new Signature("path/to/document.pdf")) {
    // Your signing code here
} catch (Exception e) {
    // Handle errors
}
// File handle automatically released when try block exits
```
或手动方式：
```java
Signature signature = null;
try {
    signature = new Signature("path/to/document.pdf");
    // Your signing code
} finally {
    if (signature != null) {
        signature.dispose();
    }
}
```

### 问题 2：签名出现但渐变未显示

**直接回答**：如果查看器不支持、透明度设为 1.0，或画笔未正确附加，渐变可能不可见。请确认使用的 PDF 查看器（Adobe Acrobat、Foxit 或现代浏览器），将透明度设在 0.3‑0.7 之间，并确保已调用 `background.setBrush(brush)` 与 `options.setBackground(background)`。

**可能原因**：

1. 查看器不支持渐变 – 使用现代查看器进行测试。  
2. 透明度设置过高 – 降低至 0.3‑0.7。  
3. 画笔未应用 – 再次检查方法调用。

**调试提示**：先使用高对比度颜色（如红‑蓝）确认渐变渲染成功，再进行细调。

### 问题 3：签名覆盖重要文档内容

**直接回答**：当定位值将签名放置在已有文字或表单字段上方时会出现覆盖。可动态计算空白区域或使用页面级分析自动重新定位签名。

**解决方案模式**：
```java
// For documents with content primarily at the top
options.setVerticalAlignment(VerticalAlignment.Bottom);
Padding padding = new Padding();
padding.setBottom(30);  // Leave space from bottom edge
options.setMargin(padding);

// For documents that need signatures in specific locations
options.setVerticalAlignment(VerticalAlignment.Top);
options.setHorizontalAlignment(HorizontalAlignment.Left);
padding.setTop(600);     // Absolute Y position
padding.setLeft(400);    // Absolute X position
options.setMargin(padding);
```

### 问题 4：大型文档的性能问题

**直接回答**：对大型 PDF 进行签名可能较慢，因为 GroupDocs 会处理整个文件并为每页渲染渐变。可限制仅在特定页签名，使用更简单的双色渐变，减小签名尺寸，并采用异步方式执行，以保持 UI 响应。

**性能示例**：
```java
// Faster configuration
TextSignOptions options = new TextSignOptions("Approved");
options.setWidth(80);   // Smaller than default 100
options.setHeight(60);  // Smaller than default 80

// Simple horizontal gradient (fastest)
LinearGradientBrush brush = new LinearGradientBrush(
    Color.BLUE, 
    Color.WHITE, 
    0  // Horizontal gradient
);
```

### 问题 5：颜色不符合预期

**直接回答**：颜色偏差可能来源于 RGB 到 PDF 颜色空间的转换、透明度混合或显示器校准差异。请使用精确的 sRGB 值，保持透明度在 0.3‑0.5 之间，并在多个查看器上测试，以确保品牌颜色一致。

## 生产环境的最佳实践

| 实践 | 原因 |
|----------|----------------|
| 在辅助类中集中样式 | 确保所有文档外观一致 |
| 在签名前验证源文档 | 防止损坏文件中断签名流水线 |
| 记录每一次签名操作 | 为合规提供审计轨迹 |
| 优雅地处理异常 | 在意外情况下保持服务稳定 |
| 使用真实场景的 PDF 进行测试（表单、扫描图像、已有签名） | 确保所有情况下均能正确渲染渐变 |

**辅助类示例**：
```java
public class SignatureStyles {
    public static TextSignOptions getApprovalSignature(String signerName) {
        TextSignOptions options = new TextSignOptions(signerName);
        
        Background background = new Background();
        background.setTransparency(0.4f);
        
        LinearGradientBrush brush = new LinearGradientBrush(
            new Color(0, 102, 204),  // Brand blue
            Color.WHITE,
            45
        );
        
        background.setBrush(brush);
        options.setBackground(background);
        
        // Standard positioning
        options.setWidth(100);
        options.setHeight(70);
        
        return options;
    }
    
    // Add more style methods as needed
}
```

**文档验证代码片段**：
```java
try {
    Signature signature = new Signature("path/to/document.pdf");
    
    // Validate format
    if (!"PDF".equalsIgnoreCase(signature.getDocumentInfo().getFileType())) {
        throw new IllegalArgumentException("Only PDF files supported");
    }
    
    // Ensure at least one page
    if (signature.getDocumentInfo().getPageCount() < 1) {
        throw new IllegalArgumentException("Document has no pages");
    }
    
    // Proceed with signing...
    
} catch (Exception e) {
    // Handle validation errors
}
```

**日志记录示例**：
```java
SignResult result = signature.sign(outputPath, options);
logger.info("Document signed: " + outputPath);
logger.info("Signatures applied: " + result.getSucceeded().size());
logger.info("Signer: " + signerName);
logger.info("Timestamp: " + LocalDateTime.now());

if (!result.getFailed().isEmpty()) {
    logger.warn("Failed signatures: " + result.getFailed().size());
}
```

**异常处理模式**：
```java
try {
    SignResult result = signature.sign(outputPath, options);
    return result.getSucceeded().size() > 0;
} catch (GroupDocsSignatureException e) {
    logger.error("Signature error: " + e.getMessage());
    return false;
} catch (IOException e) {
    logger.error("File I/O error: " + e.getMessage());
    return false;
} catch (Exception e) {
    logger.error("Unexpected error during signing: " + e.getMessage());
    return false;
}
```

## 高级用户的专业提示

### 提示 1：创建自定义配色方案

```java
public class BrandColors {
    public static final Color PRIMARY   = new Color(0, 102, 204);
    public static final Color SECONDARY = new Color(102, 178, 255);
    public static final Color ACCENT    = new Color(255, 193, 7);
    
    public static LinearGradientBrush getPrimaryGradient(int angle) {
        return new LinearGradientBrush(PRIMARY, Color.WHITE, angle);
    }
}
```

### 提示 2：基于文档类型的动态透明度

```java
public static float getOptimalTransparency(Signature signature) {
    if (hasComplexBackground(signature)) {
        return 0.6f; // More transparent for image‑heavy docs
    }
    return 0.4f;
}
```

### 提示 3：使用线程池进行批处理

```java
ExecutorService executor = Executors.newFixedThreadPool(4);
List<String> files = getDocumentsToSign();

for (String file : files) {
    executor.submit(() -> {
        try {
            signDocument(file);
        } catch (Exception e) {
            logger.error("Failed to sign: " + file, e);
        }
    });
}
executor.shutdown();
executor.awaitTermination(5, TimeUnit.MINUTES);
```

### 提示 4：基于签名类型的条件样式

```java
public static TextSignOptions getStyledSignature(String name, SignatureType type) {
    TextSignOptions options = new TextSignOptions(name);
    LinearGradientBrush brush;
    switch (type) {
        case APPROVAL:   brush = new LinearGradientBrush(Color.GREEN, Color.WHITE, 45); break;
        case REJECTION:  brush = new LinearGradientBrush(Color.RED,   Color.WHITE, 45); break;
        case REVIEW:     brush = new LinearGradientBrush(Color.ORANGE,Color.WHITE,45); break;
        default:         brush = new LinearGradientBrush(Color.BLUE,  Color.WHITE,45);
    }
    Background bg = new Background();
    bg.setBrush(brush);
    bg.setTransparency(0.5f);
    options.setBackground(bg);
    return options;
}
```

## 常见问题

**Q: 我可以在基于 Web 的 Java 服务中使用吗？**  
A: 可以。GroupDocs.Signature 纯 Java 实现，能够在任何基于 Java 的后端运行，包括 Spring Boot、Jakarta EE 或微服务框架。

**Q: 渐变会影响已签署 PDF 的文件大小吗？**  
A: 影响极小。渐变作为视觉外观流存储，通常只会为文件增加几千字节。

**Q: 如何签署受密码保护的 PDF？**  
A: 在创建 `Signature` 对象时传入密码，例如 `new Signature("file.pdf", "password")`。

**Q: 能否将渐变应用于基于图像的签名而不是文字？**  
A: 完全可以。使用 `ImageSignOptions` 并像文字示例一样为其 `Background` 设置 `LinearGradientBrush`。

**Q: 如果需要径向渐变而不是线性渐变怎么办？**  
A: 目前 GroupDocs 仅支持 `LinearGradientBrush`。若需径向效果，可生成径向渐变 PNG 并将其作为背景图像使用。

---

**Last Updated:** 2026-07-25  
**Tested With:** GroupDocs.Signature 23.12 for Java  
**Author:** GroupDocs

## 相关教程

- [在 Java 中加载和保存文档 - 完整 GroupDocs.Signature 教程](/signature/java/document-loading-saving/)
- [在 Java 中向 PDF 添加文字签名 - 完整 GroupDocs 教程](/signature/java/text-signatures/implement-text-signatures-groupdocs-java/)
- [Java 签名验证教程 - 搜索与验证数字签名](/signature/java/search-verification/)