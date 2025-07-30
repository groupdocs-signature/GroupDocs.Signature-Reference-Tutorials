---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature 在 Java 中实现和验证二维码签名，从而增强文档安全性。请按照本分步指南，了解如何安全签名。"
"title": "保护您的文档 &#58; 使用 GroupDocs.Signature 在 Java 中实现二维码签名"
"url": "/zh/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
---

# 保护您的文档：使用 GroupDocs.Signature 在 Java 中实现二维码签名

在当今的数字环境中，确保合同、发票或敏感个人信息等文档的安全至关重要。增强文档安全性并简化验证流程的一种创新方法是使用二维码签名。本教程将指导您使用 GroupDocs.Signature 在 Java 中为文档实现和验证二维码签名。

## 您将学到什么
- 如何使用二维码签署文件
- 使用二维码验证已签名的文件
- 在文档中搜索现有的二维码签名
- 更新和删除文档中的二维码签名

让我们设置您的环境并开始吧！

### 先决条件
开始之前，请确保您满足以下先决条件：

#### 所需的库和依赖项
您需要 GroupDocs.Signature for Java。您可以通过 Maven 或 Gradle 将其添加，或者直接下载。

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

**直接下载**
从下载最新版本 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

#### 环境设置要求
- 确保您已安装 Java 开发工具包 (JDK) 8 或更高版本。
- 使用 IntelliJ IDEA、Eclipse 或 NetBeans 等 IDE。

#### 知识前提
对 Java 编程和文档处理有基本的了解是有益的。

## 为 Java 设置 GroupDocs.Signature
要在您的项目中使用 GroupDocs.Signature，请按照以下步骤操作：
1. **安装**：根据您的设置在 Maven、Gradle 或直接下载之间进行选择。
2. **许可证获取**：
   - 从免费试用开始 [GroupDocs 网站](https://releases。groupdocs.com/signature/java/).
   - 考虑从以下机构获取临时许可证，以进行扩展测试和开发： [这里](https://purchase。groupdocs.com/temporary-license/).
3. **基本初始化**： 
    初始化 GroupDocs.Signature 的方法如下：

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

这为您实施二维码签名做好了准备。

## 实施指南

### 使用二维码签名签署文件
#### 概述
使用二维码签署文档需要嵌入一个代表您数字签名的唯一代码。此过程可确保文档安全，并方便日后验证其真实性。

##### 步骤 1：设置您的签名选项
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

Signature signature = new Signature("YOUR_DOCUMENT_PATH");
QrCodeSignOptions signOptions = new QrCodeSignOptions("John Smith", com.groupdocs.signature.domain.qrcodes.QrCodeTypes.QR);

signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
```
**解释**： `QrCodeSignOptions` 配置为创建具有特定文本和对齐方式的二维码。根据需要调整宽度和高度。

##### 步骤 2：自定义签名外观
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // 设置二维码颜色
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**解释**：自定义字体和颜色可增强视觉识别。

##### 步骤3：签署文件
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**解释**：此步骤对文档进行签名并存储签名 ID 以供将来参考。

### 使用二维码签名验证文档
#### 概述
验证可确保文档已合法签名。以下是如何验证文档中二维码签名的方法。

##### 步骤 1：设置验证选项
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // 短信验证
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**解释**：验证选项指定要查找的二维码类型和文本，确保签名符合您的期望。

##### 第 2 步：执行验证
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**解释**：这将检查文档是否包含符合您条件的有效二维码。

### 搜索文档中的二维码签名
#### 概述
有时需要在文档中查找现有签名。以下是使用 GroupDocs.Signature 搜索签名的方法。

##### 步骤 1：配置搜索选项
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**解释**：这将设置工具来扫描所有页面上的二维码签名。

##### 第 2 步：执行搜索
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**解释**：这将检索文档中找到的所有二维码签名。

### 更新文档二维码签名
#### 概述
更新签名涉及更改其属性，例如位置或大小。操作方法如下：

##### 步骤 1：准备更新签名
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// 假设“签名”是通过搜索获得的 QrCodeSignature 对象列表
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**解释**：调整每个签名的位置和大小。

##### 第 2 步：更新文档
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**解释**：文档已使用修改后的二维码签名进行更新。

### 删除文档二维码按ID签名
#### 概述
如果签名不再需要或错误添加，则可能需要删除该签名。您可以使用其唯一 ID 将其删除，具体方法如下。

##### 步骤 1：识别要删除的签名
```java
import com.groupdocs.signature.domain.SignatureCollection;
import java.util.Arrays;

SignatureCollection signaturesToDelete = signature2.search(QrCodeSignature.class);
Arrays.stream(signaturesToDelete).forEach(signature -> {
    if (signature.getSignatureId().equals("YOUR_SIGNATURE_ID")) {
        signature.delete();
    }
});
```
**解释**：通过其唯一 ID 查找并删除二维码签名。

## 结论
本指南已引导您使用 GroupDocs.Signature 在 Java 中使用二维码签名来保护文档安全。遵循这些步骤，您可以确保文档安全签名，并轻松验证其真实性。