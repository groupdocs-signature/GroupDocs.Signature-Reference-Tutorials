---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 加密和簽署文檔元數據，從而保護文檔元資料的安全。本指南涵蓋自訂資料簽章、XOR 加密以及如何將這些功能整合到您的 Java 應用程式中。"
"title": "如何使用 GroupDocs.Signature for Java 加密和簽署文檔元資料—綜合指南"
"url": "/zh-hant/java/metadata-signatures/encrypt-sign-metadata-groupdocs-java/"
"weight": 1
---

# 如何使用 GroupDocs.Signature for Java 加密和簽署文件元資料：綜合指南

## 介紹
在當今的數位時代，保護文件元資料對於維護專業環境中的機密性和真實性至關重要。無論您處理的是敏感合約還是個人數據，未經授權的存取都可能導致嚴重的安全漏洞。本教程將指導您使用 **GroupDocs.Signature for Java** 有效地加密和簽署文件元數據，增強數據保護，同時確保符合行業標準。

在本綜合指南中，我們將探討如何：
- 建立自訂資料簽章類別。
- 實施XOR加密以確保資料安全。
- 設定元資料簽章並使用 GroupDocs.Signature 將其套用至文件。

在本教程結束時，您將學會如何：
- 開發具有關鍵屬性的自訂資料簽章結構。
- 使用 XOR 演算法加密和解密文件資料。
- 將這些功能整合到您的 Java 應用程式中以保護文件元資料。

### 先決條件
在深入實施之前，請確保滿足以下先決條件：

#### 所需的庫和依賴項
- **GroupDocs.Signature for Java**：確保您已安裝 23.12 或更高版本。
- **Java 開發工具包 (JDK)**：建議使用 8 或更高版本。

#### 環境設定要求
- 合適的 IDE，例如 IntelliJ IDEA 或 Eclipse。
- 在您的專案環境中設定 Maven 或 Gradle。

#### 知識前提
- 對 Java 程式設計有基本的了解。
- 熟悉加密和數位簽章等概念。

## 為 Java 設定 GroupDocs.Signature
首先，您需要將 GroupDocs.Signature 整合到您的 Java 專案中。以下是使用不同建置工具進行安裝的步驟：

### Maven 安裝
在您的 `pom.xml` 文件：
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 安裝
將此行包含在您的 `build.gradle` 文件：
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下載
或者，您可以從 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

#### 許可證取得步驟
- **免費試用**：從試用開始來評估功能。
- **臨時執照**：獲取此文件以進行無限制的擴展測試。
- **購買**：如需長期使用，請透過以下方式購買許可證 [GroupDocs 購買頁面](https://purchase。groupdocs.com/buy).

### 基本初始化和設定
安裝後，在 Java 應用程式中初始化 GroupDocs.Signature：
```java
Signature signature = new Signature("YOUR_DOCUMENT_PATH");
```

## 實施指南
我們將把實作分解為不同的功能：自訂資料簽章類別建立、XOR 加密設定和元資料簽章。

### 特性1：自訂資料簽章類
此功能可讓您為具有特定屬性（如簽署 ID、作者、簽名日期和資料因素）的文件簽章定義結構化格式。

#### 步驟 1：定義 DocumentSignatureData 類
```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.math.BigDecimal;
import java.util.Date;

public static class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID;

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    @FormatAttribute(propertyName = "SAuth")
    public final String Author;

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date();

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01);

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
**解釋**： 
- 此類別使用註釋來格式化每個屬性，以幫助序列化。
- 屬性包括以下不可變字段： `Author` 和 `Signed`，確保元資料的完整性。

### 功能2：自訂XOR加密
透過實現一種簡單而有效的加密方法，此功能可讓您使用 XOR 邏輯保護文件資料。

#### 步驟2：實作CustomXOREncryption類
```java
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;

class CustomXOREncryption implements IDataEncryption {
    @Override
    public byte[] encrypt(byte[] data) {
        byte[] result = new byte[data.length];
        for (int i = 0; i < data.length; i++) {
            result[i] = (byte)(data[i] ^ 0x5A); // 與密鑰進行異或
        }
        return result;
    }

    @Override
    public byte[] decrypt(byte[] data) {
        return encrypt(data); // 由於 XOR 屬性，解密操作相同
    }
}
```
**解釋**： 
- 這 `encrypt` 和 `decrypt` 方法是對稱的，因為使用相同金鑰的 XOR 運算可以逆轉。

### 功能 3：元資料簽名設定與簽名
此功能示範如何使用 GroupDocs.Signature 設定元資料簽章並將其套用到您的文件。

#### 步驟 3：使用自訂元資料簽署文檔
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.signatures.metadata.WordProcessingMetadataSignature;
import com.groupdocs.signature.options.sign.MetadataSignOptions;

import java.io.File;
import java.util.UUID;

public static void signDocumentWithMetadata() throws Exception {
    String filePath = "YOUR_DOCUMENT_DIRECTORY";
    String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignedDocument.docx").getPath();

    Signature signature = new Signature(filePath);
    IDataEncryption encryption = new CustomXOREncryption();

    MetadataSignOptions options = new MetadataSignOptions();
    options.setDataEncryption(encryption);

    DocumentSignatureData documentSignature = new DocumentSignatureData();
    documentSignature.setID(UUID.randomUUID().toString());
    documentSignature.setAuthor("YourUsername");
    documentSignature.setSigned(new Date());
    documentSignature.setDataFactor(new BigDecimal("11.22"));

    WordProcessingMetadataSignature mdSignature = new WordProcessingMetadataSignature("Signature", documentSignature);
    WordProcessingMetadataSignature mdAuthor = new WordProcessingMetadataSignature("Author", "Mr.Scherlock Holmes");
    mdAuthor.setDataEncryption(encryption);
    WordProcessingMetadataSignature mdDocId = new WordProcessingMetadataSignature("DocumentId", UUID.randomUUID().toString());

    options.getSignatures().add(mdSignature);
    options.getSignatures().add(mdAuthor);
    options.getSignatures().add(mdDocId);

    signature.sign(outputFilePath, options);
}
```
**解釋**： 
- 此方法設定帶有加密的元資料簽章並將其套用至文件。
- 它示範如何使用 GroupDocs.Signature 自訂和安全地簽署文件。

## 實際應用
以下是加密和簽署文檔元資料的一些實際用例：
1. **法律合約**：透過加密元資料來保護敏感的合約細節，以防止未經授權的存取。
2. **醫療記錄**：使用加密簽章保護醫療文件中病患資料的完整性。
3. **財務文件**：透過應用元資料簽章確保金融交易的真實性。
4. **公司文件**：透過強大的元資料保護來維護文件的安全性和合規性。

## 結論
透過本指南，您學習如何使用 GroupDocs.Signature for Java 加密和簽署文件元資料來增強 Java 應用程式的安全性。此過程不僅可以保護敏感訊息，還可以確保各種專業環境中文件的真實性。