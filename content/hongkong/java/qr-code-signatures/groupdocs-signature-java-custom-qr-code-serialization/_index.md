---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 在 PDF 中實作自訂二維碼序列化和加密。高效保護您的文件安全。"
"title": "使用 GroupDocs.Signature for Java 在 PDF 中實作自訂二維碼序列化和加密"
"url": "/zh-hant/java/qr-code-signatures/groupdocs-signature-java-custom-qr-code-serialization/"
"weight": 1
---

# 如何使用 GroupDocs.Signature for Java 在 PDF 中實現自訂二維碼序列化和加密

## 介紹

在數位時代，安全的文件簽章對於維護資料完整性和真實性至關重要。 GroupDocs.Signature for Java 是一個功能強大的函式庫，旨在簡化文件簽章的新增。本教學將指導您使用 GroupDocs.Signature for Java 在 PDF 中實作自訂二維碼序列化和加密。

**您將學到什麼：**
- 如何設定和配置 Java 版 GroupDocs.Signature
- 實現二維碼簽名的自訂序列化
- 加密二維碼內的序列化數據
- 應用這些功能來保護您的文檔

在深入實施之前，讓我們確保您已準備好後續的一切。

### 先決條件

為了有效使用本教程，請確保滿足以下先決條件：

1. **所需的庫和相依性：**
   - GroupDocs.Signature for Java 版本 23.12 或更高版本
   - Maven 或 Gradle 用於依賴管理（可選）

2. **環境設定要求：**
   - 您的機器上安裝了 Java 開發工具包 (JDK)
   - 對 Java 程式設計有基本的了解

3. **知識前提：**
   - 熟悉 Java 和物件導向程式設計概念
   - 使用 Java 處理 PDF 的基礎知識

## 為 Java 設定 GroupDocs.Signature

首先，您需要在專案環境中設定 GroupDocs.Signature 庫。

### Maven 安裝

如果您使用 Maven，請將以下依賴項新增至您的 `pom.xml` 文件：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 安裝

對於 Gradle 用戶，請在您的 `build.gradle` 文件：

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下載

或者，您可以直接從 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

#### 許可證取得步驟
- **免費試用：** 首先下載試用版來測試其功能。
- **臨時執照：** 如果需要，您可以申請臨時許可證，這樣您就可以不受任何限制地評估產品。
- **購買：** 為了長期使用，請考慮購買完整許可證。

安裝後，在您的專案中初始化 GroupDocs.Signature：

```java
import com.groupdocs.signature.Signature;

public class SetupGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        // 您的程式碼在這裡...
    }
}
```

## 實施指南

現在，讓我們深入研究使用 GroupDocs.Signature for Java 實作自訂二維碼序列化和加密。

### 二維碼簽名的自訂序列化類

#### 概述

此功能涉及建立一個類，用於將元資料序列化為二維碼簽章。 `DocumentSignatureData` 類別儲存ID、作者、簽名日期、資料因素等屬性。

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID;

    public void setID(String value) { 
        this.ID = value; 
    }

    @FormatAttribute(propertyName = "SAuth")
    public String author;

    public void setAuthor(String value) {
        this.author = value;
    }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public Date signed = new Date();

    public void setSigned(Date value) {
        this.signed = value;
    }

    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public BigDecimal dataFactor = new BigDecimal(0.01);

    public void setDataFactor(BigDecimal value) {
        this.dataFactor = value;
    }
}
```

#### 解釋
- **屬性：** 這 `@FormatAttribute` 註解指定如何將每個屬性序列化到二維碼中。
  - **ID**：簽名的唯一識別碼。
  - **作者**：簽署文件的人。
  - **簽署日期**：文件簽署的時間戳記。
  - **數據因素**：與簽名相關的附加數位資料。

### 具有自訂資料序列化和加密的二維碼簽名

#### 概述

本節示範如何使用包含自訂序列化資料和加密的二維碼簽署文件。

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import java.io.File;
import java.math.BigDecimal;
import java.util.Date;
import java.util.UUID;

class SignWithQRCodeCustomSerialization {
    String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf"; 
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedQRCodeCustomSerialization.pdf").getPath();

    public void signDocument() throws Exception {
        Signature signature = new Signature(filePath);

        // 在這裡實現您的自訂加密邏輯
        IDataEncryption encryption = new CustomXOREncryption();

        DocumentSignatureData documentSignature = new DocumentSignatureData();
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME")); 
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        QrCodeSignOptions options = new QrCodeSignOptions();
        options.setData(documentSignature);
        options.setEncodeType(QrCodeTypes.QR);
        options.setDataEncryption(encryption);

        // 配置對齊和外觀
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        Padding padding = new Padding();
        padding.setRight(10);
        padding.setBottom(10);
        options.setMargin(padding);

        signature.sign(outputFilePath, options);
    }
}
```

#### 解釋
- **自訂加密：** 實現您自己的加密邏輯 `CustomXOREncryption` 或使用任何其他方法實現 `IDataEncryption`。
- **簽名選項：** 使用高度、寬度、填滿等選項來配置二維碼的外觀和對齊方式。
- **簽約流程：** 這 `signature.sign()` 方法將二維碼簽名套用至文件。

### 故障排除提示

- 確保在建置工具（Maven/Gradle）中正確配置所有相依性。
- 驗證輸入和輸出文件的文件路徑是否準確。
- 確認您的自訂加密邏輯已正確實現和整合。

## 實際應用

以下是此功能的一些實際應用：

1. **法律文件簽署：** 使用嵌入二維碼的元資料安全地簽署合同，以確保真實性。
2. **發票處理：** 自動向發票新增加密簽名，以增加安全性和可追溯性。
3. **物流追蹤：** 使用簽名文件進行貨運追踪，在二維碼中嵌入唯一識別碼和時間戳記。
4. **學術認證：** 使用二維碼簽名將學生資訊安全地嵌入到數位證書中