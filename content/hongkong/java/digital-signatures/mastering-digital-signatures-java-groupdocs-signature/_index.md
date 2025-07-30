---
"date": "2025-05-08"
"description": "學習如何使用 GroupDocs.Signature for Java 在 PDF 中實作數位簽章。本指南涵蓋設定、配置和實際應用，並附帶程式碼範例。"
"title": "掌握 Java 中的數位簽章－使用 GroupDocs.Signature 的綜合指南"
"url": "/zh-hant/java/digital-signatures/mastering-digital-signatures-java-groupdocs-signature/"
"weight": 1
---

# 掌握 Java 中的數位簽章：GroupDocs.Signature 綜合指南

## 介紹

在當今快節奏的數位世界中，確保文件的真實性和完整性至關重要。本教學將指導您使用 GroupDocs.Signature for Java 在 PDF 中實現高級數位簽章。無論您是開發人員還是 IT 專業人士，這份全面的指南都能幫助您簡化文件簽署流程。

**您將學到什麼：**
- 為 Java 設定 GroupDocs.Signature
- 使用憑證和自訂外觀配置數位簽章選項
- 在 PDF 中預覽和產生數位簽名
- 管理簽名影像的輸出流

在深入實施之前，讓我們先介紹一些先決條件，以確保流暢的體驗。

### 先決條件

要學習本教程，您需要：

- **Java 開發工具包 (JDK)**：確保您已安裝 JDK 8 或更高版本。
- **Maven 或 Gradle**：熟悉這些建置工具有利於管理依賴關係。
- **GroupDocs.Signature 庫**：本指南使用該程式庫的 23.12 版本。

### 為 Java 設定 GroupDocs.Signature

首先，您需要將 GroupDocs.Signature 整合到您的專案中。具體操作如下：

**Maven：**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle：**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

或者，您可以直接從 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 授權

- **免費試用**：從免費試用開始測試 GroupDocs.Signature 的功能。
- **臨時執照**：如果需要延長測試時間，請取得臨時許可證。
- **購買**：為了長期使用，請考慮購買完整許可證。

一旦程式庫設定好，您就可以開始在 Java 應用程式中初始化和配置它。

## 實施指南

### 功能：數位簽章選項

此功能可讓您配置包含憑證詳細資訊和自訂外觀的數位簽章。讓我們分解實現步驟：

#### 概述
設定數位簽章選項包括指定憑證路徑、文件類型和外觀設置，以實現個人化。

##### 步驟 1：初始化 DigitalSignOptions

首先導入必要的類別並初始化 `DigitalSignOptions` 使用您的證書路徑。

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.DocumentType;
import com.groupdocs.signature.options.sign.DigitalSignOptions;

String certificatePath = "YOUR_DOCUMENT_DIRECTORY/certificate.pfx";
DigitalSignOptions signOptions = new DigitalSignOptions(certificatePath);
```

##### 步驟2：設定證書詳細信息

配置數位證書的基本詳細信息，例如密碼、簽名原因、聯絡資訊和位置。

```java
signOptions.setDocumentType(DocumentType.Pdf);
signOptions.setPassword("1234567890");
signOptions.setReason("Approved");
signOptions.setContact("John Smith");
signOptions.setLocation("New York");
```

##### 步驟3：自訂PDF簽名外觀

使用以下方式調整數位簽章的外觀 `PdfDigitalSignatureAppearance`。

```java
import com.groupdocs.signature.options.appearances.PdfDigitalSignatureAppearance;
import java.awt.*;

PdfDigitalSignatureAppearance pdfDigSignAppearance = new PdfDigitalSignatureAppearance();
pdfDigSignAppearance.setContactInfoLabel("Contact");
pdfDigSignAppearance.setReasonLabel("R:");
pdfDigSignAppearance.setLocationLabel("@=>");
pdfDigSignAppearance.setDigitalSignedLabel("By:");
pdfDigSignAppearance.setDateSignedAtLabel("On:");
pdfDigSignAppearance.setBackground(Color.GRAY);
pdfDigSignAppearance.setFontFamilyName("Courier");
pdfDigSignAppearance.setFontSize(8);

signOptions.setAppearance(pdfDigSignAppearance);
```

##### 步驟 4：設定簽名設定

定義其他設置，如尺寸、對齊、填充和邊框屬性。

```java
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;

signOptions.setAllPages(false);
signOptions.setWidth(200);
signOptions.setHeight(130);
signOptions.setVerticalAlignment(VerticalAlignment.Center);
signOptions.setHorizontalAlignment(HorizontalAlignment.Left);

Padding padding = new Padding();
padding.setBottom(10);
padding.setRight(10);
signOptions.setMargin(padding);

import com.groupdocs.signature.domain.Border;
import com.groupdocs.signature.domain.enums.DashStyle;

Border border = new Border();
border.setVisible(true);
border.setColor(Color.DARK_GRAY);
border.setDashStyle(DashStyle.DashDot);
border.setWeight(2);
signOptions.setBorder(border);
```

### 功能：預覽簽名選項

產生並預覽數位簽名以確保它們滿足您的要求。

#### 概述
預覽簽名可讓您直觀地看到它在最終文件中的顯示效果，並根據需要進行調整。

##### 步驟 1：設定預覽簽名選項

創造 `PreviewSignatureOptions` 管理預覽過程。

```java
import com.groupdocs.signature.options.PreviewSignatureOptions;
import com.groupdocs.signature.options.preview.PreviewFormats;

PreviewSignatureOptions previewOption = new PreviewSignatureOptions(signOptions, () -> generateSignatureStream(previewOption));
previewOption.setSignatureId(UUID.randomUUID().toString());
previewOption.setPreviewFormat(PreviewFormats.JPEG);
```

##### 步驟 2：產生簽名預覽

利用 GroupDocs.Signature API 建立簽章預覽。

```java
import com.groupdocs.signature.Signature;

Signature.generateSignaturePreview(previewOption);
```

### 功能：簽名流工廠方法

管理輸出流以有效處理產生的簽名影像。

#### 概述
這些方法有助於建立和發布流，確保正確的資源管理。

##### 步驟 1：產生簽名流

定義方法來創建 `OutputStream` 用於保存簽名影像。

```java
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

private static OutputStream generateSignatureStream(PreviewSignatureOptions previewOptions) {
    try {
        Path path = Paths.get("YOUR_OUTPUT_DIRECTORY/GenerateSignaturePreviewAdvanced/");
        if (!Files.exists(path)) {
            Files.createDirectory(path);
        }
        File imageFilePath = new File(path + "/signature" + previewOptions.getSignatureId() + "-" + previewOptions.getSignOptions().getSignatureType() + ".jpg");
        return new FileOutputStream(imageFilePath);
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
}
```

##### 步驟2：發布簽名流

確保正確關閉流以釋放資源。

```java
private static void releaseSignatureStream(PreviewSignatureOptions previewOptions, OutputStream signatureStream) {
    try {
        signatureStream.close();
    } catch (Exception e) {
        throw new RuntimeException(e.getMessage());
    }
}
```

## 實際應用

以下是數位簽名可以發揮作用的一些實際場景：

1. **合約簽訂**：自動化合約和協議的簽署流程。
2. **發票審核**：使用數位簽章簡化發票審批工作流程。
3. **文件驗證**：確保敏感交易中的文件真實性。
4. **協作工具**：與 Google Workspace 或 Microsoft 365 等工具集成，實現無縫協作。
5. **法律文件**：安全地管理需要經過驗證的簽署的法律文件。

## 性能考慮

為了優化使用 GroupDocs.Signature 時的效能：

- 透過及時釋放流來有效地管理記憶體使用情況。
- 透過適當配置簽名設定來最佳化文件處理時間。
- 盡可能使用快取機制來提高重複操作的回應時間。

## 結論

本指南全面概述如何使用 GroupDocs.Signature 在 Java 中實作數位簽章。按照概述的步驟操作，您可以增強應用程式在處理文件真實性方面的安全性和效率。更多詳情，請參閱 [GroupDocs.Signature 文檔](https://docs。groupdocs.com/signature/java/).