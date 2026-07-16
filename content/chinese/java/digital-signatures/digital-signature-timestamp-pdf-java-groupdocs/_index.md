---
categories:
- Java Development
date: '2026-06-11'
description: 了解如何使用 GroupDocs.Signature 通过 Java 对 PDF 进行签名，添加 digital signature 和
  timestamp。提供代码示例和最佳实践的分步指南。
keywords:
- how to sign pdf
- add digital signature pdf
- timestamp pdf signature
- java pdf signature library
- groupdocs signature java
lastmod: '2026-06-11'
linktitle: 在 Java 中为 PDF 添加 Digital Signature
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  headline: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  type: TechArticle
- description: Learn how to sign PDF with Java using GroupDocs.Signature, add digital
    signature and timestamp. Step-by-step guide with code examples and best practices.
  name: 'How to Sign PDF with Java: Add Digital Signature and Timestamp'
  steps:
  - name: Import Required Classes
    text: The following imports give you access to signature configuration, positioning,
      and timestamp functionality.
  - name: Define Your File Paths
    text: Set up paths for your input PDF, certificate, and where you want the signed
      PDF saved. Keep the certificate file secure; it contains your private key.
  - name: Initialize the Signature Object
    text: Create a `Signature` instance pointing to the PDF you want to sign. This
      loads the PDF into memory and prepares it for signing.
  - name: Configure Signature Properties and Timestamp
    text: The `DigitalSignature` class represents the cryptographic seal that will
      be embedded in the PDF. You can also attach a timestamp from a trusted authority.
      * **ContactInfo** – e.g., `john.doe@company.com` * **Location** – e.g., `New
      York Office` * **Reason** – e.g., `Contract Approval` We use FreeTSA
  - name: Configure Digital Sign Options
    text: The `SignOptions` class ties together the certificate, signature properties,
      and visual placement. Alignment enums control where the signature appears.
  - name: Sign and Save the Document
    text: Execute the signing process and write the signed PDF to disk. The returned
      `SignResult` object tells you whether the operation succeeded and lists any
      warnings.
  type: HowTo
- questions:
  - answer: A digital signature uses cryptographic algorithms to verify identity and
      detect tampering, while an electronic signature can be as simple as a typed
      name.
    question: What's the difference between a digital signature and an electronic
      signature?
  - answer: Only for the timestamp service; the cryptographic signing itself runs
      locally.
    question: Do I need internet connectivity to sign PDFs?
  - answer: Any modification breaks the signature, and PDF viewers will display a
      warning indicating the document has been altered.
    question: Can signed PDFs be edited later?
  - answer: Most PDF readers verify automatically; programmatically, use GroupDocs.Signature's
      verification API to check status, signer details, and timestamp validity.
    question: How do I verify a signed PDF?
  - answer: The embedded timestamp proves the signature was created while the certificate
      was still valid, preserving legal standing.
    question: What happens if my certificate expires after I've signed documents?
  type: FAQPage
tags:
- pdf-signing
- digital-signatures
- java-security
- groupdocs
title: 如何使用 Java 对 PDF 进行签名：添加 Digital Signature 和 Timestamp
type: docs
url: /zh/java/digital-signatures/digital-signature-timestamp-pdf-java-groupdocs/
weight: 1
---

# 如何使用 Java 为 PDF 添加签名和时间戳

是否曾经发送过重要文件，却担心以后会被篡改？你并不孤单。无论是构建企业文档管理系统、创建合同签署平台，还是仅仅需要以编程方式保护 PDF 文件，**如何为 PDF 添加签名** 并附加可信时间戳就是答案。添加数字签名不仅能证明是谁签署了文件，还会创建一个*精确*记录签署时间的不可变记录。

## 快速回答
- **哪个库简化了 Java 中的 PDF 签名？** GroupDocs.Signature for Java。  
- **是否需要网络连接？** 仅在获取时间戳时需要；签名本身离线完成。  
- **可以使用自签名证书进行测试吗？** 可以，使用 `keytool` 生成。  
- **是否有大小限制？** 该库可在不将整个文件加载到内存的情况下签署高达 500 MB 的 PDF。  
- **GroupDocs 支持多少种格式？** 超过 50 种输入和输出格式，包括 DOCX、XLSX、PPTX、HTML 和图像。

## 为什么数字签名重要（以及为何需要时间戳）

加载 PDF，应用加密封印，并嵌入可信时间戳——这两步过程保证了身份验证、完整性和不可否认性。时间戳证明签名在特定时刻已存在，即使签名证书随后过期或被吊销，也能证明签名的有效性。

## 如何使用 Java 为 PDF 添加签名？

使用 `new Signature("input.pdf")` 加载 PDF，配置 `DigitalSignature` 对象，附加来自可信机构的时间戳，然后调用 `sign()`——整个操作只需几行代码。GroupDocs.Signature 自动处理证书解析、哈希计算和时间戳获取，让你专注业务逻辑而非密码学细节。

## 为 Java 设置 GroupDocs.Signature

### 集成方式

选择你使用的构建工具：

**针对 Maven 用户：**  
将以下依赖添加到你的 `pom.xml` 中：
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**针对 Gradle 用户：**  
将以下内容添加到你的 `build.gradle` 中：
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**直接下载（如果你更喜欢）：**  
前往 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) 下载 JAR 包。手动将其加入项目的 classpath。详见 [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/) 获取完整 API 参考。最新构建请查看 [Latest Version & Releases](https://releases.groupdocs.com/signature/java/)。

小贴士：如果可能，使用 Maven 或 Gradle——这会让依赖管理和后期更新更加轻松。

### 获取许可证

GroupDocs 提供多种授权方式，取决于项目阶段：

1. **免费试用** – 适合评估。[下载试用版](https://releases.groupdocs.com/signature/java/) 并体验全部功能。  
2. **临时许可证** – 需要完整功能且不想出现试用水印？获取 30 天临时许可证。  
3. **商业许可证** – 生产环境使用，请 [购买许可证](https://purchase.groupdocs.com/buy)。价格依据部署类型而异。

需要帮助？访问 [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)。

### 基本初始化

`Signature` 类是 GroupDocs.Signature 的顶层对象，代表内存中的单个 PDF 文件。实例化后，所有读写操作均通过该对象进行。

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
final Signature signature = new Signature(filePath);
```

简单吧？只需指向你的 PDF 文件，即可开始使用。`Signature` 对象是所有签名操作的主要入口。

## 如何在 Java 中为 PDF 添加数字签名：逐步指南

加载 PDF，配置签名细节，附加时间戳，保存已签名文档——整个流程清晰线性。

### 步骤 1：导入所需类

以下导入提供签名配置、定位和时间戳功能。

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.PdfDigitalSignature;
import com.groupdocs.signature.domain.structs.TimeStamp;
import com.groupdocs.signature.options.sign.DigitalSignOptions;
```

### 步骤 2：定义文件路径

设置输入 PDF、证书以及签名后 PDF 的保存路径。请妥善保管证书文件，它包含私钥。

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/digitallySignedTimeStamp.pdf";
```

### 步骤 3：初始化 Signature 对象

创建指向待签名 PDF 的 `Signature` 实例。此操作会将 PDF 加载到内存并准备签名。

```java
final Signature signature = new Signature(filePath);
```

### 步骤 4：配置签名属性和时间戳

`DigitalSignature` 类代表将嵌入 PDF 的加密封印。你还可以附加来自可信机构的时间戳。

```java
PdfDigitalSignature pdfDigitalSignature = new PdfDigitalSignature();
pdfDigitalSignature.setContactInfo("Contact Information");
pdfDigitalSignature.setLocation("Location Info");
pdfDigitalSignature.setReason("Signing Reason");

// Configure the TimeStamp with URL, User Id, and Password
TimeStamp timeStamp = new TimeStamp("https://freetsa.org/tsr", "User Id", "Password");
pdfDigitalSignature.setTimeStamp(timeStamp);
```

* **ContactInfo** – 例如，`john.doe@company.com`  
* **Location** – 例如，`New York Office`  
* **Reason** – 例如，`Contract Approval`  

演示中使用 FreeTSA（免费时间戳机构）。生产环境请选用商业 TSA，以确保可用性和法律效力。

### 步骤 5：配置数字签名选项

`SignOptions` 类将证书、签名属性和可视化位置组合在一起。对齐枚举控制签名出现的位置。

```java
DigitalSignOptions options = new DigitalSignOptions(certificatePath);
options.setPassword("YourCertificatePassword"); // Certificate password
options.setSignature(pdfDigitalSignature); // Attach the PdfDigitalSignature object

// Specify signature alignment (where it appears on the page)
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
```

### 步骤 6：签署并保存文档

执行签名过程并将已签名的 PDF 写入磁盘。返回的 `SignResult` 对象指示操作是否成功，并列出任何警告。

```java
try {
    SignResult signResult = signature.sign(outputFilePath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Output: " + outputFilePath);
} catch (Exception e) {
    throw new RuntimeException("Error during signing process: " + e.getMessage());
}
```

## 常见陷阱及避免方法

### 1. 证书问题
**问题：** “Invalid certificate” 错误。  
**解决方案：** 使用 `keytool -list -v -keystore your.pfx` 验证密码。

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### 2. 时间戳服务超时
**问题：** 联系 TSA 时网络超时。  
**解决方案：** 测试连通性 (`curl -I https://freetsa.org/tsr`)，添加重试逻辑，或配置备用 TSA。

```java
new File(outputFilePath).getParentFile().mkdirs();
```

### 3. 文件权限问题
**问题：** 保存时出现 “Access denied”。  
**解决方案：** 确认输出目录存在且应用拥有写权限。

```bash
keytool -genkeypair -alias mykey -keyalg RSA -keysize 2048 -storetype PKCS12 -keystore certificate.pfx -validity 365
```

### 4. 大型 PDF 的内存问题
**问题：** 大文件导致 `OutOfMemoryError`。  
**解决方案：** 增加 JVM 堆大小 (`-Xmx4g`) 或分批处理文件。

### 5. 错误的签名位置
**问题：** 签名覆盖已有内容。  
**解决方案：** 先测试对齐设置；若需像素级定位，可使用基于坐标的选项。

## 证书管理技巧

### 获取开发用证书

使用 Java 的 `keytool` 生成自签名证书用于测试。

```java
   String certPassword = System.getenv("CERT_PASSWORD");
   ```

### 证书最佳实践

1. **绝不在代码中硬编码密码** – 使用环境变量。  
2. **在证书过期前进行轮换**。  
3. **将私钥存储在安全硬件（HSM）中**，用于高安全性应用。  
4. **在受保护的位置备份证书**。  
5. **在签名前验证证书**，以捕获已过期或被吊销的证书。

## 安全最佳实践

### 1. 保护私钥
将证书存放在项目目录之外，使用环境特定的配置，并在企业部署时考虑使用 HSM。

### 2. 验证输入 PDF
在签名前检查文件是否损坏、是否已有签名、大小限制以及内容合规性。

### 3. 实施审计日志
记录每一次签名操作的时间戳、用户、文档名称和状态。

```java
try {
    SignResult result = signature.sign(outputFilePath, options);
    logger.info("Document signed: " + filePath + " by " + signerEmail);
} catch (Exception e) {
    logger.error("Signing failed: " + filePath + " - " + e.getMessage());
    // Handle appropriately
}
```

### 4. 使用可信的时间戳机构
不要依赖本地系统时间；始终向符合 RFC 3161 的 TSA 请求时间戳。

### 5. 实施错误处理
捕获异常时不泄露敏感细节。

```java
try {
    signature.sign(outputFilePath, options);
} catch (Exception e) {
    // Log detailed error internally
    logger.error("Signing error: " + e.getMessage(), e);
    // Return generic error to client
    throw new ApplicationException("Unable to sign document. Please try again.");
}
```

## 实际使用案例和应用场景

### 1. 合同管理系统
员工电子签署 NDA 和协议；时间戳精准记录每份合同的接受时间。

### 2. 金融文档处理
批量签署发票和采购单，为监管机构提供不可篡改的审计轨迹。

### 3. 教育凭证验证
高校发行防篡改的成绩单，可通过二维码链接即时验证。

### 4. 软件许可证管理
生成带数字签名和时间戳的许可证证书，防止伪造。

### 5. 合规监管（如 FDA 21 CFR Part 11 等）
医疗器械公司签署 SOP 和验证报告；时间戳满足不可否认性要求。

## 性能考虑与优化

### 内存管理
对大 PDF 进行批处理，及时关闭 `Signature` 对象，并在必要时增大堆内存。

### 时间戳网络优化
复用 HTTP 连接，实现指数退避重试，并对连续签名缓存时间戳以提升速度。

### 批处理最佳实践
```java
// Pseudo‑code: process a list of PDFs in parallel, limiting to 5 concurrent TSA calls
```
*避免创建过多线程；5‑10 个并发签名在吞吐量与 TSA 负载之间取得平衡。*

### 磁盘 I/O 优化
临时文件使用 SSD，尽量减少读写次数，签名完成后清理临时产物。

## 故障排查指南

### 错误：“Invalid Certificate Password”
**解决方案：** 使用 `keytool -list -keystore your.pfx` 验证密码。

```java
ExecutorService executor = Executors.newFixedThreadPool(5);
List<Future<SignResult>> futures = new ArrayList<>();

for (String pdfPath : pdfPaths) {
    futures.add(executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            return sig.sign(outputPath, options);
        }
    }));
}

// Wait for all to complete
for (Future<SignResult> future : futures) {
    SignResult result = future.get();
    // Process result
}

executor.shutdown();
```

### 错误：“Timestamp Authority Not Responding”
**解决方案：** 检查 TSA URL，确认防火墙规则，并添加备用 TSA 逻辑。

```bash
keytool -list -v -keystore certificate.pfx -storetype PKCS12
```

### 错误：“PDF is Already Signed”
**解决方案：** 先检测已有签名；可以添加联署签名或对原文件重新签名。

### 错误：“Access Denied” 在保存时
**解决方案：** 确认输出目录存在、应用拥有写权限，并且没有其他进程锁定文件。

```java
TimeStamp timeStamp;
try {
    timeStamp = new TimeStamp("https://freetsa.org/tsr", "", "");
} catch (Exception e) {
    // Fallback to alternative TSA
    timeStamp = new TimeStamp("https://alternate-tsa.com/tsr", "", "");
}
```

### 错误：OutOfMemoryError
**解决方案：** 增加 JVM 堆，分批处理 PDF，或对超大文件使用流式 API。

## 结论与后续步骤

你已经掌握了 **如何使用 Java 为 PDF 添加签名**、附加可信时间戳以及常见问题的处理方法。接下来可以探索：

1. 为多方协议添加多个签名字段。  
2. 使用 GroupDocs.Signature 编程验证签名。  
3. 自定义签名外观（图像、文字、定位）。  
4. 构建具备队列和监控的批量签名服务。

## 常见问题

**Q: 数字签名和电子签名有什么区别？**  
A: 数字签名使用加密算法验证身份并检测篡改，而电子签名可以仅是键入的姓名等简单形式。

**Q: 签署 PDF 是否需要网络连接？**  
A: 仅在获取时间戳服务时需要网络，密码学签名本身在本地完成。

**Q: 已签名的 PDF 还能被编辑吗？**  
A: 任何修改都会破坏签名，PDF 阅读器会显示文档已被更改的警告。

**Q: 如何验证已签名的 PDF？**  
A: 大多数 PDF 阅读器会自动验证；编程上可使用 GroupDocs.Signature 的验证 API 检查状态、签署者信息和时间戳有效性。

**Q: 如果证书在签署后过期会怎样？**  
A: 嵌入的时间戳证明签名在证书仍然有效时创建，从而保持法律效力。

**Q: 能否在云存储（S3、Azure Blob 等）中使用？**  
A: 可以——先将 PDF 下载到临时位置签名，然后再上传已签名的版本。

**Q: 有文件大小限制吗？**  
A: 该库在不将整个文件加载到内存的情况下支持最高 500 MB 的 PDF；更大的文件可能需要流式处理。

**Q: GroupDocs.Signature 商业版费用是多少？**  
A: 费用依据部署类型而定，请联系 GroupDocs 销售获取最新报价。提供免费试用和临时许可证供评估。

**Q: 这在 Linux 服务器上能运行吗？**  
A: 完全可以。GroupDocs.Signature for Java 与平台无关，任何装有 JRE 的操作系统都能运行。

**Last Updated:** 2026-06-11  
**Tested With:** GroupDocs.Signature 23.9 for Java  
**Author:** GroupDocs

```java
File outputFile = new File(outputFilePath);
outputFile.getParentFile().mkdirs(); // Create directories if needed

if (!outputFile.canWrite() && outputFile.exists()) {
    throw new IOException("Cannot write to " + outputFilePath);
}
```

## 相关教程

- [How to Verify Digital Certificates in Java - Complete Guide with Code Examples](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [How to Sign PDF Programmatically in Java with GroupDocs.Signature](/signature/java/digital-signatures/sign-pdfs-groupdocs-signature-java/)
- [Add Image Signature to PDF Java with GroupDocs](/signature/java/image-signatures/sign-pdf-image-signature-groupdocs-java/)