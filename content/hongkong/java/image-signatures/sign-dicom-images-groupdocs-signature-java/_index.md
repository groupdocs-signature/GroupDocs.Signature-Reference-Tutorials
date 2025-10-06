---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 安全地簽署 DICOM 映像。透過嵌入二維碼和元資料來增強文件安全性。"
"title": "使用 GroupDocs.Signature for Java 對具有二維碼和元資料的 DICOM 影像進行簽名"
"url": "/zh-hant/java/image-signatures/sign-dicom-images-groupdocs-signature-java/"
"weight": 1
type: docs
---
# 如何使用 GroupDocs.Signature for Java 對具有二維碼和元資料的 DICOM 影像進行簽名

## 介紹

在快速發展的數位醫療領域，安全地管理病患資料至關重要。本教學將指導您使用 GroupDocs.Signature for Java 實現一個強大的解決方案，使用二維碼和元資料對醫學數位成像和通訊 (DICOM) 影像進行簽署。這些功能透過將重要資訊直接嵌入醫學影像中，確保了真實性、增強了可追溯性並保持了合規性。

### 您將學到什麼：
- 如何將 GroupDocs.Signature for Java 整合到您的專案中。
- 使用二維碼簽署 DICOM 影像的過程。
- 新增 XMP 元資料以增強文件安全性。
- 檢索、驗證和搜尋 DICOM 檔案中的簽名。
- 產生已簽署的 DICOM 影像的預覽。

讓我們開始吧！在開始之前，請確保您已準備好一切所需，以便順利完成學習。

## 先決條件

為了有效實現 GroupDocs.Signature 功能，請確保滿足以下先決條件：

### 所需的庫和依賴項
- **GroupDocs.Signature for Java**：您需要此庫的 23.12 或更高版本。

### 環境設定要求
- **Java 開發工具包 (JDK)**：請確保您的系統上安裝了 JDK。
- **整合開發環境**：使用整合開發環境，如 IntelliJ IDEA 或 Eclipse。

### 知識前提
基本了解：
- Java程式設計和物件導向原理。
- Maven 或 Gradle 建置工具用於依賴管理。

## 為 Java 設定 GroupDocs.Signature

要開始使用 GroupDocs.Signature，您需要將其新增為專案的依賴項。以下是使用不同建置工具執行此操作的方法：

### Maven
將以下程式碼片段新增至您的 `pom.xml` 文件：
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
將其包含在您的 `build.gradle` 文件：
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下載
或者，您可以從 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

#### 許可證取得步驟
1. **免費試用**：透過限時免費試用來測試其功能。
2. **臨時執照**：取得臨時許可證以探索全部功能。
3. **購買**：如果您需要長期訪問，請購買訂閱。

#### 基本初始化和設定

若要初始化 GroupDocs.Signature，請建立一個實例 `Signature` 班級：
```java
import com.groupdocs.signature.Signature;

// 使用 DICOM 檔案的路徑初始化簽名對象
Signature signature = new Signature(filePath);
```

## 實施指南

### 使用二維碼和元資料對 DICOM 影像進行簽名

#### 概述
此功能可讓您使用二維碼簽署 DICOM 影像並新增 XMP 元數據，從而增強文件安全性。

#### 步驟 1：設定二維碼簽名選項
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
在這裡，我們配置二維碼在 DICOM 影像上的外觀和位置。

#### 步驟 2：新增 XMP 元數據
```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomSaveOptions;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpEntry;
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.DicomXmpType;

DicomSaveOptions dicomSaveOptions = new DicomSaveOptions();
List<DicomXmpEntry> xmpEntries = new ArrayList<>();
xmpEntries.add(new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4"));
dicomSaveOptions.setXmpEntries(xmpEntries);
```
此程式碼片段將元資料新增至 DICOM 文件，嵌入額外的病患資訊。

#### 步驟3：簽署文件
```java
String outputFilePath = YOUR_OUTPUT_DIRECTORY + "/SignDicomImageAdvanced/" + fileName;
signature.sign(outputFilePath, options, dicomSaveOptions);
```
這 `sign` 方法將二維碼和元資料寫入您的 DICOM 文件，並將其儲存到指定位置。

### 檢索已簽署的 DICOM 影像資訊

#### 概述
從已簽署的 DICOM 影像中提取 XMP 元資料以用於驗證或稽核目的。
```java
import com.groupdocs.signature.domain.IDocumentInfo;
import com.groupdocs.signature.domain.signatures.MetadataSignature;

IDocumentInfo documentInfo = signature.getDocumentInfo();
for (MetadataSignature item : documentInfo.getMetadataSignatures()) {
    System.out.println(item.toString());
}
```
此程式碼檢索並列印與 DICOM 檔案相關的所有元資料簽章。

### 驗證已簽署的 DICOM

#### 概述
驗證簽署的 DICOM 影像中是否存在二維碼簽名以確認其真實性。
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
此驗證步驟可確保二維碼符合預期標準，從而確認文件的完整性。

### 在簽署的 DICOM 中搜尋簽名

#### 概述
找到簽署的 DICOM 影像中的所有二維碼簽名以進行審查或審核。
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
此功能可用於掃描文件中的所有二維碼簽名，提供全面的可視性。

### 產生簽名 DICOM 的預覽

#### 概述
為簽署的 DICOM 影像的每一頁建立預覽，無需開啟整個文件即可進行快速目視檢查。
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
此程式碼片段為每個頁面產生圖像預覽，這對於快速驗證或共享很有用。

## 實際應用

GroupDocs.Signature for Java 提供了幾個實際應用程式：
- **醫學影像**：使用二維碼和元資料安全地簽署和管理病患 DICOM 影像。
- **法律文件管理**：提高法律訴訟中的文件真實性和合規性。
- **金融服務**：在敏感的財務文件上實施安全電子簽名。