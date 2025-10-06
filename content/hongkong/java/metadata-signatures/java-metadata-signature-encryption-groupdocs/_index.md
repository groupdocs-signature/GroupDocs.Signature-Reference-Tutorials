---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature 在 Java 中實作安全元資料簽名，增強文件的完整性和真實性。"
"title": "使用 GroupDocs 透過元資料簽章和加密保護 Java 文檔"
"url": "/zh-hant/java/metadata-signatures/java-metadata-signature-encryption-groupdocs/"
"weight": 1
type: docs
---
# 使用 GroupDocs 透過元資料簽章和加密保護 Java 文檔

## 介紹
在數位時代，保護文件對於保護敏感資訊至關重要。 **GroupDocs.Signature for Java** 提供強大的文件簽章和加密解決方案，確保文件的安全性和真實性。本教學將指導您使用 Java 實作元資料簽章和加密。

您將學到什麼：
- 為 GroupDocs.Signature 設定環境
- 使用 Java 建立自訂元資料資料類
- 使用加密元資料簽名對文件進行簽名

在繼續之前，讓我們先回顧一下先決條件。

## 先決條件
在開始之前，請確保您已準備好以下內容：

### 所需的庫和依賴項
- **GroupDocs.Signature for Java**：使用 Maven 或 Gradle 將此庫包含在您的專案中。

### 環境設定要求
- JDK 8 或更高版本
- IntelliJ IDEA 或 Eclipse 等 IDE
- 用於測試的範例文件（例如 Word 文件）

### 知識前提
- 對 Java 程式設計有基本的了解
- 熟悉 Maven 或 Gradle 建置工具

## 為 Java 設定 GroupDocs.Signature
若要使用 GroupDocs.Signature，請將其作為依賴項新增至您的專案：

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

**直接下載：**
從下載最新版本 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 許可證取得步驟
- **免費試用**：從免費試用開始探索功能。
- **臨時執照**：取得臨時許可證以進行延長測試。
- **購買**：購買許可證以獲得完全訪問和支援。

若要初始化 GroupDocs.Signature，請建立一個實例 `Signature` 班級：
```java
Signature signature = new Signature("YOUR_DOCUMENT_PATH");
```

## 實施指南
### 自訂元資料資料類
#### 概述
此功能可讓您為文件簽名定義自訂元資料。透過建立資料類，您可以儲存其他信息，例如作者詳細資料和簽名日期。

#### 實作資料類
1. **定義資料類**
   ```java
   import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
   import java.util.Date;
   import java.math.BigDecimal;

   class DocumentSignatureData {
       @FormatAttribute(propertyName = "SignID")
       public String ID;

       public void setID(String value) { ID = value; }
       public String getID() { return ID; }

       @FormatAttribute(propertyName = "SAuth")
       public final String Author;

       public DocumentSignatureData(String author) {
           this.Author = author;
       }

       public void setAuthor(String value) { /* 未使用 */ }
       public final String getAuthor() { return Author; }

       @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
       public Date Signed = new Date();

       public void setSigned(Date value) { /* 未使用 */ }
       public final Date getSigned() { return Signed; }

       @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
       public BigDecimal DataFactor = new BigDecimal(0.01);

       public void setDataFactor(BigDecimal value) { /* 未使用 */ }
       public final BigDecimal getDataFactor() { return DataFactor; }
   }
   ```
   - **參數**：每個欄位都帶有註釋 `@FormatAttribute` 定義其名稱和格式。
   - **目的**：此類存儲元數據，如簽名 ID、作者、簽名日期和數據因素。

### 帶有加密的元資料簽名
#### 概述
此功能示範如何使用加密元資料簽名對文件進行簽名，確保文件的元資料保持安全且防篡改。

#### 實現加密
1. **設定密鑰和密碼**
   ```java
   String key = "1234567890";
   String salt = "1234567890";
   ```
2. **建立資料加密對象**
   使用Rijndael演算法進行加密：
   ```java
   IDataEncryption encryption = new SymmetricEncryption(SymmetricAlgorithmType.Rijndael, key, salt);
   ```
3. **配置元資料簽章選項**
   ```java
   MetadataSignOptions options = new MetadataSignOptions();
   options.setDataEncryption(encryption);
   ```
4. **建立並新增元資料簽名**
   ```java
   DocumentSignatureData documentSignature = new DocumentSignatureData(System.getenv("USERNAME"));
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setSigned(new Date());
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   WordProcessingMetadataSignature mdSignature = new WordProcessingMetadataSignature("Signature", documentSignature);
   WordProcessingMetadataSignature mdAuthor = new WordProcessingMetadataSignature("Author", "Mr.Scherlock Holmes");
   WordProcessingMetadataSignature mdDocId = new WordProcessingMetadataSignature("DocumentId", UUID.randomUUID().toString());

   options.getSignatures().add(mdSignature);
   options.getSignatures().add(mdAuthor);
   options.getSignatures().add(mdDocId);
   ```
5. **簽署文件**
   ```java
   signature.sign(outputFilePath, options);
   ```

### 故障排除提示
- 確保您的文件路徑正確。
- 驗證您的加密金鑰和鹽是否設定正確。
- 檢查簽名過程中是否有異常並進行適當處理。

## 實際應用
1. **法律文件管理**：使用加密元資料安全地簽署合約以確保真實性。
2. **企業合規**：使用元資料簽章來追蹤文件批准和修改。
3. **金融交易**：透過加密元資料來保護敏感的財務文件。
4. **醫療記錄**：透過使用加密元資料簽署醫療記錄來確保患者的隱私。
5. **教育機構**：安全地管理學生記錄和成績單。

## 性能考慮
- **優化資源使用**：使用高效的資料結構來最大限度地減少記憶體使用。
- **Java記憶體管理**：監控並調整 JVM 設定以獲得最佳效能。
- **最佳實踐**：遵循 GroupDocs.Signature 的指南，有效處理大型文件。

## 結論
本教學探討如何使用 GroupDocs.Signature 實作帶有加密的 Java 元資料簽章。請按照以下步驟操作，您可以有效地保護文檔，確保其完整性和真實性。

### 後續步驟
- 嘗試不同的加密演算法。
- 探索 GroupDocs.Signature 的其他功能。
- 將 GroupDocs.Signature 整合到更大的應用程式中。

## 常見問題部分
**Q1：什麼是 Java 版 GroupDocs.Signature？**
A1：它是一個為 Java 應用程式中的文件簽章和加密提供全面解決方案的函式庫。

**Q2：如何在我的專案中設定 GroupDocs.Signature？**
A2：使用 Maven 或 Gradle 將其新增為依賴項，或直接從他們的網站下載 JAR 檔案。

**問題 3：我可以將自訂元資料與簽章一起使用嗎？**
A3：是的，您可以為您的文件簽章定義和使用自訂元資料資料類別。

**Q4：支援哪些加密演算法？**
A4：GroupDocs.Signature 支援各種對稱加密演算法，包括 Rijndael。

**Q5：簽約過程中出現異常如何處理？**
A5：使用try-catch區塊來有效地擷取和管理異常。