---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature 实现 Java 二维码签名。增强文档安全性、配置签名选项并在 Java 应用程序中应用自定义加密。"
"title": "Java QR 码签名指南 &#58; 使用 GroupDocs.Signature 保护您的文档"
"url": "/zh/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature for Java 实现 Java QR 码签名

## 介绍

通过在 Java 应用程序中嵌入二维码，增强数字文档的安全性。利用 GroupDocs.Signature for Java，您可以有效地确保文档的真实性和可追溯性。本指南将指导您创建自定义数据签名、配置二维码签名选项，并使用强大的加密技术保护您的文档。

**您将学到什么：**
- 如何使用 GroupDocs.Signature 创建自定义数据签名类
- 在 Java 应用程序中配置二维码签名选项
- 使用二维码签署文档并应用自定义加密

让我们深入了解先决条件并开始将此功能集成到您的项目中！

## 先决条件

在开始之前，请确保您已经在开发环境中设置了必要的库和依赖项。

### 所需的库和版本

要为 Java 实现 GroupDocs.Signature，请包含以下依赖项：

**Maven**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle**
```gradle
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

您也可以直接从 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 环境设置要求

- 确保您已安装可运行的 Java 开发工具包 (JDK)。
- 设置您的集成开发环境 (IDE)，例如 IntelliJ IDEA 或 Eclipse。

### 知识前提

- 对 Java 编程和面向对象概念有基本的了解。
- 熟悉使用 Maven 或 Gradle 处理依赖项。

## 为 Java 设置 GroupDocs.Signature

首先，按照上面的安装说明在您的项目中设置 GroupDocs.Signature，并将其包含在您的构建配置中。

### 许可证获取步骤

GroupDocs 提供不同的许可选项：
- **免费试用**：无限制测试所有功能。
- **临时执照**：获取用于评估目的的许可证。
- **购买**：获得商业使用的完整许可。

下载后，像这样初始化 GroupDocs.Signature：

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // 您现在可以开始使用签名对象来处理文档。
    }
}
```

## 实施指南

让我们将实施过程分解为易于管理的部分，重点关注关键特性。

### 自定义数据签名类

#### 概述
创建一个自定义类来存储签名数据，例如 ID、作者、签名日期和其他因素。这可确保您的签名中封装了所有必要的元数据。

#### 逐步实施

**定义 DocumentSignatureData 类**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // 签名的唯一标识符
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // 文档的作者
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // 签署日期和时间
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // 签名的附加数据因素
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**解释：**
- **格式属性**：注释属性以自定义序列化。
- **特性**：捕获必要的详细信息，例如唯一 ID、作者姓名、签名日期和数据因素。

### QR 码签名选项配置

#### 概述
配置二维码签名选项来定义二维码在文档上的显示方式，包括大小、对齐方式和填充。

#### 逐步实施

**定义 QrCodeSignOptionsConfig 类**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // 将自定义数据对象序列化为二维码
        options.setData(documentSignature);
        
        // 指定二维码类型
        options.setEncodeType(QrCodeTypes.QR);
        
        // 配置对齐的填充
        Padding padding = new Padding();
        padding.setRight(10); // 右填充（以像素为单位）
        padding.setBottom(10); // 底部填充（以像素为单位）
        options.setMargin(padding);
        
        // 定义二维码的大小和位置
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**解释：**
- **QrCodeSignOptions**：管理二维码的显示方式，包括其大小和位置。
- **填充**：调整文档内的对齐方式。

### 使用二维码和自定义加密进行文档签名

#### 概述
结合二维码和自定义加密技术，安全地签署文档。这确保了数据的完整性和保密性。

#### 逐步实施

**使用二维码签署文件**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // 自定义XOR加密策略
            IDataEncryption encryption = new CustomXOREncryption();

            // 配置自定义文档签名数据对象
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // 设置二维码选项
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // 对二维码内的数据进行加密
            options.setDataEncryption(encryption);

            // 签署并保存文件
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**解释：**
- **自定义异或加密**：实施自定义加密策略来保护二维码数据。
- **唯一标识符**：为每个签名生成一个唯一的标识符。