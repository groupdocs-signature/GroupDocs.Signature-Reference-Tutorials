---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 安全地对包含 HIBC 数据编码的二维码文档进行签名。立即简化您的文档管理流程。"
"title": "使用 GroupDocs.Signature for Java 实现二维码文档签名的综合指南"
"url": "/zh/java/qr-code-signatures/groupdocs-signature-qr-code-document-signing/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature for Java 实现主文档二维码签名

## 介绍

在数字时代，高效管理和保护药品数据对于合规性和运营效率至关重要。将全面的产品信息集成到文档中可能颇具挑战性。本教程演示了如何使用 **GroupDocs.Signature for Java** 在二维码中编码健康产业条形码 (HIBC) 数据并无缝签署文件。

### 您将学到什么：
- 为 Java 设置 GroupDocs.Signature。
- 创建 HIBCLICPrimaryData、HIBCLICSecondaryAdditionalData 及其组合形式的实例。
- 使用编码详细产品信息的二维码签署文件。
- 在有效管理资源的同时优化性能。

## 先决条件

### 所需的库和依赖项
要使用 GroupDocs.Signature for Java，请确保您已具备：
- **Java 开发工具包 (JDK)**：版本 8 或更高版本。
- **Maven** 或者 **Gradle**：用于依赖管理。

### 环境设置要求
确保您的开发环境配置为使用 Maven 或 Gradle，从而简化依赖关系和项目构建管理。

### 知识前提
熟悉 Java 编程将有助于理解代码片段和实现细节。

## 为 Java 设置 GroupDocs.Signature

### 安装信息

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
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**直接下载**：从下载最新版本 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 许可证获取步骤
1. **免费试用**：首先下载试用版来测试基本功能。
2. **临时执照**：在评估期间，您可以不受限制地获得完全访问权限。
3. **购买**：考虑购买长期项目的许可证。

#### 基本初始化和设置
安装完成后，初始化 `Signature` 对象与您想要签署的文档的文件路径：
```java
String filePath = "Sample.pdf";
Signature signature = new Signature(filePath);
```

## 实施指南

### 创建 HIBC LIC 原始数据
**概述**：本节演示如何创建和配置 `HIBCLICPrimaryData`，其中包含重要的产品信息。

#### 步骤 1：初始化主数据对象
```java
HIBCLICPrimaryData primaryData = new HIBCLICPrimaryData();
```

#### 步骤 2：设置基本属性
- **产品或目录编号**：产品的唯一标识符。
- **标签识别码**：标识制造商。
- **计量单位 ID**：指定测量单位。

```java
primaryData.setProductOrCatalogNumber("12345");
primaryData.setLabelerIdentificationCode("A999");
primaryData.setUnitOfMeasureID(1);
```

### 创建 HIBC LIC 辅助附加数据
**概述**：本节介绍创建和配置 `HIBCLICSecondaryAdditionalData`，其中包括有效期和批号等其他详细信息。

#### 步骤 1：初始化辅助数据对象
```java
HIBCLICSecondaryAdditionalData secondaryData = new HIBCLICSecondaryAdditionalData();
```

#### 步骤 2：设置其他属性
- **到期日**：使用当前日期进行演示。
- **数量、批号、序列号**：定义产品细节。
- **生产日期和链接字符**：建立制造细节。

```java
secondaryData.setExpiryDate(new Date());
secondaryData.setExpiryDateFormat(HIBCLICDateFormat.MMDDYY);
secondaryData.setQuantity(30);
secondaryData.setLotNumber("LOT123");
secondaryData.setSerialNumber("SERIAL123");
secondaryData.setDateOfManufacture(new Date());
secondaryData.setLinkCharacter('S');
```

### 结合 HIBC LIC 的主要数据和次要数据
**概述**：了解如何将主要数据和次要数据合并为一个 `HIBCLICCombinedData` 对象进行流水线化处理。

#### 步骤 1：初始化组合数据对象
```java
HIBCLICCombinedData combinedData = new HIBCLICCombinedData();
```

#### 步骤2：设置主要数据和次要数据
- 将两个数据集链接起来以形成完整的数据结构。

```java
combinedData.setPrimaryData(primaryData);
combinedData.setSecondaryAdditionalData(secondaryData);
```

### 使用包含 HIBC LIC 组合数据的二维码签署文件
**概述**：最后一部分演示了如何使用对组合的 HIBC 数据进行编码的二维码来签署文档。

#### 步骤 1：定义文件路径
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/Sample.pdf";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithQRCodeHIBCLICCombinedData/" + fileName;
```

#### 步骤 2：设置二维码签名选项
- **编码类型**： 使用 `QrCodeTypes.HIBCLICQR` 指定编码类型。
- **数据分配**：传递组合数据以包含在二维码中。

```java
Signature signature = new Signature(filePath);
try {
    QrCodeSignOptions options = new QrCodeSignOptions();
    options.setEncodeType(QrCodeTypes.HIBCLICQR);
    options.setData(combinedData);

    // 签署并保存文件
    signature.sign(outputFilePath, options);
} finally {
    if (signature != null) signature.dispose();
}
```

## 实际应用
1. **药品合规性**：通过这种集成简化对监管标准的遵守。
2. **供应链管理**：通过文件中的二维码增强药品的可追溯性。
3. **医疗保健系统集成**：在医疗记录中嵌入全面的产品数据，以提高患者的安全性。

## 性能考虑
- **优化资源使用**：通过处理 `Signature` 对象后操作。
- **最佳实践**：定期更新到最新的 GroupDocs.Signature 版本以提高性能并修复错误。

## 结论
通过本指南，您学习了如何创建 HIBC LIC 主数据对象和次数据对象，将它们合并为一个实体，以及如何使用 GroupDocs.Signature for Java 为文档签名二维码。这些技能可以增强文档安全性，并确保制药行业的合规性。

### 后续步骤
- 探索 GroupDocs.Signature 的其他功能。
- 将此解决方案集成到您现有的系统中，以自动化文档签名流程。

## 常见问题解答部分
1. **什么是 HIBC 数据？**
   - 健康产业条形码 (HIBC) 数据包含医疗保健和制药行业使用的重要产品信息。
2. **我可以将 GroupDocs.Signature 用于其他类型的条形码吗？**
   - 是的，GroupDocs.Signature 除了支持二维码之外，还支持多种条形码格式。
3. **如果我的文档格式不是 PDF 怎么办？**
   - GroupDocs.Signature 支持多种文档格式，包括 Word 和 Excel。
4. **签名过程中出现异常如何处理？**
   - 实现 try-catch 块以有效管理异常并确保资源清理。
5. **每份文件的二维码数量有限制吗？**
   - 没有固有的限制；但是，添加大量代码时要考虑性能影响。

## 资源
- **文档**： [Java 文档的 GroupDocs.Signature](https://docs.groupdocs.com/signature/java/)
- **API 参考**： [GroupDocs API 参考](https://reference.groupdocs.com/signature/java/)
- **下载**： [最新 GroupDocs.Releases](https://releases.groupdocs.com/signature/java/)
- **购买**： [购买许可证](https://purchase.groupdocs.com/buy)
- **免费试用**： [免费试用](https://releases.groupdocs.com/signature/java/)
- **临时执照**： [在此申请](https://purchase.groupdocs.com/temporary-license/)