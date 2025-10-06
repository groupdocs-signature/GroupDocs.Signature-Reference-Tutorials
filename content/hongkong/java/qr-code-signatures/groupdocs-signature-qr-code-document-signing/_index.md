---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 安全地對包含 HIBC 資料編碼的二維碼文件進行簽署。立即簡化您的文件管理流程。"
"title": "使用 GroupDocs.Signature for Java 實作二維碼文件簽章的綜合指南"
"url": "/zh-hant/java/qr-code-signatures/groupdocs-signature-qr-code-document-signing/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature for Java 實作主文檔二維碼簽名

## 介紹

在數位時代，高效管理和保護藥品數據對於合規性和營運效率至關重要。將全面的產品資訊整合到文件中可能頗具挑戰性。本教學示範如何使用 **GroupDocs.Signature for Java** 在二維碼中編碼健康產業條碼 (HIBC) 資料並無縫簽署文件。

### 您將學到什麼：
- 為 Java 設定 GroupDocs.Signature。
- 建立 HIBCLICPrimaryData、HIBCLICSecondaryAdditionalData 及其組合形式的實例。
- 使用編碼詳細產品資訊的二維碼簽署文件。
- 在有效管理資源的同時優化效能。

## 先決條件

### 所需的庫和依賴項
若要使用 GroupDocs.Signature for Java，請確保您已具備：
- **Java 開發工具包 (JDK)**：版本 8 或更高版本。
- **Maven** 或者 **Gradle**：用於依賴管理。

### 環境設定要求
確保您的開發環境配置為使用 Maven 或 Gradle，從而簡化依賴關係和專案建置管理。

### 知識前提
熟悉 Java 程式設計將有助於理解程式碼片段和實作細節。

## 為 Java 設定 GroupDocs.Signature

### 安裝訊息

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

**直接下載**：從下載最新版本 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 許可證取得步驟
1. **免費試用**：首先下載試用版來測試基本功能。
2. **臨時執照**：在評估期間，您可以不受限制地獲得完全存取權限。
3. **購買**：考慮購買長期專案的許可證。

#### 基本初始化和設定
安裝完成後，初始化 `Signature` 物件與您想要簽署的文件的文件路徑：
```java
String filePath = "Sample.pdf";
Signature signature = new Signature(filePath);
```

## 實施指南

### 建立 HIBC LIC 原始數據
**概述**：本節示範如何建立和配置 `HIBCLICPrimaryData`，其中包含重要的產品資訊。

#### 步驟 1：初始化主資料對象
```java
HIBCLICPrimaryData primaryData = new HIBCLICPrimaryData();
```

#### 步驟 2：設定基本屬性
- **產品或目錄編號**：產品的唯一識別碼。
- **標籤識別碼**：標識製造商。
- **計量單位 ID**：指定測量單位。

```java
primaryData.setProductOrCatalogNumber("12345");
primaryData.setLabelerIdentificationCode("A999");
primaryData.setUnitOfMeasureID(1);
```

### 建立 HIBC LIC 輔助附加數據
**概述**：本節介紹建立和配置 `HIBCLICSecondaryAdditionalData`，其中包括有效期和批號等其他詳細資訊。

#### 步驟 1：初始化輔助資料對象
```java
HIBCLICSecondaryAdditionalData secondaryData = new HIBCLICSecondaryAdditionalData();
```

#### 步驟 2：設定其他屬性
- **到期日**：使用目前日期進行演示。
- **數量、批號、序號**：定義產品細節。
- **生產日期和連結字符**：建立製造細節。

```java
secondaryData.setExpiryDate(new Date());
secondaryData.setExpiryDateFormat(HIBCLICDateFormat.MMDDYY);
secondaryData.setQuantity(30);
secondaryData.setLotNumber("LOT123");
secondaryData.setSerialNumber("SERIAL123");
secondaryData.setDateOfManufacture(new Date());
secondaryData.setLinkCharacter('S');
```

### 結合 HIBC LIC 的主要數據和次要數據
**概述**：了解如何將主要數據和次要數據合併為一個 `HIBCLICCombinedData` 對象進行管線化處理。

#### 步驟 1：初始化組合資料對象
```java
HIBCLICCombinedData combinedData = new HIBCLICCombinedData();
```

#### 步驟2：設定主要數據和次要數據
- 將兩個資料集連結起來以形成完整的資料結構。

```java
combinedData.setPrimaryData(primaryData);
combinedData.setSecondaryAdditionalData(secondaryData);
```

### 使用包含 HIBC LIC 組合資料的二維碼簽署文件
**概述**：最後一部分示範如何使用對組合的 HIBC 資料進行編碼的二維碼來簽署文件。

#### 步驟 1：定義檔案路徑
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/Sample.pdf";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithQRCodeHIBCLICCombinedData/" + fileName;
```

#### 步驟 2：設定二維碼簽名選項
- **編碼類型**： 使用 `QrCodeTypes.HIBCLICQR` 指定編碼類型。
- **資料分配**：傳遞組合資料以包含在二維碼中。

```java
Signature signature = new Signature(filePath);
try {
    QrCodeSignOptions options = new QrCodeSignOptions();
    options.setEncodeType(QrCodeTypes.HIBCLICQR);
    options.setData(combinedData);

    // 簽署並儲存文件
    signature.sign(outputFilePath, options);
} finally {
    if (signature != null) signature.dispose();
}
```

## 實際應用
1. **藥品合規性**：透過這種整合簡化對監管標準的遵守。
2. **供應鏈管理**：透過文件中的二維碼增強藥品的可追溯性。
3. **醫療保健系統集成**：在醫療記錄中嵌入全面的產品數據，以提高病患的安全性。

## 性能考慮
- **優化資源使用**：透過處理 `Signature` 對象後操作。
- **最佳實踐**：定期更新至最新的 GroupDocs.Signature 版本以提高效能並修復錯誤。

## 結論
透過本指南，您學習如何建立 HIBC LIC 主資料對象和次資料對象，將它們合併為單一實體，以及如何使用 GroupDocs.Signature for Java 為文件簽署二維碼。這些技能可以增強文件安全性，並確保製藥業的合規性。

### 後續步驟
- 探索 GroupDocs.Signature 的其他功能。
- 將此解決方案整合到您現有的系統中，以自動化文件簽署流程。

## 常見問題部分
1. **什麼是 HIBC 資料？**
   - 健康產業條碼 (HIBC) 資料包含醫療保健和製藥業使用的重要產品資訊。
2. **我可以將 GroupDocs.Signature 用於其他類型的條碼嗎？**
   - 是的，GroupDocs.Signature 除了支援二維碼之外，還支援多種條碼格式。
3. **如果我的文件格式不是 PDF 怎麼辦？**
   - GroupDocs.Signature 支援多種文件格式，包括 Word 和 Excel。
4. **簽名過程中出現異常如何處理？**
   - 實作 try-catch 區塊以有效管理異常並確保資源清理。
5. **每份文件的二維碼數量有限制嗎？**
   - 沒有固有的限制；但是，在添加大量程式碼時要考慮效能影響。

## 資源
- **文件**： [Java 文件的 GroupDocs.Signature](https://docs.groupdocs.com/signature/java/)
- **API 參考**： [GroupDocs API 參考](https://reference.groupdocs.com/signature/java/)
- **下載**： [最新 GroupDocs.Releases](https://releases.groupdocs.com/signature/java/)
- **購買**： [購買許可證](https://purchase.groupdocs.com/buy)
- **免費試用**： [免費試用](https://releases.groupdocs.com/signature/java/)
- **臨時執照**： [在此申請](https://purchase.groupdocs.com/temporary-license/)