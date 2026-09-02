---
categories:
- Java Development
date: '2026-06-11'
description: 学习如何使用 Java 为 PDF 和文档添加 digital signatures。完整指南，包含 code examples、troubleshooting
  tips 和 security best practices。
keywords:
- add digital signature java
- implement digital signatures java
- java document signing library
- groupdocs signature java
- digital certificate handling java
lastmod: '2025-01-02'
linktitle: Java 中的 Digital Signatures
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to add digital signatures to PDF and documents using Java.
    Complete guide with code examples, troubleshooting tips, and security best practices.
  headline: How to Add Digital Signatures to Documents in Java
  type: TechArticle
- description: Learn how to add digital signatures to PDF and documents using Java.
    Complete guide with code examples, troubleshooting tips, and security best practices.
  name: How to Add Digital Signatures to Documents in Java
  steps:
  - name: '**Incorrect password** – verify with OpenSSL: `openssl pkcs12 -info -in
      yourcert.pfx`.'
    text: '**Incorrect password** – verify with OpenSSL: `openssl pkcs12 -info -in
      yourcert.pfx`.'
  - name: '**Expired certificate** – check the validity using `keytool -list -v -keystore
      yourcert.pfx`.'
    text: '**Expired certificate** – check the validity using `keytool -list -v -keystore
      yourcert.pfx`.'
  - name: '**Wrong file format** – only `.pfx` or `.p12` (which contain private keys)
      are accepted.'
    text: '**Wrong file format** – only `.pfx` or `.p12` (which contain private keys)
      are accepted.'
  - name: '**File permission problems** – ensure the Java process can read the certificate
      file.'
    text: '**File permission problems** – ensure the Java process can read the certificate
      file.'
  - name: Store `.pfx` files in a secure vault (AWS Secrets Manager, Azure Key Vault,
      or HashiCorp Vault).
    text: Store `.pfx` files in a secure vault (AWS Secrets Manager, Azure Key Vault,
      or HashiCorp Vault).
  - name: Load the password at runtime from environment variables or the vault’s API.
    text: Load the password at runtime from environment variables or the vault’s API.
  - name: Restrict file system permissions so only the service account can read the
      certificate.
    text: Restrict file system permissions so only the service account can read the
      certificate.
  - name: Rotate certificates at least 30 days before expiration and update the stored
      secret accordingly.
    text: Rotate certificates at least 30 days before expiration and update the stored
      secret accordingly.
  - name: '**Automated Contract Workflows** – When a contract reaches the “approved”
      state in your BPM system, trigger the signing service to embed the legal department’s
      certificate and email the signed copy to the vendor.'
    text: '**Automated Contract Workflows** – When a contract reaches the “approved”
      state in your BPM system, trigger the signing service to embed the legal department’s
      certificate and email the signed copy to the vendor.'
  - name: '**Invoice Approval Systems** – After finance signs off an invoice, automatically
      add a digital signature before sending it to the customer, providing cryptographic
      proof of authenticity.'
    text: '**Invoice Approval Systems** – After finance signs off an invoice, automatically
      add a digital signature before sending it to the customer, providing cryptographic
      proof of authenticity.'
  type: HowTo
- questions:
  - answer: iText focuses solely on PDF and requires you to handle low‑level cryptography
      yourself, while GroupDocs.Signature supports 30+ formats, offers ready‑made
      visual stamps, and abstracts certificate handling, reducing development time
      dramatically.
    question: What’s the main difference between GroupDocs.Signature and iText for
      PDF signing?
  - answer: Yes. Add the Maven dependency, create a `@Service` bean that wraps the
      signing logic, and inject it wherever you need to sign documents. This keeps
      your controllers thin and your signing code reusable.
    question: Can I integrate GroupDocs.Signature into a Spring Boot microservice?
  - answer: The library uses standard PKI algorithms (RSA/ECDSA) and follows the same
      specifications as browsers and Adobe Reader. Security depends on the quality
      of your certificate; always use a CA‑issued certificate and protect the private
      key.
    question: How secure are signatures created with GroupDocs.Signature?
  - answer: Absolutely. As long as the signing certificate is trusted, Adobe Reader,
      Foxit, and modern browsers will validate the signature correctly. Self‑signed
      certificates will display a warning but remain technically valid.
    question: Will signed documents work across different PDF readers?
  - answer: Yes—simply omit the `ImageFilePath` and set size parameters to zero. The
      resulting signature is invisible but still cryptographically sound, perfect
      for backend automation where visual cues aren’t required.
    question: Is it possible to sign documents without a visible signature image?
  type: FAQPage
tags:
- digital-signatures
- document-security
- java-libraries
- pdf-signing
title: 如何在 Java 中为文档添加 Digital Signatures
type: docs
url: /zh/java/digital-signatures/groupdocs-signature-java-digital-signing-guide/
weight: 1
---

# 如何在 Java 中为文档添加数字签名

## 介绍

实现 **add digital signature java** 功能可能感觉像在雷区中行走。您必须兼顾证书格式、签名位置和严格的安全策略——同时保持用户体验流畅。一步走错，就会出现无效签名或在 Adobe Reader 中验证失败的文档。

幸运的是，您无需重新发明轮子或与底层加密搏斗。无论是构建合同管理门户、需要签名收据的电子商务结算，还是内部 HR 工作流，可靠的 Java 库都能为您节省数小时的开发时间并消除常见陷阱。

在本指南中，我们将深入了解 **GroupDocs.Signature for Java**，这是一款商业库，抽象了数字签名的繁重工作。您将学习如何：

* 正确设置库并配置证书  
* 使用专业的可视化印章对 PDF、Word、Excel 和 PowerPoint 文件进行签名  
* 验证签名并处理常见错误，如不受信任的证书或内存瓶颈  
* 为生产环境应用最佳实践安全措施  

完成后，您将拥有一个即插即用的实现，可扩展到应用处理的任何文档类型。

## 快速答案
- **哪个库可以在 Java 中添加数字签名？** GroupDocs.Signature for Java。  
- **支持多少种文档格式？** 超过 30 种格式，包括 PDF、DOCX、XLSX、PPTX 和图像文件。  
- **生产环境是否需要许可证？** 是的——商业许可证可去除水印并解锁全部功能。  
- **能否在不出现 OOM 错误的情况下签署大型 PDF（100+ 页）？** 可以——通过调整 JVM 堆并使用 `setAllPages(false)` 选项。  
- **是否支持时间戳？** 当然；您可以附加受信任的时间戳机构（TSA）令牌，以实现长期有效性。

## 什么是 add digital signature java？
`add digital signature java` 指的是使用 Java API 将加密签名嵌入数字文档的编程过程。签名将签署者的身份（由数字证书验证）绑定到文档内容，确保完整性、不可否认性以及跨平台的法律效力。

## 为什么在 Java 中实现数字签名？
GroupDocs.Signature 支持 **30+ 输入和输出格式**，并且能够在不将整个文件加载到内存的情况下处理高达 **500 MB** 的文件，提供 **2‑5×** 的速度提升，相比手动使用 PDFBox 实现更快的交易时间和更低的服务器成本，适用于高并发工作负载。

## 前提条件

在开始之前，请确认您具备以下条件：

* **Java Development Kit (JDK) 8+** – 推荐使用 JDK 11，以获得更强的 TLS 支持。  
* **IDE** – IntelliJ IDEA、Eclipse 或带有 Java 扩展的 VS Code。  
* **GroupDocs.Signature for Java** – 我们将展示三种将其加入构建的方法。  
* **有效的数字证书**，格式为 **PFX** 或 **P12**（需要私钥和密码）。  

可选但有帮助：

* 熟悉 **Maven** 或 **Gradle** 进行依赖管理。  
* 用于测试签名流程的示例 PDF、DOCX 或 XLSX 文件。  

## 如何安装 GroupDocs.Signature for Java？

GroupDocs.Signature 只需在构建配置中简单添加即可。使用与您的构建工具匹配的代码片段，将占位版本号替换为最新稳定版，然后运行构建命令从 Maven Central 拉取库。

**Maven（添加到 pom.xml）：**  
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```  

**Gradle（添加到 build.gradle）：**  
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```  

**手动安装（如果不使用构建工具）：**  
从官方发布页面下载 JAR — [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) — 并将其加入类路径。

> **专业提示：** 始终引用最新的稳定版本。本文撰写时，版本 23.12 为当前版本，但更新的发布通常包含安全补丁和性能改进。

## 如何获取并应用 GroupDocs 许可证？

GroupDocs.Signature 在生产环境中需要许可证。许可证可去除水印并解锁完整功能集，确保签署的文档符合企业政策。

* **免费试用：** 在 [Temporary License Page](https://purchase.groupdocs.com/temporary-license/) 获取 30 天临时许可证。  
* **付费许可证：** 在 [GroupDocs Purchase Page](https://purchase.groupdocs.com/buy) 购买开发者或企业许可证。  

没有有效许可证，签署的文档将包含可见水印，仅用于评估目的。

## 如何初始化 Signature 对象？

`Signature` 类是所有文档操作的入口点。它在内存中表示单个文件，并提供签名、验证和提取签名的方法。创建 `Signature` 实例会加载目标文件并为后续处理做好准备。

```java
Signature signature = new Signature("path/to/input.pdf");
```

**这里发生了什么？**  
此行创建了一个加载目标文档的 `Signature` 实例。路径可以是绝对或相对的，只需确保文件存在。该对象可在批处理场景中重复用于多次签名或验证，从而降低开销。

## 如何配置数字签名选项？

数字签名选项封装了生成有效 PKI 签名所需的所有设置，包括证书信息、视觉外观和放置规则。正确的配置可确保生成的签名在密码学上可靠且在文档类型上视觉合适。

### 如何设置证书详情？

`DigitalSignOptions` 类保存所有与证书相关的设置。下面是该类的首次定义锚点。

`DigitalSignOptions` 定义了加密参数——证书文件、密码以及可选的元数据——库使用这些信息创建有效的 PKI 签名。

```java
DigitalSignOptions options = new DigitalSignOptions();
options.setCertificatePath("YOUR_DOCUMENT_DIRECTORY/certificate.pfx");
options.setCertificatePassword("yourPassword");
options.setReason("Approved Contract");
options.setContact("legal@yourcompany.com");
options.setLocation("New York, USA");
```

**关键要点：**  
* 切勿在代码中硬编码密码；应从环境变量或密钥管理器加载。  
* 使用 `setReason`、`setContact` 和 `setLocation` 为审阅者在检查签名属性时提供上下文。

### 如何自定义签名的视觉外观？

`SignatureOptions`（`DigitalSignOptions` 的子类）控制页面上的渲染。它允许您附加图像、调整大小并在页面上定位可视化印章。

`SignatureOptions` 允许您附加图像、调整大小并在页面上定位可视化印章。

```java
options.setImageFilePath("YOUR_DOCUMENT_DIRECTORY/signature.png");
options.setAllPages(true);
options.setWidth(150);
options.setHeight(0); // Auto‑scale based on image aspect ratio
```

* **ImageFilePath：** 指向手写签名或公司徽标的 PNG 或 JPG。透明 PNG 效果最佳。  
* **AllPages：** 对需要在每页都留下证明的合同设为 `true`；否则设为 `false` 仅在最后一页签名。  
* **Width/Height：** 以像素为单位；**50‑80** 像素的高度在大多数商务文档中看起来专业。

## 如何控制对齐和内边距？

对齐设置决定印章在页面上的落点，内边距则在视觉元素周围添加缓冲，防止其触及页面边缘。正确的对齐提升可读性，并确保签名不会干扰已有内容。

`AlignmentOptions` 提供垂直和水平放置常量，如 `Bottom`、`Right`、`Top` 和 `Center`。

```java
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setPadding(10);
```

* **Padding：** 为印章添加呼吸空间；**10** 像素的值可防止图像触及页面边缘。  
* **真实案例：** 在发票模板中，您可能使用 `Top`/`Left` 将审批人的签名放在页眉附近。

## 如何为 Office 文档添加签名行？

在签署 DOCX 或 XLSX 文件时，可见的签名行可提升终端用户的可读性。库会创建 Microsoft 风格的签名行，显示签署者的姓名、职务和电子邮件，模拟原生 Office 体验。

`SignatureLineOptions` 创建 Microsoft 风格的签名行，显示签署者的姓名、职务和电子邮件。

```java
options.setSignatureLineText("John Doe", "Chief Legal Officer", "j.doe@yourcompany.com");
```

* 此功能在 PDF 中被忽略，但对在 Microsoft Office 中打开的 Word 和 Excel 文件至关重要。

## 如何实际签署文档？

使用 `Signature` 实例加载源文件，应用完整配置的 `DigitalSignOptions`，并调用 `sign()`。库会将新文件写入输出路径，原文件保持不变。对于大型 PDF（50+ 页），预计处理时间为 2‑5 秒；在 Web 服务中可考虑异步执行。

```java
Signature signature = new Signature("SAMPLE_WORDPROCESSING/contract.docx");
DigitalSignOptions options = new DigitalSignOptions();
// ...configure options as shown earlier...
signature.sign("OUTPUT_FOLDER/signed_contract.docx", options);
```

**性能提示：** 对于超过 100 页的文档，增大 JVM 堆 (`-Xmx2g`) 或关闭 `setAllPages(true)` 以限制内存消耗。

## 如何排查常见问题？

签名失败时，最常见的问题与证书处理、视觉放置或内存限制有关。先确定症状，然后按照下面的针对性检查清单快速解决。

### 为什么会看到 “Invalid Certificate” 或 “Cannot Load Certificate” 错误？

这些异常通常源于以下四种原因：

1. **密码错误** – 使用 OpenSSL 验证：`openssl pkcs12 -info -in yourcert.pfx`。  
2. **证书已过期** – 使用 `keytool -list -v -keystore yourcert.pfx` 检查有效期。  
3. **文件格式错误** – 仅接受包含私钥的 `.pfx` 或 `.p12`。  
4. **文件权限问题** – 确保 Java 进程能够读取证书文件。

### 为什么签名没有出现在页面上？

* **AllPages 标志** 可能为 `false`，导致您查看的页面没有印章。  
* **图像路径** 可能拼写错误；打印 `options.getImageFilePath()` 进行确认。  
* **对齐设置** 可能将印章推到屏幕外；调试时可临时切换为 `Center`。

### 为什么 Adobe Reader 报告 “Signature Invalid”？

* **证书不受信任** – 自签名证书会触发警告。生产环境请使用 CA 颁发的证书。  
* **证书链不完整** – 确保 `.pfx` 包含中间证书和根证书。  
* **缺少时间戳** – 若未附加 TSA 令牌，证书过期后签名可能被视为无效。GroupDocs 支持通过 `setTimeStampOptions()` 添加时间戳。

### 如何避免在处理大型 PDF 时出现 OutOfMemoryError？

* 增大 JVM 堆 (`-Xmx4g` 或更高)。  
* 仅签署所需页面 (`setAllPages(false)`)。  
* 在受限环境下，将文件分批处理或使用流式方式读取。

## 如何在生产环境中安全管理证书？

切勿在源代码中嵌入证书或密码。请遵循以下步骤：

1. 将 `.pfx` 文件存放在安全保管库中（AWS Secrets Manager、Azure Key Vault 或 HashiCorp Vault）。  
2. 在运行时从环境变量或保管库 API 加载密码。  
3. 限制文件系统权限，仅允许服务账号读取证书。  
4. 在证书到期前至少 30 天进行轮换，并相应更新存储的密钥。

```java
String certPath = System.getenv("CERT_PATH");
String certPassword = System.getenv("CERT_PASSWORD");
options.setCertificatePath(certPath);
options.setCertificatePassword(certPassword);
```

## 如何记录签名操作以满足审计合规性？

审计日志提供不可否认的证据。请为每次签名事件记录以下字段：

* 签名前的文档名称和哈希值  
* 签署者身份（证书主题）  
* 操作时间戳（建议使用 UTC）  
* 结果状态（成功/失败）以及错误详情（如有）  

```java
logger.info("Signing document {} with certificate {} at {}", docPath, options.getCertificatePath(), Instant.now());
```

## 如何在签名后验证签名？

验证可确保文档在签名后未被篡改。使用 `verify()` 方法，它返回包含有效性状态、签署者详情以及时间戳信息的 `VerificationResult`。成功的验证同时确认完整性和真实性。

```java
VerificationResult result = signature.verify("OUTPUT_FOLDER/signed_contract.docx");
if (result.isValid()) {
    logger.info("Signature is valid and trusted.");
} else {
    logger.warn("Signature verification failed: {}", result.getErrorMessage());
}
```

## 如何向单个文档添加多个签名？

您可能需要批准人和见证人签名。对不同的 `DigitalSignOptions` 实例多次调用 `sign()`，每个实例使用各自的证书和视觉设置。库会保留已有签名并追加新签名。

```java
// First signature (approver)
signature.sign("output.docx", approverOptions);
// Second signature (witness)
signature.sign("output.docx", witnessOptions);
```

## 如何为不同文档类型创建工厂方法？

可以编写一个帮助方法，根据文件扩展名返回预配置好的 `DigitalSignOptions`，从而保持代码 DRY。该方法统一管理证书加载、视觉默认值以及 PDF、Word、Excel 等格式的页面选择逻辑。

```java
public DigitalSignOptions getOptionsFor(String extension) {
    DigitalSignOptions opts = new DigitalSignOptions();
    // common settings
    if (extension.equalsIgnoreCase("pdf")) {
        opts.setImageFilePath("signatures/pdf_stamp.png");
    } else if (extension.equalsIgnoreCase("docx")) {
        opts.setSignatureLineText("Jane Smith", "Finance Manager", "j.smith@company.com");
    }
    return opts;
}
```

## 如何验证文档是否已经签名？

在应用新签名之前，检查是否已有签名以避免重复签名。使用 `getSignatures()` 方法；如果返回的集合非空，则决定是追加新签名还是中止操作。

```java
List<SignatureInfo> existing = signature.getSignatures();
if (!existing.isEmpty()) {
    logger.warn("Document already contains {} signatures.", existing.size());
}
```

## 实际应用（真实案例）

1. **自动化合同工作流** – 当合同在 BPM 系统中进入 “已批准” 状态时，触发签名服务嵌入法务部门的证书并将签署副本邮件给供应商。  
2. **发票审批系统** – 财务完成发票签署后，自动添加数字签名再发送给客户，提供加密的真实性证明。  
3. **文档验证门户** – 提供自助门户，用户上传 PDF，您使用公司统一证书签名并返回防篡改文件，以满足法律合规。  
4. **合规性高的行业** – 在医疗（HIPAA）或金融（SOX）领域，数字签名通过证明签署人和签署时间满足审计要求。  
5. **内部政策分发** – 用自动化流程替代人工在 HR 政策上盖章，使用首席人力资源官的证书签署最终 PDF，确保每位员工收到经过验证的副本。

## 性能考虑

| 文档大小 | 平均处理时间 | 推荐设置 |
|----------|--------------|----------|
| 1‑5 页   | ~0.5 秒      | 默认选项 |
| 5‑50 页  | 1‑3 秒       | 增大堆内存，必要时 `setAllPages(true)` |
| 50‑200 页| 3‑10 秒      | `setAllPages(false)`，异步执行，增大堆内存 |

**优化技巧：**  

* 在批量签署多个文件时复用同一个 `Signature` 实例。  
* 缓存已加载的 `DigitalSignOptions` 对象；重复加载证书会增加开销。  
* 对于 Web 服务，将签名调用包装在 `CompletableFuture` 中或推送到消息队列，以保持 UI 响应。

## 专业技巧（高级用法）

* **长期有效性的时间戳** – 使用 `setTimeStampOptions()` 附加 TSA 令牌，确保证书过期后签名仍然有效。  
* **隐形签名** – 省略 `ImageFilePath` 并将 `Width`/`Height` 设为 `0`，即可创建在密码学上有效但不可见的签名，适用于不需要视觉印章的后台流程。  
* **自定义二维码签名** – GroupDocs 能嵌入包含签署者元数据的二维码，适用于需要通过移动设备快速验证的供应链文档。  

## 常见问题

**Q: GroupDocs.Signature 与 iText 在 PDF 签名方面的主要区别是什么？**  
A: iText 仅专注于 PDF，且需要自行处理底层加密；而 GroupDocs.Signature 支持 30+ 格式，提供即用的可视化印章，并抽象证书处理，大幅缩短开发时间。

**Q: 能否将 GroupDocs.Signature 集成到 Spring Boot 微服务中？**  
A: 能。添加 Maven 依赖，创建包装签名逻辑的 `@Service` Bean，并在需要签名的地方注入它。这样可保持控制器简洁，签名代码可复用。

**Q: 使用 GroupDocs.Signature 创建的签名有多安全？**  
A: 库使用标准 PKI 算法（RSA/ECDSA），遵循浏览器和 Adobe Reader 相同的规范。安全性取决于证书质量；请始终使用 CA 颁发的证书并保护私钥。

**Q: 已签名的文档能在不同的 PDF 阅读器中正常工作吗？**  
A: 完全可以。只要签名证书受信任，Adobe Reader、Foxit 以及现代浏览器都会正确验证签名。自签名证书会显示警告，但在技术上仍然有效。

**Q: 能否在不使用可见签名图像的情况下签署文档？**  
A: 可以——只需省略 `ImageFilePath` 并将尺寸参数设为零。生成的签名虽不可见，但在密码学上仍然有效，适合后端自动化场景。

## 结论

您现在已经掌握了使用 GroupDocs.Signature 实现 **add digital signature java** 的完整、可投入生产的路线图。我们覆盖了从环境搭建、证书处理到视觉自定义、性能调优以及多签名和时间戳等高级场景的全部内容。

**后续步骤：**  

1. 使用自己的证书和文档模板测试示例代码。  
2. 通过将证书迁移至密钥管理器并配置适当的 JVM 内存限制来加固部署。  
3. 扩展帮助方法以支持批量处理或与现有工作流引擎集成。  

欲深入了解，请查阅官方文档和下方链接的社区论坛。

---

**最后更新：** 2026-06-11  
**测试环境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs  

**资源：**  
- [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/)  
- [Support Forum](https://forum.groupdocs.com/c/signature/)  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}
```java
import com.groupdocs.signature.Signature;

public class SignatureSetup {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // Your signing logic goes here
    }
}
```
```java
import com.groupdocs.signature.options.sign.DigitalSignOptions;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

DigitalSignOptions options = new DigitalSignOptions("YOUR_DOCUMENT_DIRECTORY/CertificatePfx");
options.setPassword("1234567890"); // Ensure your certificate password is secure
options.setReason("Sign"); // Reason for signing, e.g., "Contract Approval"
options.setContact("JohnSmith"); // Contact information of the signer
options.setLocation("Office1"); // Location where document is signed
```
```java
options.setImageFilePath("YOUR_DOCUMENT_DIRECTORY/ImageHandwrite");
options.setAllPages(true); // Apply signature to all pages of the document
options.setWidth(0); // Auto-width based on content
options.setHeight(60); // Height in pixels
```
```java
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
Padding padding = new Padding();
padding.setBottom(10); // Bottom padding for aesthetic spacing
padding.setRight(10); // Right padding to prevent clipping at edges
options.setMargin(padding);
```
```java
import com.groupdocs.signature.domain.signatures.DigitalSignatureAppearance;

options.setAppearance(new DigitalSignatureAppearance("John Smith", "Title", "jonny@test.com"));
```
```java
try {
    Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SAMPLE_WORDPROCESSING");
    String outputFilePath = "YOUR_OUTPUT_DIRECTORY/DigitalAppearance.docx";
    signature.sign(outputFilePath, options);
} catch (GroupDocsSignatureException e) {
    throw new RuntimeException(e.getMessage());
}
```
```java
// BAD - Don't do this
options.setPassword("1234567890");

// GOOD - Load from environment variable
String certPassword = System.getenv("CERT_PASSWORD");
if (certPassword == null) {
    throw new RuntimeException("CERT_PASSWORD environment variable not set");
}
options.setPassword(certPassword);
```
```java
logger.info("Document signed: {}, SignedBy: {}, Timestamp: {}", 
    documentName, signerEmail, LocalDateTime.now());
```
```java
// Verify the signature immediately after signing
List<DigitalSignature> signatures = signature.verify();
if (signatures.isEmpty()) {
    throw new RuntimeException("Signature verification failed");
}
```
```java
signature.sign(outputPath, approverOptions);
signature = new Signature(outputPath); // Reload the signed document
signature.sign(finalOutputPath, witnessOptions);
```
```java
public DigitalSignOptions getOptionsForDocType(String docType) {
    DigitalSignOptions options = new DigitalSignOptions(certPath);
    if (docType.equals("contract")) {
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        // Contract-specific settings
    } else if (docType.equals("invoice")) {
        options.setVerticalAlignment(VerticalAlignment.Top);
        // Invoice-specific settings
    }
    return options;
}
```
```java
List<DigitalSignature> existingSignatures = signature.search(DigitalSignature.class);
if (!existingSignatures.isEmpty()) {
    System.out.println("Document already signed by: " + 
        existingSignatures.get(0).getContactInfo());
}
```

## Related Tutorials

- [Java 中的数字签名 - 证书加载与文档签名完整指南](/signature/java/digital-signatures/digital-signature-loading-signing-groupdocs-java/)
- [如何在 Java 中验证数字证书 - 包含代码示例的完整指南](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Java 文档签名教程 - 添加文本签名并处理事件](/signature/java/event-handling/java-text-signing-groupdocs-signature-event-handling/)