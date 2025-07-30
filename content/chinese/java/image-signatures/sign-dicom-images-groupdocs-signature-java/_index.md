---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 安全地签署 DICOM 图像。通过嵌入二维码和元数据来增强文档安全性。"
"title": "使用 GroupDocs.Signature for Java 对带有二维码和元数据的 DICOM 图像进行签名"
"url": "/zh/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
---

# 如何使用 GroupDocs.Signature for Java 对带有二维码和元数据的 DICOM 图像进行签名

## 介绍

在快速发展的数字医疗领域，安全地管理患者数据至关重要。本教程将指导您使用 GroupDocs.Signature for Java 实现一个强大的解决方案，使用二维码和元数据对医学数字成像和通信 (DICOM) 图像进行签名。这些功能通过将重要信息直接嵌入医学图像中，确保了真实性、增强了可追溯性并保持了合规性。

### 您将学到什么：
- 如何将 GroupDocs.Signature for Java 集成到您的项目中。
- 使用二维码签署 DICOM 图像的过程。
- 添加 XMP 元数据以增强文档安全性。
- 检索、验证和搜索 DICOM 文件中的签名。
- 生成已签名的 DICOM 图像的预览。

让我们开始吧！在开始之前，请确保您已准备好一切所需，以便顺利完成学习。

## 先决条件

为了有效实现 GroupDocs.Signature 功能，请确保满足以下先决条件：

### 所需的库和依赖项
- **GroupDocs.Signature for Java**：您需要此库的 23.12 或更高版本。

### 环境设置要求
- **Java 开发工具包 (JDK)**：确保您的系统上安装了 JDK。
- **集成开发环境**：使用集成开发环境，如 IntelliJ IDEA 或 Eclipse。

### 知识前提
基本了解：
- Java编程和面向对象原理。
- Maven 或 Gradle 构建工具用于依赖管理。

## 为 Java 设置 GroupDocs.Signature

要开始使用 GroupDocs.Signature，您需要将其添加为项目的依赖项。以下是使用不同构建工具执行此操作的方法：

### Maven
将以下代码片段添加到您的 `pom.xml` 文件：
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
将其包含在您的 `build.gradle` 文件：
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下载
或者，您可以从 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

#### 许可证获取步骤
1. **免费试用**：通过限时免费试用来测试其功能。
2. **临时执照**：获取临时许可证以探索全部功能。
3. **购买**：如果您需要长期访问，请购买订阅。

#### 基本初始化和设置

要初始化 GroupDocs.Signature，请创建一个实例 `Signature` 班级：
```java
import com.groupdocs.signature.Signature;

// 使用 DICOM 文件的路径初始化签名对象
Signature signature = new Signature(filePath);
```

## 实施指南

### 使用二维码和元数据对 DICOM 图像进行签名

#### 概述
此功能允许您使用二维码签署 DICOM 图像并添加 XMP 元数据，从而增强文档安全性。

#### 步骤 1：设置二维码签名选项
```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.signatures.QrCodeSignOptions;

Padding padding = new Padding();
padding.setRight(5);
padding.setLeft(5);

QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues");
options.setAllPages(true);
options.setWidth(100);
options.setHeight(100);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setMargin(padding);
```
在这里，我们配置二维码在 DICOM 图像上的外观和位置。

#### 步骤 2：添加 XMP 元数据
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
此代码片段将元数据添加到 DICOM 文件，嵌入额外的患者信息。

#### 步骤3：签署文件
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
这 `sign` 方法将二维码和元数据写入您的 DICOM 文件，并将其保存到指定位置。

### 检索已签名的 DICOM 图像信息

#### 概述
从签名的 DICOM 图像中提取 XMP 元数据以用于验证或审计目的。
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
此代码检索并打印与 DICOM 文件相关的所有元数据签名。

### 验证已签名的 DICOM

#### 概述
验证签名的 DICOM 图像中是否存在二维码签名以确认其真实性。
```java
import com.groupdocs.signature.domain.VerificationResult;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;
import com.groupdocs.signature.domain.enums.TextMatchType;

QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();
verifyOptions.setAllPages(true);
verifyOptions.setText("Patient #36363393");
verifyOptions.setMatchType(TextMatchType.Contains);

VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    System.out.println(filePath + " has successfully verified signatures!");
} else {
    System.out.println(filePath + " failed verification process.");
}
```
此验证步骤可确保二维码符合预期标准，从而确认文档的完整性。

### 在签名的 DICOM 中搜索签名

#### 概述
找到签名的 DICOM 图像中的所有二维码签名以进行审查或审核。
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.util.List;

List<QrCodeSignature> signatures = signature.search(QrCodeSignature.class);
for (QrCodeSignature qrCodeSignature : signatures) {
    System.out.println("QRCode signature found at page " +
        qrCodeSignature.getPageNumber() + ": " +
        qrCodeSignature.getEncodeType().getTypeName() + ": " +
        qrCodeSignature.getText());
}
```
此功能可用于扫描文档中的所有二维码签名，提供全面的可视性。

### 生成签名 DICOM 的预览

#### 概述
为签名的 DICOM 图像的每一页创建预览，无需打开整个文件即可进行快速目视检查。
```java
import com.groupdocs.signature.options.PreviewOptions;
import java.io.File;
import java.io.FileOutputStream;
import java.nio.file.Paths;

PreviewOptions previewOption = new PreviewOptions(pageNumber -> {
    try {
        String pageFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/image-" + pageNumber + ".jpg";
        return new FileOutputStream(Paths.get(pageFilePath).toFile());
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
});

signature.generatePreview(previewOption);
```
此代码片段为每个页面生成图像预览，这对于快速验证或共享很有用。

## 实际应用

GroupDocs.Signature for Java 提供了几个实际应用程序：
- **医学成像**：使用二维码和元数据安全地签署和管理患者 DICOM 图像。
- **法律文件管理**：提高法律诉讼中的文件真实性和合规性。
- **金融服务**：在敏感的财务文件上实施安全电子签名。