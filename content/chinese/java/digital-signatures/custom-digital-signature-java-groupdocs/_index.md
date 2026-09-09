---
categories:
- Document Security
- Java Development
date: '2026-06-21'
description: 了解如何使用 GroupDocs.Signature 在 pdf 中添加 java 签名。提供代码片段的分步教程，帮助实现安全的数字签名
  java。
keywords:
- java add signature to pdf
- digital signature implementation java
- groupdocs signature java
lastmod: '2026-06-21'
linktitle: java 在 pdf 中添加签名
schemas:
- author: GroupDocs
  dateModified: '2026-06-21'
  description: Learn how to java add signature to pdf using GroupDocs.Signature. Step-by-step
    tutorial with code snippets for secure digital signature implementation java.
  headline: java add signature to pdf with GroupDocs.Signature
  type: TechArticle
- description: Learn how to java add signature to pdf using GroupDocs.Signature. Step-by-step
    tutorial with code snippets for secure digital signature implementation java.
  name: java add signature to pdf with GroupDocs.Signature
  steps:
  - name: Set Up Your File Paths
    text: 'First, define where everything lives—your document, certificate, signature
      image, and output file: **Real‑world tip:** Use environment variables or configuration
      files for these paths instead of hard‑coding them. Makes deployment across different
      environments much cleaner.'
  - name: Initialize the Signature Object
    text: 'Create a Signature object that points to your document: **What''s happening
      here:** The `Signature` class is the core component of GroupDocs.Signature that
      represents a single document in memory and prepares it for signing. It automatically
      detects the document type (PDF, DOCX, etc.) and uses the app'
  - name: Configure Digital Sign Options
    text: 'Now comes the interesting part—setting up how you want to sign the document:
      **Let''s break this down:** - **Certificate path**: Your digital ID (the `.pfx`
      file) - **Password**: Protects your certificate (like a PIN for your ID card)
      - **Reason**: Why you''re signing (appears in signature properties)'
  - name: Customize Signature Appearance
    text: 'Here''s where you make it look professional. You can add your logo, position
      it precisely, and ensure it doesn''t overlap with document content: **Customization
      tips:** - **Image size**: Keep it reasonable (50‑100 px typically). Too large
      and it dominates the page. - **Positioning**: Bottom‑right is s'
  - name: Apply the Signature and Save
    text: 'Time to actually sign the document and save the result: **What''s happening:**
      The `sign()` method applies your digital signature to the document and saves
      it to the output path. The `SignResult` object contains information about what
      was signed (useful for logging or audit trails). **Performance not'
  type: HowTo
- questions:
  - answer: Use GroupDocs.Signature's verification feature with a `VerifyOptions`
      object; the `verify()` method returns a `VerifyResult` indicating integrity
      and trust status.
    question: How do I verify if a signature is valid?
  - answer: Absolutely. Omit the `setImageFilePath()` call and the document will be
      cryptographically signed while remaining visually unchanged.
    question: Can I sign documents without a visible signature image?
  - answer: PDF, DOC/DOCX, XLS/XLSX, PPT/PPTX, ODT, ODS, ODP, JPEG, PNG, TIFF, BMP,
      GIF, and many more – see the full list in the [format documentation](https://docs.groupdocs.com/signature/java/supported-document-formats/).
    question: What document formats does GroupDocs.Signature support?
  - answer: Pricing varies by license type (developer, site, OEM). Start with their
      [free trial](https://releases.groupdocs.com/signature/java/) to test functionality.
      For production, [contact sales](https://purchase.groupdocs.com/buy) or check
      pricing on their website. Discounts are available for multiple licenses.
    question: How much does GroupDocs.Signature cost?
  - answer: Both. GroupDocs.Signature runs anywhere Java runs—Spring Boot, servlets,
      microservices, or desktop apps. In web scenarios, handle file uploads server‑side,
      sign, then stream the signed file back to the client.
    question: Can I use this in a web application or only desktop apps?
  type: FAQPage
tags:
- digital-signatures
- java
- pdf-signing
- document-security
- groupdocs
title: 使用 GroupDocs.Signature 在 pdf 中添加 java 签名
type: docs
url: /zh/java/digital-signatures/custom-digital-signature-java-groupdocs/
weight: 1
---

# 如何在 Java 中使用 GroupDocs.Signature 为 PDF 添加签名

是否曾经通过电子邮件发送过重要文件，却担心在到达收件人之前会被篡改？或者你是否经历过打印、签名、扫描、再通过电子邮件来回传递文件的繁琐过程？有更好的办法。

数字签名优雅地解决了这两个问题。它们就像普通签名，但更好——它们能够证明你的文档没有被更改 *并且* 验证签署者的身份。如果你正在构建处理合同、发票、报告或任何需要身份验证的文档的 Java 应用程序，你一定想了解如何正确实现数字签名。

在本指南中，我将带你使用 **GroupDocs.Signature** 在 Java 中为文档添加数字签名。我们将覆盖从基础设置到自定义签名外观的全部内容（是的，你可以添加公司徽标！）。阅读完毕后，你将拥有可以直接放入项目的可运行代码。

**你将学到的内容：**
- 为什么数字签名对文档安全至关重要
- 如何在 Java 中设置并使用 GroupDocs.Signature
- 带有自定义的逐步代码实现
- 常见陷阱及规避方法
- 实际使用案例和最佳实践

让我们开始吧。

## 快速答案
- **如何在 Java 中为 PDF 添加数字签名？** 使用 GroupDocs.Signature 的 `Signature` 类，配置 `SignOptions`，然后调用 `sign()` —— 只需几行代码。  
- **是否需要可见的签名图片？** 不需要。通过省略图片配置即可创建不可见的加密签名。  
- **支持哪些文件格式？** 超过 50 种格式，包括 PDF、DOCX、XLSX、PPTX 以及常见的图像类型。  
- **需要哪个 Java 版本？** JDK 8 或更高；库兼容 Java 8‑21。  
- **生产环境是否需要许可证？** 是的，有效的 GroupDocs.Signature 许可证会去除试用水印并解锁全部功能。

## 什么是 java add signature to pdf？
短语 *java add signature to pdf* 描述了使用 Java 代码以编程方式对 PDF 文档应用加密数字签名的过程。此操作保证了签名文件的真实性、完整性和不可否认性。通过嵌入签署者的证书，后续可以验证签名，以确保文档在签署后未被修改。

## 为什么数字签名很重要

在进入代码之前，先来聊聊 *为什么* 需要数字签名。

**传统签名存在问题。** 任何拥有扫描仪的人都可以复制你的签名并粘贴到其他文档上。没有办法证明文档在签署后未被修改。而且说实话，2025 年的打印‑签名‑扫描工作流已经让人痛苦不堪。

**数字签名通过加密解决这些问题。** 它们为你提供：

- **身份验证**：证明签署者的身份（就像出示身份证）  
- **完整性**：检测签署后文档是否被任何人修改（即使是单个字符的更改也会破坏签名）  
- **不可否认性**：签署者不能声称自己没有签署（前提是私钥保持私密）  
- **合规性**：满足许多司法辖区的法律要求（美国 ESIGN 法案，欧盟 eIDAS）  

可以把它想象成用蜡封住信封。如果封条被破坏，你就知道有人篡改了信件。数字签名以电子方式实现相同的效果，且安全性更强。

## 为什么选择 GroupDocs.Signature for Java？

在 Java 中有多种数字签名库可供选择。那么为什么选 GroupDocs.Signature？

**相较于 iText 或 Apache PDFBox 等替代方案：**

- **多格式支持**：支持 PDF、Word、Excel、PowerPoint、图像等（不仅限于 PDF）——覆盖超过 50 种输入和输出格式。  
- **更简洁的 API**：代码样板更少，方法更直观，平均可提升开发速度约 40 %。  
- **视觉自定义**：轻松添加图片、定位和样式，让每份文档都带有品牌标识。  
- **内置验证**：无需额外库即可验证已有签名，降低依赖负担。  
- **积极维护**：定期更新并提供响应式支持，确保库在最新的 Java 版本上安全兼容。  

**适用场景：**
- 构建文档管理系统  
- 创建自动化签署工作流  
- 为现有应用添加签名功能  
- 处理多种文档格式  

**可能选择其他方案的情况：**
- 仅需免费/开源（GroupDocs 在生产环境需要许可证）  
- 仅限 PDF 且需要非常底层的控制（iText 可能更合适）  
- 简单任务可以使用 Java 自带的安全类完成  

对于大多数需要可靠、可投入生产的跨格式签名实现的真实场景，GroupDocs.Signature 是最佳选择。

## 前置条件

在开始编码之前，请确保你已经具备：

- **Java Development Kit (JDK) 8 或更高** – 从 [Oracle](https://www.oracle.com/java/technologies/javase-downloads.html) 下载或使用 OpenJDK  
- **Maven 或 Gradle** – 用于依赖管理（本教程使用 Maven，Gradle 亦可）  
- **基本的 Java 知识** – 熟悉类、对象和异常处理  
- **数字证书** – 需要 `.pfx` 或 `.p12` 文件（稍后会解释）  
- **GroupDocs.Signature 许可证** – 可先使用他们的 [免费试用](https://releases.groupdocs.com/signature/java/) 或获取 [临时许可证](https://purchase.groupdocs.com/temporary-license/)  

**关于数字证书：** 将证书视作你的数字身份证。它包含公钥，通常由证书颁发机构（CA）签发。测试时，你可以使用 Java 的 `keytool` 创建自签名证书。正式环境则建议使用 DigiCert、Let’s Encrypt 等受信任的 CA 颁发的证书。

## 为 Java 设置 GroupDocs.Signature

让我们把库引入项目。非常简单——只需添加依赖即可。

### Maven 设置

在你的 `pom.xml` 文件中加入以下内容：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**注意：** 请查看 [GroupDocs releases](https://releases.groupdocs.com/signature/java/) 获取最新版本号。使用最新版本可获得错误修复和新功能。

### Gradle 设置

如果使用 Gradle，请在 `build.gradle` 中加入：

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下载选项

不想使用构建工具？你可以直接从 [GroupDocs.Signature releases](https://releases.groupdocs.com/signature/java/) 下载 JAR 并手动加入项目的类路径。（不过说实话，使用 Maven 或 Gradle 更省事。）

### 许可证配置

**使用免费试用版：** 试用版功能完整，但会在输出文档上添加水印，适合测试和开发。

**生产环境使用：** 需要临时许可证（开发 30 天）或正式许可证。请在创建 `Signature` 对象之前在代码中应用：

```java
License license = new License();
license.setLicense("path/to/GroupDocs.Signature.lic");
```

## 如何在 Java 中为 PDF 添加签名？

`Signature` 类代表可以签名或验证的文档。使用 `new Signature("input.pdf")` 加载目标 PDF，配置 `SignOptions`（包括证书路径、密码、原因、位置等），可选地设置可见图片，然后调用 `sign(outputPath)`。这段简洁的流程在内存中完成签名，并将防篡改的 PDF 写入磁盘，仅需几行 Java 代码。

## 实现：为文档添加数字签名

下面我们一步步编写代码，帮助你理解每个部分的作用。

### 步骤 1：设置文件路径

首先，定义文档、证书、签名图片和输出文件的所在位置：

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/contract.pdf";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signed_contract.pdf";
String certificatePath = "YOUR_CERTIFICATE_PATH/certificate.pfx";
String imagePath = "YOUR_IMAGE_PATH/company_logo.jpg";
```

**实际经验提示：** 使用环境变量或配置文件来存放这些路径，而不是硬编码。这样在不同环境之间部署会更干净。

### 步骤 2：初始化 Signature 对象

创建指向文档的 Signature 对象：

```java
try {
    Signature signature = new Signature(filePath);
```

**发生了什么：** `Signature` 类是 GroupDocs.Signature 的核心组件，代表内存中的单个文档并为签名做好准备。它会自动检测文档类型（PDF、DOCX 等），并使用相应的处理器。

**常见错误：** 忘记关闭 `Signature` 对象。请始终使用 try‑with‑resources 或在 finally 块中显式调用 `signature.close()`，以避免内存泄漏。

### 步骤 3：配置数字签名选项

接下来设置签名的具体参数：

```java
DigitalSignOptions digitalSignOptions = new DigitalSignOptions(certificatePath);
digitalSignOptions.setPassword("1234567890");
digitalSignOptions.setReason("Agreement approval");
digitalSignOptions.setContact("john.smith@company.com");
digitalSignOptions.setLocation("New York Office");
```

**拆解说明：**

- **证书路径**：你的数字身份证（`.pfx` 文件）  
- **密码**：保护证书的密码（相当于身份证的 PIN）  
- **原因**：签署的目的（会出现在签名属性中）  
- **联系人**：你的电子邮件或联系信息  
- **位置**：签署发生的地点  

**这些细节为何重要：** 当有人在 Adobe Acrobat 或其他 PDF 查看器中查看签名属性时，会看到这些信息。它提供上下文并增加验证力度。在法律场景下，这些元数据可能至关重要。

### 步骤 4：自定义签名外观

在这里让签名更具专业感。你可以添加公司徽标、精准定位，并确保不与文档内容重叠：

```java
// Add your company logo or signature image
digitalSignOptions.setImageFilePath(imagePath);
digitalSignOptions.setWidth(80);  // Width in pixels
digitalSignOptions.setHeight(60); // Height in pixels

// Position it in the bottom-right corner
digitalSignOptions.setVerticalAlignment(VerticalAlignment.Bottom);
digitalSignOptions.setHorizontalAlignment(HorizontalAlignment.Right);

// Add some breathing room so it doesn't touch the edges
Padding padding = new Padding();
padding.setBottom(10);
padding.setRight(10);
digitalSignOptions.setMargin(padding);
```

**自定义技巧：**

- **图片尺寸**：保持在 50‑100 px 左右，太大容易抢占页面。  
- **定位**：右下角是常规位置，可根据文档布局自行调整。  
- **内边距**：至少留 10 px，防止裁剪或覆盖内容。  
- **图片格式**：PNG（透明）最适合徽标，JPG 适用于照片。  

**如果不想要可见签名怎么办？** 只需省略 `setImageFilePath()` 行。文档仍会被加密签名，只是页面上看不见任何视觉标记。

### 步骤 5：应用签名并保存

最后真正签署文档并写入结果：

```java
    SignResult signResult = signature.sign(outputFilePath, digitalSignOptions);
    System.out.println("Document signed successfully!");
    System.out.println("Output saved to: " + outputFilePath);
    
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
    throw new GroupDocsSignatureException(e.getMessage());
}
```

**发生了什么：** `sign()` 方法将数字签名应用到文档并保存到指定输出路径。`SignResult` 对象包含签署的详细信息，便于日志记录或审计。

**性能提示：** 对于 100 页以上的大文档，可能需要几秒钟。建议在生产环境中异步执行，以免阻塞用户交互。

## GroupDocs.Signature 中的 Signature 类是什么？
`Signature` 类是 GroupDocs.Signature 中所有签署和验证操作的入口点。它加载文档、检测格式，并提供用于应用或验证数字签名的方法。开发者还可以通过该对象的属性获取签名元数据，如签署时间和签署者信息。

## 为什么要自定义数字签名的外观？

自定义外观可以让收件人立即识别签署者的品牌，提升文档的视觉可信度。添加徽标、统一位置和企业配色可以降低签名被视为通用占位符的风险，这在受监管行业尤为重要。精心设计的签名还能符合品牌指南，并可包含签署日期或角色等附加信息，进一步增强可信度。

## 如何以编程方式验证已签名的 PDF？

`VerifyOptions` 用于指定验证过程的参数，例如待检查的文件和验证设置。使用 `Signature` 对象的 `verify()` 方法并传入配置好的 `VerifyOptions`，即可得到 `VerifyResult`，该结果指示签名是否完整、证书是否受信任以及是否检测到篡改。这样可以在自动化工作流中在进一步处理前拒绝被修改的文件。

## 何时使用不可见的数字签名？

不可见签名非常适合内部审计日志、批处理流水线或任何会因视觉签名而导致文档布局混乱的场景。它们仍然提供完整的完整性和真实性证明，但最终用户看到的是干净、未被修改的文档。

## 常见陷阱及解决方案

我在多个项目中实现过此功能，以下是我遇到的问题（你也可能会遇到）：

### 问题 1：“Invalid Certificate Password”

**症状：** 加载证书时抛出异常。

**解决方案：** 
- 仔细检查密码（虽然显而易见，但经常出错）  
- 确认证书文件未损坏（可在 Windows 中打开或使用 `keytool` 检查）  
- 确认使用的是正确的证书类型（`.pfx` 或 `.p12`）

### 问题 2：签名出现在错误位置

**症状：** 签名图片出现在奇怪的位置或被截断。

**解决方案：** 
- 检查填充值——负数填充会把签名推到页面之外  
- 核实垂直/水平对齐设置  
- 在不同页面尺寸（A4 与 Letter）下测试  
- 记住：坐标是相对于页面的，而非绝对坐标

### 问题 3：大文档导致 OutOfMemoryError

**症状：** 对 50 MB 以上的 PDF 签名时应用崩溃。

**解决方案：** 
- 增加 JVM 堆内存：`-Xmx2g`  
- 若一次签署多个文件，请分批处理  
- 如库版本支持，考虑使用流式 API  
- 使用完毕后立即关闭 `Signature` 对象

### 问题 4：签名仅出现在首页

**症状：** 多页文档只在第 1 页显示签名。

**解决方案：** 默认情况下签名会应用到所有页面。如果只在一页看到，检查是否设置了特定页码：

```java
// This restricts to page 1 only - remove if not needed
digitalSignOptions.setPageNumber(1);
```

想让签名出现在所有页面？不要设置页码。若只想在特定页面出现，请使用 `setAllPages(false)` 并指定页码。

## 实际使用案例

下面展示数字签名在生产环境中的真实应用：

### 案例 1：自动化合同签署工作流

**场景：** 为 HR 系统构建在审批通过后自动签署 offer letter 的功能。

**实现：**  
- 将证书安全存储在 Azure Key Vault、AWS Secrets Manager 等位置  
- 审批工作流完成后触发签署  
- 将已签署文档通过电子邮件发送给候选人  
- 将签署副本存入文档管理系统  

**收益：** 消除手动打印/扫描环节，将周转时间从数天缩短至数分钟。

### 案例 2：批量发票签署

**场景：** 会计部门每月生成 500 份发票，需要统一签署。

**实现：**  
- 从目录加载所有发票 PDF  
- 循环对每个文件应用签名  
- 为签名添加时间戳以作审计追踪  
- 输出至 `signed_invoices` 文件夹  

**收益：** 原本半天的工作现在只需 5 分钟，且数字签名防止发票被篡改。

### 案例 3：保障学位证书真实性

**场景：** 大学需要为成千上万的毕业证书和成绩单提供认证。

**实现：**  
- 根据学生数据库生成证书 PDF  
- 使用学校官方数字签名进行签署  
- 添加指向验证门户的二维码  
- 安全存储并通过电子邮件发送给毕业生  

**收益：** 毕业生可向雇主证明证书真实性，学校降低伪造风险并减少行政成本。

### 案例 4：API 文档签署服务

**场景：** 构建一个 REST API，供客户端上传文档进行签署。

**实现：**  
- 接收 POST 请求中的文档  
- 应用组织的数字签名  
- 返回已签署文档或下载链接  
- 记录所有签署操作以满足合规要求  

**收益：** 为多个应用提供统一的签署服务，便于集中管理证书和审计。

## 生产环境最佳实践

在多个系统中实现数字签名后，我总结出以下建议：

**安全：**  
- 将证书存放在安全金库，绝不放入版本控制  
- 使用强密码（16 位以上，避免常见模式）  
- 在证书到期前进行轮换  
- 实施访问控制，仅授权特定用户触发签署操作  
- 为每次签署记录时间戳、用户 ID 等日志信息  

**性能：**  
- 若一次签署多份文档，可缓存 `Signature` 对象（批处理后记得关闭）  
- 对大文档使用异步处理  
- 对网络获取文档的场景实现重试机制  
- 监控生产环境的内存使用情况  

**用户体验：**  
- 为大文档签署提供进度指示器  
- 给出明确的错误信息（如 “证书已过期” 而不是 “Error 500”）  
- 允许用户在下载前预览已签署文档  
- 签署完成后发送邮件通知  

**维护：**  
- 为证书到期设置 60 天提前警报  
- 定期更新 GroupDocs.Signature 以获取安全补丁  
- 定期进行签名验证测试  
- 编写并维护证书续期流程文档  

## 为什么数字签名实现 Java 是战略优势

一个 **digital signature implementation java** 利用 GroupDocs.Signature 能够处理超过 50 种输入/输出格式，支持最高 200 页文档而无需一次性加载全部内容，并在典型服务器硬件上实现 200 ms 以下的签名验证。这些量化能力转化为更快的用户 onboarding、降低人工成本以及在企业应用中提供合规信心。

## 结论

现在你已经掌握了在 Java 应用中实现数字签名的全部要点。我们覆盖了数字签名为何重要、完整的代码实现、常见问题以及真实案例。

**快速回顾：**  
- 数字签名提供身份验证、完整性和不可否认性  
- GroupDocs.Signature 简化了跨多种文档格式的实现  
- 自定义选项让签名具备专业品牌形象  
- 生产环境必须做好错误处理和安全防护  

**下一步：**  
- 使用自己的文档和证书尝试上述代码  
- 探索 GroupDocs.Signature 的其他功能（签名验证、二维码、表单字段）  
- 将签署功能集成到现有工作流中  
- 查阅 [文档](https://docs.groupdocs.com/signature/java/) 了解高级场景  

有疑问？遇到问题？[GroupDocs 论坛](https://forum.groupdocs.com/c/signature/) 活跃且乐于助人。

## FAQ

**Q: 如何验证签名是否有效？**  
A: 使用 GroupDocs.Signature 的验证功能，创建 `VerifyOptions` 对象并调用 `verify()` 方法，返回的 `VerifyResult` 会指示完整性、证书可信度以及是否检测到篡改。

**Q: 可以在不显示签名图片的情况下签署文档吗？**  
A: 完全可以。省略 `setImageFilePath()` 调用，文档仍会被加密签名，只是视觉上保持不变。

**Q: GroupDocs.Signature 支持哪些文档格式？**  
A: PDF、DOC/DOCX、XLS/XLSX、PPT/PPTX、ODT、ODS、ODP、JPEG、PNG、TIFF、BMP、GIF 等等——完整列表请参见 [格式文档](https://docs.groupdocs.com/signature/java/supported-document-formats/)。

**Q: GroupDocs.Signature 的费用是多少？**  
A: 费用取决于许可证类型（开发者、站点、OEM）。可先使用他们的 [免费试用](https://releases.groupdocs.com/signature/java/) 进行功能测试。生产环境请 [联系销售](https://purchase.groupdocs.com/buy) 或查看官网定价。多许可证可享受折扣。

**Q: 这可以用于 Web 应用吗，还是只能用于桌面应用？**  
A: 两者皆可。GroupDocs.Signature 可运行在任何支持 Java 的环境——Spring Boot、Servlet、微服务或桌面应用。Web 场景下，服务器端处理文件上传、签署后再将已签署文件流回客户端。

**Q: 如果我的证书过期会怎样？**  
A: 已签名的文档如果已时间戳，则仍然有效。过期证书无法用于创建新签名，请提前续订并在配置中更新证书路径。

**Q: 这在法律上有约束力吗？**  
A: 符合 X.509 等标准的数字签名在大多数司法辖区被法律认可（如 ESIGN 法案、eIDAS 等）。具体法律要求因地区而异，请咨询法律顾问以确保合规。

## 资源

- **文档**： [GroupDocs.Signature for Java 文档](https://docs.groupdocs.com/signature/java/)  
- **API 参考**： [完整的 Java API 参考](https://reference.groupdocs.com/signature/java/)  
- **下载**： [最新版本与发布](https://releases.groupdocs.com/signature/java/)  
- **支持**： [GroupDocs 论坛](https://forum.groupdocs.com/c/signature/)  
- **购买**： [购买许可证](https://purchase.groupdocs.com/buy)  
- **免费试用**： [下载试用版](https://releases.groupdocs.com/signature/java/)

---

**最后更新：** 2026-06-21  
**测试于：** GroupDocs.Signature 23.10 for Java  
**作者：** GroupDocs

```java
DigitalVerifyOptions verifyOptions = new DigitalVerifyOptions();
VerificationResult result = signature.verify(verifyOptions);
System.out.println("Valid: " + result.isValid());
```

## 相关教程

- [如何在 Java 中添加数字签名 - 完整的 GroupDocs 教程](/signature/java/getting-started/groupdocs-signature-java-digital-setup-guide/)  
- [在 Java 中为 PDF 添加数字签名](/signature/java/digital-signatures/implement-digital-signatures-pdf-groupdocs-java/)  
- [在 Java 中为 PDF 添加带时间戳的数字签名](/signature/java/digital-signatures/digital-signature-timestamp-pdf-java-groupdocs/)