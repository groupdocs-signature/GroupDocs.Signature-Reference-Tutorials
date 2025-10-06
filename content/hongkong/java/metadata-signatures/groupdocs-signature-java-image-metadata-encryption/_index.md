---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 加密來保護映像元資料。透過逐步指導確保資料的完整性和真實性。"
"title": "使用 GroupDocs.Signature 在 Java 中實現圖像元資料簽章和加密"
"url": "/zh-hant/java/metadata-signatures/groupdocs-signature-java-image-metadata-encryption/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature 在 Java 中實現圖像元資料加密簽名

## 介紹

在當今的數位時代，保護文檔元資料中的敏感資訊至關重要。無論是機密的商業合約還是個人識別照片，維護圖像元資料的完整性和真實性有助於防止未經授權的存取和篡改。 **GroupDocs.Signature for Java** 提供了一個強大的解決方案來安全地簽署和加密影像元資料。

本教學將指導您使用 GroupDocs.Signature 的強大功能，在 Java 中實現帶有加密的圖像元資料簽章。按照以下步驟操作，您將能夠有效地將此功能整合到您的 Java 應用程式中。

**您將學到什麼：**
- 使用 GroupDocs.Signature for Java 簽署文檔元數據
- 使用加密實作自訂物件簽名
- 使用對稱金鑰加密設定安全環境

## 先決條件

在開始之前，請確保滿足以下先決條件：

### 所需的庫和相依性：
- **GroupDocs.Signature for Java**：確保您擁有 23.12 或更高版本。

### 環境設定要求：
- 在您的機器上安裝 Java 開發工具包 (JDK)。
- 使用整合開發環境 (IDE)，如 IntelliJ IDEA、Eclipse 或 NetBeans。

### 知識前提：
- 對 Java 程式設計有基本的了解。
- 熟悉 Maven 或 Gradle 的依賴管理。

## 為 Java 設定 GroupDocs.Signature

若要在您的專案中使用 GroupDocs.Signature，請包含以下必要的依賴項：

### 使用 Maven
將此添加到您的 `pom.xml` 文件：
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### 使用 Gradle
將其包含在您的 `build.gradle` 文件：
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下載
或者，從下載最新版本 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

#### 許可證取得步驟
- **免費試用**：從試用開始探索功能。
- **臨時執照**：如果需要，請申請進行全面測試。
- **購買**：從以下位置取得生產使用許可證 [群組文檔](https://purchase。groupdocs.com/buy).

## 基本初始化和設定

以下是如何在 Java 應用程式中初始化 GroupDocs.Signature：

```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) {
        // 文件路徑
        String filePath = "path/to/your/document.jpg";
        
        // 建立簽名的新實例
        Signature signature = new Signature(filePath);

        System.out.println("GroupDocs.Signature initialized successfully.");
    }
}
```

## 實施指南

### 功能：自訂物件的元資料簽名

#### 概述
此功能允許使用自訂物件簽署影像元資料並對其進行加密以增加安全性，確保只有授權方才能存取或修改元資料。

#### 逐步實施

##### 1. 定義文件簽章資料類
建立一個類別來保存您的元資料資訊：

```java
import java.math.BigDecimal;
import java.util.Date;

class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    @FormatAttribute(propertyName = "SignID")
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    @FormatAttribute(propertyName = "SAuth")
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

##### 2. 實作簽章邏輯
以下是使用加密對元資料進行簽署的方法：

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.domain.signatures.metadata.ImageMetadataSignature;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithCustomObject {
    // 使用佔位符初始化檔案路徑
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithCustomMetadata/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // 設定加密的金鑰和密碼
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // 設定自訂元資料屬性
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // 為選項新增元資料簽名
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```

#### 關鍵配置選項
- **對稱加密**：利用Rijndael演算法進行加密。
- **元資料簽章選項**：配置簽名過程並指定要簽署的元資料。

##### 故障排除提示
- 確保您的文件路徑正確且可存取。
- 檢查環境變數 `USERNAME` 是否設定正確。
- 驗證 GroupDocs.Signature 庫版本是否與您的程式碼依賴項相符。

### 功能：帶有加密的元資料簽名

#### 概述
此功能專注於加密元資料簽章以保護影像檔案中的敏感資訊。

#### 逐步實施
##### 1.實現加密邏輯
以下是使用加密對元資料進行簽署的方法：
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.nio.file.Paths;
import java.util.UUID;

public class SignMetadataWithEncryption {
    // 使用佔位符初始化檔案路徑
    String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", 
                                       "SignedImageWithEncryption/SampleImage_signed.jpg").getPath();

    public void run() throws Exception {
        Signature signature = new Signature(filePath);

        // 設定加密的金鑰和密碼
        String key = "1234567890";
        String salt = "1234567890";
        IDataEncryption encryption = new SymmetricEncryption(
            SymmetricAlgorithmType.Rijndael, key, salt);

        MetadataSignOptions options = new MetadataSignOptions();
        DocumentSignatureData documentSignature = new DocumentSignatureData();
        
        // 設定自訂元資料屬性
        documentSignature.setID(UUID.randomUUID().toString());
        documentSignature.setAuthor(System.getenv("USERNAME"));
        documentSignature.setSigned(new Date());
        documentSignature.setDataFactor(new BigDecimal("11.22"));

        ImageMetadataSignature mdDocument = new ImageMetadataSignature(41996, documentSignature);
        mdDocument.setDataEncryption(encryption);

        // 為選項新增元資料簽名
        options.getSignatures().add(mdDocument);

        signature.sign(outputFilePath, options);
    }
}
```