---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 的二维码加密和数字签名来保护 PDF 文档。有效增强文档安全性。"
"title": "使用 GroupDocs.Signature 在 Java 中实现带有二维码加密的安全 PDF 签名"
"url": "/zh/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
type: docs
---
# 如何使用 GroupDocs.Signature 在 Java 中实现带有二维码加密的安全 PDF 签名

在当今的数字时代，保护文档中的敏感信息至关重要。网络威胁的兴起使得数据加密成为文档管理的重要组成部分。本教程将指导您使用 GroupDocs.Signature for Java 实现安全的 PDF 签名，并使用二维码加密。学完本文后，您将能够将强大的安全功能集成到您的应用程序中。

## 您将学到什么：
- 理解 Java 中的对称数据加密
- 创建自定义签名类
- 使用自定义数据和对齐方式配置二维码签名
- 集成 GroupDocs.Signature 实现安全的 PDF 签名

准备好了吗？让我们开始吧！

## 先决条件
在开始之前，请确保您具备以下条件：
- **Java 开发工具包 (JDK)：** 版本 8 或更高版本。
- **Maven 或 Gradle：** 用于依赖管理。请根据您的项目设置进行选择。
- **Java编程知识：** 对 Java 面向对象编程有基本的了解。

## 为 Java 设置 GroupDocs.Signature
要开始使用 GroupDocs.Signature，您需要将其添加为项目的依赖项。该库提供了用于管理数字签名和文档加密的强大工具。

### Maven 设置
将以下依赖项添加到您的 `pom.xml` 文件：
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 设置
对于 Gradle 用户，将其包含在您的 `build.gradle` 文件：
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下载
或者，从下载最新版本 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 许可证获取
您可以先免费试用 GroupDocs.Signature 来评估其功能。如需长期使用，请考虑购买许可证或通过其网站申请临时许可证。

## 实施指南
本指南分为几个主要部分，涵盖数据加密、自定义签名创建和二维码签名配置。

### 对称算法数据加密
加密数据可确保其在传输和存储过程中的安全。以下是使用 GroupDocs.Signature 设置对称加密的方法：

#### 设置对称加密
1. **导入必要的包：**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **初始化加密对象：**
   使用安全密钥和盐进行加密。替换 `"YOUR_SECURE_KEY"` 使用您自己的钥匙。
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **对称算法类型.Rijndael：** 这指定了要使用的对称算法的类型。
   - **密钥和盐：** 确保这些对于您的应用程序来说是唯一的和安全的。

### 自定义数据签名类
创建自定义类可以让你有效地管理签名属性。具体方法如下：

#### 定义 `DocumentSignatureData` 班级
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **ID、作者、签名：** 这些字段存储签名的元数据。
- **数据因素：** 保存与应用程序逻辑相关的数值。

### QR码签名选项
二维码提供了一种紧凑的信息嵌入方式。您可以使用自定义数据和加密方式进行配置：

#### 设置二维码签名
1. **初始化 `Signature` 目的：**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **配置二维码选项：**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // 使用加密对象
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **编码类型：** 指定二维码格式。
   - **对齐和边距：** 自定义二维码在文档上的显示方式。

### 示例用法
要使用您配置的选项签署文档：
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\