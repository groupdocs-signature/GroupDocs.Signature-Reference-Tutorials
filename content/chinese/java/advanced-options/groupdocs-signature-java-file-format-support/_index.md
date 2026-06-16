---
categories:
- Java Document Processing
date: '2026-05-11'
description: 了解如何使用 GroupDocs.Signature 检查 Java 文件扩展名并验证文档格式。完整指南，包含代码示例、故障排除技巧以及文档类型检查的最佳实践。
keywords:
- check file extension java
- validate document type java
- java upload file validation
- how to detect file format java
lastmod: '2025-01-02'
linktitle: Java 文件格式检测指南
schemas:
- author: GroupDocs
  dateModified: '2026-05-11'
  description: Learn how to check file extension java and validate document formats
    using GroupDocs.Signature. Complete guide with code examples, troubleshooting
    tips, and best practices for document type checking.
  headline: Java File Format Detection - Validate and Check Document Types
  type: TechArticle
- questions:
  - answer: Change the `<version>` tag in your `pom.xml` to the desired version, then
      run `mvn clean install`. Always review the [release notes](https://releases.groupdocs.com/signature/java/)
      for breaking changes.
    question: How do I update my GroupDocs.Signature library version in Maven?
  - answer: Yes. The library performs content‑based validation, so a file renamed
      from `.exe` to `.pdf` will be rejected as not a valid PDF during processing.
      `getSupportedFileTypes()` only lists formats the library can handle; you still
      need to attempt opening the file to verify its true type.
    question: Can GroupDocs.Signature detect file formats even if the extension is
      wrong?
  - answer: The free trial gives immediate access but includes evaluation watermarks
      and some feature limits. A temporary license provides full feature access for
      30 days without watermarks, ideal for thorough testing in a production‑like
      environment.
    question: What's the difference between a free trial and temporary license?
  - answer: 'Return a concise error like “Unsupported format. Supported extensions
      are: .pdf, .docx, .xlsx, .png, .jpg.” Log the incident for security monitoring
      and consider notifying the user with a UI tooltip that lists allowed types.'
    question: How should I handle unsupported file formats in my application?
  - answer: Yes, but you must supply the password when creating the `Signature` instance.
      Format detection itself does not require the password, but any subsequent processing
      (e.g., adding a signature) will.
    question: Does GroupDocs.Signature work with encrypted or password‑protected files?
  type: FAQPage
tags:
- file-validation
- java-libraries
- document-management
- format-detection
title: Java 文件格式检测 - 验证并检查文档类型
type: docs
url: /zh/java/advanced-options/groupdocs-signature-java-file-format-support/
weight: 1
---

# 检查文件扩展名 java – Java 文件格式检测：验证和检查文档类型

在处理文档之前，最常见的任务之一是 **检查文件扩展名 java**。  

是否曾经上传文件后因格式不符合预期而导致应用崩溃？你并不孤单。在 Java 中检测和验证文件格式对于构建稳健的文档处理应用至关重要——但这比仅检查文件扩展名要更棘手（扩展名容易被伪造或不正确）。

在本指南中，你将学习如何使用 GroupDocs.Signature 在 Java 中可靠地检测文件格式，这是一款超越简单扩展名检查的强大库。无论你是构建文档管理系统、验证用户上传，还是与云存储服务集成，你都将发现实用技术，以自信地处理多种文档类型。

**你将学到的内容：**
- 如何在 Java 中以编程方式检索受支持的文件格式
- 何时使用基于库的检测 vs. 内置的 Java 方法
- 验证文件类型时的常见陷阱（以及如何避免）
- 真实场景的集成示例和性能优化技巧
- 格式检测问题的故障排除策略

通过本指南，你将拥有一个可直接放入 Java 应用的实现示例。让我们先确保你已经准备好所需的一切。

## 快速答案
- **检查文件扩展名 java 的最快方法是什么？** 使用 `Signature.getSupportedFileTypes()` 获取完整列表，并将文件的扩展名与之比较。
- **使用 GroupDocs.Signature 是否需要许可证？** 免费试用可用于开发；永久许可证可移除所有评估限制。
- **可以在不读取整个文件的情况下验证上传吗？** 可以——GroupDocs.Signature 检查文件头部，远比加载整个文档更省资源。
- **GroupDocs.Signature 支持多少种格式？** 超过 50 种输入和输出格式，包括 PDF、DOCX、XLSX、PPTX、JPG、PNG 等。
- **是否需要缓存格式列表？** 缓存可消除重复的反射开销，提高高并发服务的吞吐量。

## 前置条件

在深入文件格式检测之前，请确保已准备好以下必备条件：

### 必需的库和版本
- **GroupDocs.Signature Library**：版本 23.12 或更高（我们将使用最新的稳定版）
- **Java Development Kit**：JDK 1.8 或更高（推荐使用 JDK 11+ 以获得更好性能）
- **构建工具**：Maven 3.x 或 Gradle 6.x 用于依赖管理

### 环境搭建要求
你应当熟悉：
- 基本的 Java 编程概念（类、循环、导入）
- 使用 Maven 或 Gradle 管理依赖
- 在 IDE 或命令行中运行 Java 应用

**小技巧：** 如果要处理大文档或计划并发处理文件，请为 JVM 分配足够的堆内存（后面会介绍优化方法）。

环境准备就绪后，接下来我们在项目中配置 GroupDocs.Signature。

## 为 Java 设置 GroupDocs.Signature

将 GroupDocs.Signature 引入项目非常简单——选择你喜欢的构建工具并按以下步骤操作。

### 使用 Maven

在 `pom.xml` 文件中添加以下依赖：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

添加依赖后，运行 `mvn clean install` 下载库。

### 使用 Gradle

在 `build.gradle` 文件中加入此行：

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

然后同步 Gradle 项目或运行 `gradle build`。

### 直接下载替代方案

不使用构建工具？你可以直接从 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) 下载 JAR 并手动加入类路径。（不过说实话，使用 Maven 或 Gradle 能省去很多后顾之忧。）

### 许可证获取步骤

GroupDocs.Signature 提供灵活的授权选项：

- **免费试用**：适合测试——立即开始，无需信用卡，链接见 [no credit card required](https://releases.groupdocs.com/signature/java/)
- **临时许可证**：需要更长时间评估？可申请 30 天的临时许可证，享受无限制访问
- **购买**：准备投入生产后，可从 [GroupDocs Purchase Page](https://purchase.groupdocs.com/buy) 购买永久许可证

**专业提示：** 先使用免费试用探索全部功能。临时许可证可去除水印和限制，适合延长评估时间。

### 基本初始化与设置

`Signature` 是 GroupDocs.Signature 所有操作的核心入口。它封装了文档加载、格式处理和签名处理。

下面展示如何在 Java 应用中初始化 GroupDocs.Signature：

```java
import com.groupdocs.signature.Signature;

// Create an instance of Signature class
Signature signature = new Signature("sample.pdf");
```

这会为指定文档创建一个签名对象。实际处理文档时会使用此模式，但在获取受支持的格式时并不需要特定文件（后面会演示）。

完成上述设置后，我们开始实现检测并检索受支持文件格式的核心功能。

## 实现指南

下面进入实战。我们将构建一个简单工具，获取所有受支持的文件格式——相当于为你的文档处理管道创建一个“兼容性检查器”。

### 为什么这很重要

在实现文档处理功能之前，你需要了解库支持哪些文件类型。此实现动态提供这些信息，意味着：
- 不必硬编码可能过时的扩展名列表
- 可轻松根据受支持的格式验证用户上传
- 为 UI 中的文件类型过滤器提供快速参考

### 步骤实现

**1. 导入必要的类**

`FileType` 是格式检测的入口，它包含了所有受支持文档类型的元数据。

```java
import com.groupdocs.signature.domain.documentpreview.FileType;
import java.util.List;
```

`FileType` 类是 GroupDocs.Signature 为每种受支持格式提供的描述符，公开了扩展名、MIME 类型和描述等属性。

**2. 创建检索类**

完整实现如下：

```java
public class GetSupportedFileFormats {
    public static void run() {
        // Retrieve a list of supported file types from the FileType utility.
        List<FileType> supportedFileTypes = FileType.getSupportedFileTypes();

        // Iterate over each FileType object and print its extension to the console.
        for (FileType fileType : supportedFileTypes) {
            System.out.print("\n" + fileType.getExtension());
        }
    }
}
```

**实现要点：**
- `getSupportedFileTypes()`：此静态方法查询库内部注册表，返回 `FileType` 对象列表
- 循环遍历每种格式并输出其扩展名（如 `.pdf`、`.docx`、`.xlsx`）
- 每个 `FileType` 对象还包含其他元数据，可在下文中进一步探索

### 超越基本扩展名

`FileType` 对象提供的不止扩展名。下面展示还能获取哪些信息：

```java
for (FileType fileType : supportedFileTypes) {
    System.out.println("Extension: " + fileType.getExtension());
    System.out.println("Format: " + fileType.getFileFormat());
    // Additional properties available depending on version
}
```

当需要显示友好的格式名称或按类型（文档、电子表格、图像）分组时，这些信息非常有用。

## 何时使用此方法

并非所有场景都需要库级别的解决方案。以下情况适合使用 GroupDocs.Signature 的格式检测：

### 理想使用场景

**1. 构建文档上传验证器**  
当用户向你的应用上传文件时，需要在服务器端验证格式（永远不要仅依赖客户端验证）。此方法可在处理前对照完整的受支持格式列表进行检查。

**2. 动态文件类型过滤器**  
构建文件选择器或上传界面时，可动态生成允许的格式列表，而不是维护一个可能不同步的静态数组。

**3. 多格式文档处理流水线**  
如果你的系统需要处理来自电子邮件、云存储、用户上传等多来源的文档，可靠的格式检测可将文件路由到相应的处理器。

**4. 与云存储服务集成**  
在同步 AWS S3、Google Drive 或 Azure Blob Storage 时，先验证文档兼容性再下载和处理，可节省带宽和处理时间。

### 内置 Java 方法可能已足够的情况

对于更简单的场景，Java 自带的方法或许已经满足需求：
- **仅检查扩展名**：`file.getName().endsWith(".pdf")`
- **MIME 类型检测**：`Files.probeContentType(path)`
- **基本验证**：当你控制上传源并信任文件扩展名时

**重要提醒：** 内置方法容易被欺骗。将 `malicious.exe` 重命名为 `document.pdf` 能通过扩展名检查，却会在真正的验证阶段被拦截。GroupDocs.Signature 通过更深层次的检查避免此类风险。

## 常见问题与故障排除

下面列出你可能遇到的问题及快速解决方案。

### 问题 1：返回的列表为空或为 null

**症状：** `getSupportedFileTypes()` 返回空列表或 null。

**原因与解决方案：**
- **库未正确初始化**：确认 Maven/Gradle 依赖已正确添加并同步
- **版本兼容性**：确保使用 23.12 或更高版本（早期版本 API 可能不同）
- **类路径问题**：若使用手动 JAR，确认已正确加入类路径

**快速修复：**
```java
List<FileType> formats = FileType.getSupportedFileTypes();
if (formats == null || formats.isEmpty()) {
    System.err.println("Error: No file types loaded. Check library initialization.");
    return;
}
```

### 问题 2：缺少预期的格式

**症状：** 你期望支持的某种格式未出现在列表中。

**可能原因：**
- 该格式需要额外插件（某些 CAD 或医学影像格式需单独模块）
- 格式在更高版本中才加入——请查看发行说明
- 该格式仅支持读取而不支持签名操作（GroupDocs.Signature 主要用于添加签名，非所有操作都兼容所有格式）

**调试思路：**
```java
// Check for specific format
boolean hasPDF = supportedFileTypes.stream()
    .anyMatch(ft -> ft.getExtension().equalsIgnoreCase(".pdf"));
System.out.println("PDF supported: " + hasPDF);
```

### 问题 3：频繁调用导致性能下降

**症状：** 多次调用 `getSupportedFileTypes()` 会拖慢应用。

**解决方案：** 将结果缓存！运行时列表不会改变：

```java
public class FormatCache {
    private static List<FileType> cachedFormats = null;
    
    public static List<FileType> getSupportedFormats() {
        if (cachedFormats == null) {
            cachedFormats = FileType.getSupportedFileTypes();
        }
        return cachedFormats;
    }
}
```

此模式确保在应用生命周期内仅查询一次库。

### 问题 4：许可证相关限制

**症状：** 出现评估警告或格式支持受限。

**解决方案：**
- 在调用任何 GroupDocs 方法前先加载许可证
- 确认许可证文件路径正确
- 若使用限时许可证，检查到期日期

```java
try {
    License license = new License();
    license.setLicense("path/to/GroupDocs.Signature.lic");
} catch (Exception e) {
    System.err.println("License error: " + e.getMessage());
}
```

## 文件格式检测最佳实践

遵循以下指南，构建稳健且易维护的检测逻辑。

### 1. 早期验证，快速失败

在处理管道的最前端检查文件格式：

```java
public boolean validateFileFormat(String filePath) {
    String extension = getFileExtension(filePath);
    List<FileType> supported = FormatCache.getSupportedFormats();
    
    boolean isSupported = supported.stream()
        .anyMatch(ft -> ft.getExtension().equalsIgnoreCase(extension));
    
    if (!isSupported) {
        throw new UnsupportedFormatException(
            "File format " + extension + " is not supported"
        );
    }
    return true;
}
```

这样可避免在不受支持的文件上浪费处理时间。

### 2. 提供明确的用户反馈

拒绝文件时，告知用户当前 **支持的** 格式：

```java
public String getSupportedFormatsMessage() {
    List<FileType> formats = FormatCache.getSupportedFormats();
    String extensions = formats.stream()
        .map(FileType::getExtension)
        .collect(Collectors.joining(", "));
    
    return "Supported formats: " + extensions;
}
```

### 3. 不要仅信任扩展名

将 `.exe` 重命名为 `.pdf` 会拥有 `.pdf` 扩展名，却不是有效的 PDF。GroupDocs.Signature 会验证实际内容，但仍建议结合两种方式：

```java
// First check extension (fast)
if (!hasValidExtension(file)) {
    return false;
}

// Then validate with library (more thorough)
try (Signature signature = new Signature(file)) {
    // If initialization succeeds, format is valid
    return true;
} catch (Exception e) {
    return false;
}
```

### 4. 优雅地处理异常

文件验证可能因多种原因失败：

```java
public ValidationResult validateDocument(String path) {
    try {
        // Your validation logic
        return ValidationResult.success();
    } catch (UnsupportedFormatException e) {
        return ValidationResult.failure("Unsupported format: " + e.getMessage());
    } catch (IOException e) {
        return ValidationResult.failure("File access error: " + e.getMessage());
    } catch (Exception e) {
        return ValidationResult.failure("Unexpected error: " + e.getMessage());
    }
}
```

### 5. 关注格式支持的变更

升级 GroupDocs.Signature 时，请检查发行说明，关注：
- 新增支持的格式
- 已废弃的格式
- 检测行为的变化

建议编写单元测试，验证关键格式仍受支持：

```java
@Test
public void testEssentialFormatsSupported() {
    List<String> required = Arrays.asList(".pdf", ".docx", ".xlsx");
    List<FileType> supported = FileType.getSupportedFileTypes();
    
    for (String format : required) {
        assertTrue(
            supported.stream().anyMatch(ft -> ft.getExtension().equals(format)),
            format + " should be supported"
        );
    }
}
```

## 性能考量

在处理成千上万文档或并发上传时，文件格式检测的优化尤为重要。

### 内存管理

**缓存策略：** 如前所述，缓存受支持的格式列表：

```java
// Good: Load once, reuse many times
private static final List<FileType> SUPPORTED_FORMATS = 
    FileType.getSupportedFileTypes();

// Bad: Loads list every time method is called
public boolean isSupported(String ext) {
    return FileType.getSupportedFileTypes().stream()
        .anyMatch(ft -> ft.getExtension().equals(ext));
}
```

**原因：** 加载格式列表涉及反射和库内部初始化。只做一次即可节省 CPU 和内存分配。

### 资源使用指南

**高并发场景：**
- 使用线程安全的缓存（上述示例是不可变的，天然线程安全）
- 若应用并非始终需要格式检测，可采用懒加载
- 处理文档后及时关闭 `Signature` 对象，释放资源

```java
try (Signature signature = new Signature(filePath)) {
    // Process document
} // Automatically closed, resources freed
```

### 批量处理优化

若一次验证多个文件，可考虑并行化：

```java
List<String> files = Arrays.asList("doc1.pdf", "doc2.docx", "doc3.xlsx");

// Process in parallel
files.parallelStream()
    .forEach(file -> {
        if (validateFileFormat(file)) {
            processDocument(file);
        }
    });
```

**注意：** 不要过度并行。若受 I/O 限制，过多线程并不会提升性能。请自行测试找到最佳线程数。

### JVM 调优建议

针对文档密集型应用：
- 增大堆内存，例如 `-Xmx2g`（根据实际需求调整）
- 监控垃圾回收：使用 `-XX:+PrintGCDetails` 观察问题
- 考虑使用 G1GC 以获得更短的停顿时间：`-XX:+UseG1GC`

## 实际应用与集成案例

下面展示文件格式检测在真实项目中的关键作用。

### 1. 文档管理系统

**场景：** 用户上传文档，需要进行索引、处理并存储。

**实现模式：**
```java
public class DocumentUploadHandler {
    public void handleUpload(MultipartFile file) {
        // Validate format first
        if (!isFormatSupported(file.getOriginalFilename())) {
            throw new InvalidFormatException(
                "Please upload: " + getSupportedFormatsString()
            );
        }
        
        // Process valid document
        processAndStore(file);
    }
    
    private boolean isFormatSupported(String filename) {
        String ext = getExtension(filename);
        return FormatCache.getSupportedFormats().stream()
            .anyMatch(ft -> ft.getExtension().equalsIgnoreCase(ext));
    }
}
```

### 2. 云存储集成

**场景：** 从 AWS S3 或 Google Drive 同步文档，仅处理受支持的格式。

**价值：** 避免下载和处理不兼容文件，节省带宽和计算资源。

```java
public void syncFromS3(String bucketName) {
    S3Client s3 = S3Client.create();
    ListObjectsV2Request listReq = ListObjectsV2Request.builder()
        .bucket(bucketName)
        .build();
    
    ListObjectsV2Response listing = s3.listObjectsV2(listReq);
    
    for (S3Object object : listing.contents()) {
        if (isFormatSupported(object.key())) {
            // Download and process only supported formats
            downloadAndProcess(bucketName, object.key());
        } else {
            logger.info("Skipping unsupported format: " + object.key());
        }
    }
}
```

### 3. 企业工作流自动化

**场景：** 根据文档类型将其路由至不同处理流水线。

**示例：** PDF 进入签名工作流，电子表格进入数据抽取，图像进入 OCR 处理。

```java
public void routeDocument(String filePath) {
    try (Signature signature = new Signature(filePath)) {
        FileType type = signature.getDocumentInfo().getFileType();
        
        switch (type.getExtension()) {
            case ".pdf":
            case ".docx":
                sendToSignatureWorkflow(filePath);
                break;
            case ".xlsx":
            case ".csv":
                sendToDataExtractionWorkflow(filePath);
                break;
            case ".jpg":
            case ".png":
                sendToOCRWorkflow(filePath);
                break;
            default:
                logger.warn("No workflow defined for: " + type.getExtension());
        }
    }
}
```

### 4. 构建文件类型选择器

**场景：** 创建前端 UI 组件，动态展示支持的格式。

**前端集成示例：**
```java
@RestController
public class FormatController {
    @GetMapping("/api/supported-formats")
    public ResponseEntity<List<String>> getSupportedFormats() {
        List<String> extensions = FileType.getSupportedFileTypes().stream()
            .map(FileType::getExtension)
            .sorted()
            .collect(Collectors.toList());
        
        return ResponseEntity.ok(extensions);
    }
}
```

随后前端可使用该数据配置文件上传组件：
```javascript
// Frontend code (for context, not part of Java implementation)
fetch('/api/supported-formats')
    .then(res => res.json())
    .then(formats => {
        fileInput.accept = formats.join(',');
    });
```

## 如何检查文件扩展名 java？

加载文件名，提取其后缀，并与 `Signature.getSupportedFileTypes()` 返回的缓存列表进行比较。这种两步走的方法确保你使用的是最新的目录，而不是硬编码的数组。同时，GroupDocs.Signature 在进一步处理前会验证文件头部，防止伪造的扩展名。

## 什么是 GroupDocs.Signature？

GroupDocs.Signature 是一款 Java 库，帮助开发者在超过 50 种文档格式上添加、验证和管理数字签名。它提供统一的 API，支持 PDF、Office、图片等多种类型，并能处理加密文件、受密码保护的文档以及多页签名等复杂场景。

## 为什么使用基于库的检测而不是 Java 内置方法？

基于库的检测会检查文件的实际头部信息和内部结构，确保内容真正匹配声明的格式。Java 的 `Files.probeContentType` 或简单的字符串后缀检查容易被重命名的恶意文件欺骗。GroupDocs.Signature 通过深度内容分析，在任何进一步处理之前就拦截不合法文件。

## 何时应缓存受支持的文件格式？

在应用启动时或首次需要时缓存格式列表，并在整个 JVM 生命周期内复用该不可变集合。对于高吞吐量的 Web 服务来说，缓存尤为重要，因为每次请求若重新触发反射式库初始化，会增加数毫秒的延迟。

## 如何在 Java 中处理不受支持的文件格式？

在早期检测到不受支持的格式后，记录审计日志并向用户返回明确的错误信息，列出允许的扩展名。此做法提升用户体验，同时降低后端不必要的处理负担。

## 常见问答

**Q: 如何在 Maven 中更新 GroupDocs.Signature 库版本？**  
A: 在 `pom.xml` 中修改 `<version>` 标签为目标版本，然后运行 `mvn clean install`。更新前请务必阅读 [release notes](https://releases.groupdocs.com/signature/java/) 了解可能的破坏性更改。

**Q: 即使扩展名错误，GroupDocs.Signature 能否检测文件格式？**  
A: 能。库执行基于内容的验证，因此将 `.exe` 重命名为 `.pdf` 的文件会在处理时被识别为无效 PDF。`getSupportedFileTypes()` 仅列出库能够处理的格式，真正的类型仍需尝试打开文件进行验证。

**Q: 免费试用和临时许可证有什么区别？**  
A: 免费试用可立即使用，但会有水印和部分功能限制。临时许可证提供完整功能的 30 天无水印使用，适合在接近生产环境的场景中进行彻底测试。

**Q: 应该如何在应用中处理不受支持的文件格式？**  
A: 返回类似 “不支持的格式。支持的扩展名包括：.pdf, .docx, .xlsx, .png, .jpg。” 的简洁错误信息。记录该事件以便安全审计，并考虑在 UI 中提供工具提示列出允许的类型。

**Q: GroupDocs.Signature 能否处理加密或受密码保护的文件？**  
A: 能，但在创建 `Signature` 实例时必须提供密码。格式检测本身不需要密码，后续的签名等操作则需要。

**Q: 是否有 GroupDocs.Signature 的社区或支持论坛？**  
A: 当然！访问 [GroupDocs Forum](https://forum.groupdocs.com/c/signature/) 可参与社区讨论、获取代码示例并直接向 GroupDocs 团队提问。

## 资源

**文档：**
- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/) – 完整指南与教程
- [API Reference](https://reference.groupdocs.com/signature/java/) – 包含所有类和方法的详细说明

**下载与授权：**
- [Download Library](https://releases.groupdocs.com/signature/java/) – 最新发布及历史版本
- [Purchase Licenses](https://purchase.groupdocs.com/buy) – 价格与授权选项
- [Free Trial](https://releases.groupdocs.com/signature/java/) – 立即开始测试

**支持与社区：**
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/) – 社区讨论与技术支持

---

**最后更新：** 2026-05-11  
**测试环境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs

```xml
<version>24.1</version>  <!-- Update to newer version -->
```

```java
try {
    validateAndProcess(file);
} catch (UnsupportedFormatException e) {
    return ResponseEntity
        .badRequest()
        .body("Unsupported format. Please upload: " + getSupportedFormatsString());
}
```

```java
LoadOptions loadOptions = new LoadOptions();
loadOptions.setPassword("your-password");
Signature signature = new Signature("protected.pdf", loadOptions);
```

## 相关教程

- [Add QR Code to PDF Java - Complete Guide with GroupDocs.Signature](/signature/java/qr-code-signatures/qr-code-signatures-java-groupdocs/)
- [Java Text Signature Search - A Complete Guide to Document Verification with GroupDocs.Signature](/signature/java/search-verification/java-text-signature-search-groupdocs-signature/)
- [Digital Signature in Java - Complete Guide to Certificate Loading and Document Signing](/signature/java/digital-signatures/digital-signature-loading-signing-groupdocs-java/)