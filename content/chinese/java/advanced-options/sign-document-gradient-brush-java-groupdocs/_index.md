---
categories:
- Document Processing
date: '2026-03-14'
description: 学习如何在 Java 中使用 GroupDocs.Signature 通过渐变效果自定义签名外观。包括完整的代码示例和故障排除。
keywords: java digital signature with gradient effect, customize document signature
  appearance java, groupdocs signature gradient brush tutorial, java pdf signature
  styling, gradient brush document signing java code
lastmod: '2026-03-14'
linktitle: Java Gradient Signature Tutorial
tags:
- java
- digital-signature
- groupdocs
- pdf-signing
- document-styling
title: 如何在 Java 中使用渐变自定义签名外观
type: docs
url: /zh/java/advanced-options/sign-document-gradient-brush-java-groupdocs/
weight: 1
---

 keep markdown formatting, code placeholders unchanged.

Proceed to craft final answer.# 如何在 Java 中使用渐变自定义签名外观

你是否注意到有些电子签名的文档看起来很…无聊？仅仅是白色背景上的普通文字？如果你正在构建需要专业外观文档签名的应用——比如合同、发票或证书——你会希望它既突出又实用。**在本教程中，你将学习如何在 Java 中通过使用渐变画笔来自定义签名外观。** 创建渐变数字签名不仅能提升视觉效果，还能强化品牌形象并提升感知的真实性。

## 快速答案
- **什么是渐变数字签名？** 使用颜色渐变作为背景或文字填充的数字签名可视元素。  
- **哪个库在 Java 中支持此功能？** GroupDocs.Signature for Java 提供内置的渐变画笔支持。  
- **渐变会影响加密安全性吗？** 不会。渐变纯粹是视觉效果；底层的数字签名保持不变。  
- **需要哪个 Java 版本？** JDK 8 或更高（推荐 JDK 11+）。  
- **生产环境是否需要许可证？** 是——非评估使用必须拥有有效的 GroupDocs.Signature 许可证。

## 如何在 Java 中使用渐变画笔自定义签名外观
在本节中，我们将完整演示整个过程——从设置库到对文本签名应用线性渐变画笔。完成后，你将能够 **创建渐变数字签名** 对象，使其外观精致并匹配品牌颜色。

## 为什么在数字签名中使用渐变画笔？

在深入代码之前，先来聊聊为什么要使用渐变效果。

**品牌一致性**：如果公司使用特定的配色方案，渐变签名有助于在所有文档中保持视觉一致性。金融服务公司可能使用蓝到白的渐变来传递信任，创意机构则可能使用鲜艳的颜色过渡来突出创意。

**文档层级**：渐变效果可以帮助区分不同类型的签名。你可以为标准批准使用细微的渐变，为高管签署或法律授权使用更显眼的渐变。

**不妥协的视觉吸引力**：这里的好处是——在不牺牲数字签名的加密安全性的前提下，你可以获得专业的样式。渐变纯粹是视觉层面的；签名的有效性保持完整。

**降低伪造感知**：带样式的签名往往让终端用户觉得更真实。虽然这并不会提升实际安全性，但能提升感知的合法性（这对用户信任很重要）。

## 你将学到

完成本指南后，你将能够：

- 在项目中设置 GroupDocs.Signature for Java（Maven、Gradle 或手动方式）  
- 使用线性渐变画笔创建基于文本的签名  
- **自定义签名外观**、位置和透明度  
- 排查开发者常见的错误  
- 为生产环境优化性能  
- 应用可维护签名代码的最佳实践  

## 前置条件

在开始之前，请确保你具备以下条件：

- **Java Development Kit (JDK)**：8 版或更高（推荐 JDK 11+ 以获得更佳性能）  
- **IDE**：IntelliJ IDEA、Eclipse 或带有 Java 扩展的 VS Code  
- **GroupDocs.Signature for Java Library**：我们将在后面通过 Maven 或 Gradle 添加  
- **基础 Java 知识**：应熟悉对象、方法和异常处理  

### 必需的库

使用你喜欢的构建工具将 GroupDocs.Signature 添加到项目中。

**对于 Maven**（添加到 `pom.xml`）：
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**对于 Gradle**（添加到 `build.gradle`）：
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**手动安装**：如果不使用构建工具（虽然建议使用），可以直接从 [GroupDocs 签名发布](https://releases.groupdocs.com/signature/java/) 下载 JAR 文件并将其加入项目的类路径。

### 许可证获取

GroupDocs 提供免费试用，适合测试和开发。生产使用时需要许可证。以下是获取方式：

1. **免费试用**：访问 [GroupDocs 免费试用](https://releases.groupdocs.com/) 下载，无需任何承诺  
2. **临时许可证**：从 [GroupDocs 临时许可证](https://purchase.groupdocs.com/temporary-license/) 获取 30 天的临时许可证，以进行全功能测试  
3. **正式许可证**：准备投入生产时，可查看其定价选项  

试用版会有评估水印，若要构建面向客户的产品，请获取临时许可证。

## 设置 GroupDocs.Signature for Java

让我们准备好开发环境。无论是新项目还是在已有应用中集成，此设置都适用。

### 安装步骤

**1. 添加依赖**（我们已在上面介绍——Maven 或 Gradle）

**2. 通过创建一个简单的测试类来验证安装**：

```java
import com.groupdocs.signature.Signature;

public class SignatureTest {
    public static void main(String[] args) {
        System.out.println("GroupDocs.Signature loaded successfully!");
    }
}
```

如果能够成功编译且没有错误，则说明环境已就绪。

**3. 设置文档目录结构**。我喜欢这样组织：

```
project-root/
├── src/
├── resources/
│   ├── input/        // Source documents to sign
│   └── output/       // Signed documents
└── pom.xml (or build.gradle)
```

**4. 基本初始化**（魔法从这里开始）：

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

**小贴士**：始终在 `try‑with‑resources` 语句中包装你的 `Signature` 对象，或手动调用 `dispose()`。GroupDocs 会持有文件句柄，忘记释放会导致“文件被占用”错误（我就是这么知道的）。

## 实现指南：创建渐变签名

现在进入有趣的部分——构建带有渐变画笔效果的签名。我们将从简单开始，逐步加入复杂度。

### 步骤 1：初始化签名选项

首先，定义签名的文本内容及其行为。`TextSignOptions` 类负责基于文本的签名：

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.TextSignOptions;

TextSignOptions options = new TextSignOptions("John Smith");
```

这会创建一个文本为 “John Smith” 的基础签名。看起来很普通，对吧？仅仅是透明背景上的黑色文字——很无聊。这时就需要渐变了。

**为什么要把选项与签名对象分离？** 这种设计模式可以让你在多个文档中复用同一套签名配置。只需设置一次，即可在任何地方使用。

### 步骤 2：使用渐变画笔自定义背景

这里是签名变得专业的地方。我们将创建一个从绿色到白色的线性渐变：

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

**下面逐项解释发生了什么：**

- **基础颜色**：`setColor(Color.GREEN)` 设置了一个固体回退颜色。如果渐变失败（极少见），会使用该颜色。  
- **透明度**：`setTransparency(0.5f)` 让签名半透明。这对于不想遮挡文档底层文字的场景至关重要。数值越接近 0 越不透明，越接近 1 越透明。  
- **渐变角度**：`45` 表示渐变从左上角向右下角对角线方向流动。`0` 为水平（左→右），`90` 为垂直（上→下），其他角度则介于两者之间。

**颜色选择很重要**：绿色到白色暗示批准或确认（类似“通行”信号）。蓝到白传递信任与专业感。红到白可能表示紧急或重要。请选择与文档目的及品牌形象相符的配色。

### 步骤 3：设置签名位置

接下来，需要告诉系统签名 **出现在哪里**。定位比看起来更复杂，因为要兼顾可见性与不遮挡重要内容：

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

**对齐方式 vs. 边距**：把对齐方式视为锚点，边距是相对于该锚点的偏移。若将 `HorizontalAlignment.Center` 设置为页面中心，然后通过边距进行微调，就能实现精确控制。

**常见定位模式**：

- **右下角**：`HorizontalAlignment.Right`、`VerticalAlignment.Bottom`，并使用负的上边距  
- **页眉区域**：`VerticalAlignment.Top`、`HorizontalAlignment.Right`，加上适当的内边距  
- **页面中心**：水平和垂直对齐均设为 `Center`，根据需要调整边距  

**尺寸考虑**：`setWidth(100)` 与 `setHeight(80)` 适用于大多数标准文档，但根据文档大小和签名文本长度可能需要调整。如果文字被截断，请增大宽度；若显得过于拥挤，可增高或减小字体大小。

### 步骤 4：应用签名并保存

最后，签署文档并输出文件。所有配置将在这里汇聚：

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

**`sign()` 方法内部做了什么？** 它接受源文档，应用已配置的签名选项，并将签名嵌入到新文件中。原始文件保持不变（这是最佳实践——永远不要直接修改源文件）。

**`SignResult` 对象** 会告诉你签名的执行情况。检查 `getSucceeded()` 以确认哪些签名成功，`getFailed()` 则用于捕获未成功的签名。

## 完整可运行示例

下面是一段完整的、可直接复制运行的示例类：

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

将此代码与 `resources/input/` 目录下的 PDF 文件一起运行，即可得到带有精美渐变效果的签名版 PDF。

## 常见使用场景

下面列出在实际应用中最适合使用渐变签名的情形。

### 1. 企业合同管理系统
**场景**：构建一个合同审批工作流，多个利益相关者在不同阶段签署文档。  
**应用**：使用不同的渐变颜色表示不同的审批层级——部门负责人使用蓝到白渐变，法务审查使用金到白渐变，执行层使用深蓝到浅蓝渐变。视觉层级帮助用户快速辨识签署人及其级别。

### 2. 自动化发票处理
**场景**：会计系统在向客户发送发票前自动签名。  
**应用**：使用与公司品牌色相匹配的细腻渐变，使发票更具专业感且更难伪造。保持渐变适度，以免影响可读性。

### 3. 证书生成
**场景**：为在线课程或培训项目生成结业证书。  
**应用**：使用鲜艳的庆祝渐变（如金到黄或蓝到紫）让证书显得正式且值得分享。视觉吸引力提升感知价值，促进社交传播。

### 4. 文档水印
**场景**：需要在文档上标记 “草稿”、 “机密” 或 “已批准”。  
**应用**：虽然不是签名本身，但可以复用渐变技术，将透明文字作为水印加入，既不遮挡内容，又能吸引注意。将透明度设为 0.7‑0.8 可获得柔和效果。

## 故障排查常见问题

以下是我在使用渐变签名时遇到并解决的问题，帮助你省去调试时间。

### Issue 1: “File is being used by another process”
**症状**：即使没有其他程序打开文件，应用仍抛出无法访问文件的异常。  
**原因**：忘记调用 `signature.dispose()` 或未正确关闭 `Signature` 对象。Java 会一直持有文件句柄，直至对象被垃圾回收。  
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
或手动：

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

### Issue 2: Signature appears but gradient doesn't show
**症状**：签名文字出现，但只有纯色，没有渐变。  
**可能原因**：  
1. **PDF 阅读器不支持渐变**——请使用 Adobe Acrobat、Foxit Reader 或现代浏览器进行测试。  
2. **透明度设置过高**——`setTransparency(1.0f)` 会导致渐变不可见。尝试 0.3‑0.7。  
3. **未正确应用画笔**——确保调用了 `background.setBrush(brush)` **并且** `options.setBackground(background)`。  

**调试技巧**：先使用高对比度颜色（例如 `Color.RED` 到 `Color.BLUE`）进行测试。如果仍看不到渐变，则说明配置有误，而非颜色问题。

### Issue 3: Signature overlaps important document content
**症状**：渐变签名效果很好，但覆盖了关键文字或表单字段。  
**解决方案**：根据文档内容动态调整位置。下面是一段我常用的模式：

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
**更佳做法**：先解析文档寻找空白区域，然后在代码中自动将签名放置到这些位置。

### Issue 4: Performance issues with large documents
**症状**：对页数众多或高分辨率图片的 PDF 进行签名时耗时较长。  
**原因**：GroupDocs 会处理整份文档，复杂的渐变会增加渲染开销。  
**解决方案**：  
1. **仅对特定页面签名**，而非整份文件。  
2. **使用更简洁的渐变**——两色线性渐变比径向或多停点渐变更快。  
3. **减小签名尺寸**——宽高越小渲染工作越少。  
4. **异步处理**——不要在主线程中阻塞签名操作。  

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

### Issue 5: Color doesn't match expectations
**症状**：实际呈现的渐变颜色与代码中指定的颜色不符。  
**原因**：  
1. **RGB 色彩空间差异**——Java 的 `Color` 使用 sRGB，而 PDF 可能在不同色彩空间下渲染。  
2. **透明度交互**——半透明渐变会与文档背景混合，导致感知颜色变化。  
3. **显示器校准**——不同设备的显示效果可能不同。  

**解决方案**：在多台设备和多款 PDF 阅读器上测试签名文档。若品牌一致性至关重要，请使用精确的 RGB 值并在各平台验证。将不透明度保持在 0.3‑0.5 左右，可最大程度降低颜色偏差。

## 生产环境最佳实践

以下是我在真实系统中使用渐变签名的经验总结。

### 1. 集中管理签名配置
不要在代码各处散落样式配置。创建一个帮助类：

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
以后即可统一调用：`SignatureStyles.getApprovalSignature("Jane Doe")`。

### 2. 在签名前验证文档有效性
始终检查源文档是否可用：

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

### 3. 记录签名操作
保持审计日志：

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

### 4. 优雅地处理异常
切勿让签名失败导致服务崩溃：

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

### 5. 使用真实业务文档进行测试
不要仅依赖示例 PDF。使用实际工作流中的文件进行验证：
- 包含已有字段的表单  
- 多页合同  
- 扫描图片（基于图像的 PDF）  
- 已经包含签名的文档  

不同类型的文档在渐变渲染上可能表现不同。

## 高级用户的专业技巧

准备好提升了吗？以下是一些进阶技巧。

### Tip 1: Create Custom Color Schemes
一次性定义品牌调色板并复用：

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

### Tip 2: Dynamic Transparency Based on Document Type
```java
public static float getOptimalTransparency(Signature signature) {
    if (hasComplexBackground(signature)) {
        return 0.6f; // More transparent for image‑heavy docs
    }
    return 0.4f;
}
```

### Tip 3: Batch Processing with Thread Pools
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

### Tip 4: Conditional Styling Based on Signature Type
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

## 常见问题解答

**Q: 可以在基于 Web 的 Java 服务中使用吗？**  
A: 可以。GroupDocs.Signature 是纯 Java 实现，能够在任何基于 Java 的后端运行，包括 Spring Boot 或 Jakarta EE 服务。

**Q: 渐变会影响已签 PDF 的文件大小吗？**  
A: 影响极小。渐变作为视觉外观流存储，通常只会增加几 KB。

**Q: 如何签署受密码保护的 PDF？**  
A: 在创建 `Signature` 对象时传入密码，例如 `new Signature("file.pdf", "password")`。

**Q: 能否将渐变应用于基于图像的签名而不是文本？**  
A: 完全可以。使用 `ImageSignOptions` 并像文本示例一样为其 `Background` 设置 `LinearGradientBrush`。

**Q: 如果需要径向渐变而不是线性渐变怎么办？**  
A: 目前 GroupDocs 仅支持 `LinearGradientBrush`。若需径向效果，可预先生成径向渐变图片并将其作为背景图像使用。

---

**最后更新：** 2026-03-14  
**测试版本：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs