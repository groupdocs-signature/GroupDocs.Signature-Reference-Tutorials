---
categories:
- Document Signing
- Healthcare Integration
date: '2026-09-15'
description: 了解如何使用 GroupDocs.Signature for Java 以條碼簽署 PDF。一步一步的指南，教您在醫療文件中加入 Data
  Matrix 與 QR 代碼。
keywords:
- sign pdf with barcode
- add qr code pdf
- hibc barcode java
- pdf signing java
- healthcare barcode signing
lastmod: '2026-09-15'
linktitle: HIBC PDF 簽署 Java 指南
og_description: 使用 GroupDocs.Signature for Java 以條碼簽署 PDF。了解如何在幾個步驟內於醫療文件中嵌入 Data
  Matrix 與 QR 代碼。
og_image_alt: 'Developer tutorial: sign PDF with HIBC barcode using GroupDocs.Signature
  for Java'
og_title: 使用 HIBC 於 Java 中以條碼簽署 PDF – GroupDocs 指南
schemas:
- author: GroupDocs
  dateModified: '2026-09-15'
  description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  headline: Sign PDF with barcode using HIBC in Java
  type: TechArticle
- description: Learn how to sign PDF with barcode using GroupDocs.Signature for Java.
    Step‑by‑step guide for adding Data Matrix and QR codes in healthcare documents.
  name: Sign PDF with barcode using HIBC in Java
  steps:
  - name: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
    text: '**Import the required classes** – these give you access to the signature
      engine and Data Matrix options.'
  - name: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
    text: '**Instantiate the `Signature` object** with absolute paths for source and
      destination files.'
  - name: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
    text: '**Configure the Data Matrix options** – set the HIBC string, choose `QrCodeTypes.HIBCLICDataMatrix`,
      and define placement coordinates. `QrCodeTypes` enumerates the supported barcode
      formats for HIBC signatures.'
  - name: '**Apply the signature** to the PDF.'
    text: '**Apply the signature** to the PDF.'
  - name: '**Dispose of resources** to free file handles and avoid memory leaks.'
    text: '**Dispose of resources** to free file handles and avoid memory leaks.'
  - name: '**Import QR‑specific classes**'
    text: '**Import QR‑specific classes**'
  - name: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
    text: '**Create and configure QR options** – note the use of `QrCodeTypes.HIBCLICQR`.'
  - name: '**Sign the document**'
    text: '**Sign the document**'
  type: HowTo
- questions:
  - answer: Yes, it also supports DOCX, XLSX, PPTX, PNG, JPEG, and TIFF with the same
      barcode‑signing API.
    question: Can GroupDocs.Signature sign file types other than PDF?
  - answer: Verify that your HIBC string follows the exact HIBCC syntax, use the online
      validator, and ensure you’re using the correct `QrCodeTypes` constant for the
      chosen format.
    question: How do I troubleshoot “Invalid barcode content” errors?
  - answer: QR ≈ 4,296 alphanumeric characters, Aztec ≈ 3,832 numeric / 3,067 alphanumeric,
      Data Matrix ≈ 3,116 numeric / 2,335 alphanumeric. Keep codes under 200 characters
      for optimal scan reliability.
    question: What is the maximum data capacity for each HIBC format?
  - answer: Absolutely. Create separate `QrCodeSignOptions` objects with different
      positions and call `signature.sign()` for each. Just ensure they don’t overlap.
    question: Is it possible to embed multiple barcode types in one PDF?
  - answer: No. After the JAR is on the classpath and the license is activated, all
      operations are performed locally.
    question: Do I need an internet connection for signing at runtime?
  type: FAQPage
tags:
- sign pdf
- barcode
- java
- healthcare
- groupdocs
title: 如何在 Java 中使用 HIBC 條碼簽署 PDF
type: docs
url: /zh-hant/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# 使用 HIBC 在 Java 中以條碼簽署 PDF

如果您正在開發製藥或醫療保健物流軟件，可能已經遇到紙本追蹤、簽名遺失以及稽核噩夢的問題。**以條碼簽署 PDF**——尤其是 HIBC Data Matrix 或 QR 代碼——可建立防篡改、機器可讀的痕跡，能在列印、掃描和法規審查中存活。於本教學中，您將看到如何使用 GroupDocs.Signature for Java 為 PDF 添加 Data Matrix 與 QR 條碼。

## 快速回答
- **什麼程式庫在 Java 中處理 HIBC 條碼？** GroupDocs.Signature for Java。  
- **哪種條碼格式最緊湊？** Data Matrix – 適用於小尺寸標籤。  
- **我可以在同一 PDF 中同時加入 QR 與 Data Matrix 嗎？** 可以，只需建立分別的 `QrCodeSignOptions`。  
- **執行時需要網際網路連線嗎？** 不需要，程式庫安裝後即可完全離線運作。  
- **建議使用哪個 Java 版本？** Java 11+ 以獲得生產等級的效能。

## 什麼是 HIBC 條碼 PDF 簽署？
`Signature` 是 GroupDocs.Signature 的核心類別，代表 PDF 文件並允許嵌入數位簽章。GroupDocs.Signature for Java 中的 `Signature` 類別提供將 HIBC 條碼作為數位簽章嵌入的方法。透過以 HIBC 條碼簽署 PDF，您可建立可驗證、防篡改的記錄，供供應鏈任何階段掃描。

## 為何同時使用 Data Matrix 與 QR 代碼？
Data Matrix 具最小的佔位空間，同時可容納多達 2,335 個字母數字字元，適合密集標籤區域。相較之下，QR 代碼支援最高 4,296 個字元，且可被智慧手機普遍讀取。結合兩者可在空間效率與資料容量之間取得最佳平衡，確保所有利害關係人——從倉庫掃描器到行動應用程式——皆能讀取所需資訊。

## 前置條件
- **JDK 11 或更高**（Java 8 亦可使用，但建議使用 Java 11+ 以獲得最佳效能）。  
- **IDE** 如 IntelliJ IDEA、Eclipse 或具 Java 擴充功能的 VS Code。  
- **Maven 或 Gradle** 用於相依管理（以下示例）。  
- **範例 PDF**（例如 `sample.pdf`）以測試實作。  
- **有效的 GroupDocs.Signature 授權**（開發可使用免費試用，正式環境需購買授權）。

## 設定 GroupDocs.Signature for Java

### Maven 設定
將相依加入您的 `pom.xml`：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 設定
對於 Gradle 專案，將以下內容加入您的 `build.gradle`：

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下載選項
您亦可直接從 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) 下載 JAR 檔，手動加入專案的 classpath。此方式在受限網路環境中表現良好。

### 取得授權
向 GroupDocs 申請免費試用或臨時授權，以移除浮水印並解鎖全部功能。正式部署需購買授權。

### 基本初始化
`Signature` 為所有簽署操作的入口點。它會載入 PDF、套用條碼，並寫入已簽署的檔案。

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## 如何使用 HIBC 條碼建立 Data Matrix PDF？
實例化 `Signature` 並傳入來源 PDF，將 `QrCodeSignOptions` 設為 **Data Matrix** 格式，提供正確格式的 HIBC 字串，然後呼叫 `sign()`。程式庫會將已簽署的 PDF 寫入目標位置，保留版面配置，並將條碼嵌入為防篡改簽章。  
`QrCodeSignOptions` 指定條碼類型、內容、大小與簽章的放置位置。

1. **匯入所需類別** – 取得簽章引擎與 Data Matrix 選項的存取權。  

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **實例化 `Signature` 物件**，使用來源與目標檔案的絕對路徑。  

```java
String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY";
String destinFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithHIBCLICQR.pdf";

final Signature signature = new Signature(sourceFilePath);
```

3. **設定 Data Matrix 選項** – 設定 HIBC 字串、選擇 `QrCodeTypes.HIBCLICDataMatrix`，並定義放置座標。`QrCodeTypes` 列舉了 HIBC 簽章支援的條碼格式。  

```java
QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR);
hibcLic_QR.setLeft(1); // Set the position from left
hibcLic_QR.setTop(1);   // Set the position from top
hibcLic_QR.setReturnContent(true); // Return content after signing
hibcLic_QR.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

4. **套用簽章** 至 PDF。  

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **釋放資源**，以釋放檔案句柄並避免記憶體洩漏。  

```java
finally {
    if (signature != null) signature.dispose();
}
```

### 完整範例
以下是一個完整流程的單一程式碼區塊（占位符代表您先前片段中的實際程式碼）：

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

public class HibcQrSigning {
    public static void main(String[] args) {
        String sourceFilePath = "sample.pdf";
        String destinFilePath = "output/SignWithHIBCLICQR.pdf";
        
        Signature signature = null;
        try {
            signature = new Signature(sourceFilePath);
            
            QrCodeSignOptions hibcLic_QR = new QrCodeSignOptions(
                "A123PROD30917/75#422011907#GP293", 
                QrCodeTypes.HIBCLICQR
            );
            hibcLic_QR.setLeft(1);
            hibcLic_QR.setTop(1);
            hibcLic_QR.setReturnContent(true);
            hibcLic_QR.setReturnContentType(FileType.PNG);
            
            signature.sign(destinFilePath, hibcLic_QR);
            System.out.println("PDF signed successfully with HIBC QR code");
            
        } catch (Exception e) {
            System.err.println("Error signing PDF: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) signature.dispose();
        }
    }
}
```

#### 直接回答（40–70 字）
要 **建立 Data Matrix PDF**，先以來源 PDF 實例化 `Signature`，將 `QrCodeSignOptions` 設為 `QrCodeTypes.HIBCLICDataMatrix` 並提供正確格式的 HIBC 字串，然後呼叫 `signature.sign(outputPath, options)`。程式庫會將已簽署的 PDF 寫入目標位置，保留版面配置，並將條碼嵌入為防篡改簽章。

## 如何使用 GroupDocs.Signature 為 PDF 加入 QR 代碼？
載入 PDF，為 QR 格式設定 `QrCodeSignOptions`，然後呼叫 `sign()`。程式庫會調整 QR 圖片大小以確保可讀性，並根據您設定的座標定位，避免與現有內容重疊。此方式確保條碼在列印後仍可掃描，且符合 HIBC 標準。  
`QrCodeSignOptions` 定義 QR 條碼的內容、大小與位置。

1. **匯入 QR 專屬類別**  

```java
QrCodeSignOptions hibcLic_AZ = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec);
hibcLic_AZ.setLeft(1); // Set the position from left
hibcLic_AZ.setTop(200); // Set the position from top
hibcLic_AZ.setReturnContent(true); // Return content after signing
hibcLic_AZ.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

2. **建立並設定 QR 選項** – 注意使用 `QrCodeTypes.HIBCLICQR`。  

```java
signature.sign(destinFilePath, hibcLic_AZ);
```

3. **簽署文件**  

```java
QrCodeSignOptions hibcLic_DM = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix);
hibcLic_DM.setLeft(1); // Set the position from left
hibcLic_DM.setTop(400); // Set the position from top
hibcLic_DM.setReturnContent(true); // Return content after signing
hibcLic_DM.setReturnContentType(FileType.PNG); // Specify return content type as PNG
```

> **直接回答：** 在 `QrCodeSignOptions` 中使用 `QrCodeTypes.HIBCLICQR`，設定 HIBC 內容字串，使用 `setLeft()` 與 `setTop()` 位置條碼，然後呼叫 `signature.sign(outputPath, options)`。QR 條碼會即時嵌入，隨時可供智慧手機或掃描器捕捉。

## 常見錯誤須避免

### 1. 忘記釋放資源
**錯誤：**  
```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**修正：**  
將 `Signature` 的使用包在 try‑with‑resources 區塊，或在 finally 子句中明確呼叫 `close()`。

### 2. 使用不正確的 HIBC 格式字串
**錯誤：** 使用類似 “12345” 的通用字串。  
**修正：** 依照 HIBCC 標準（例如 `A123PROD30917/75#422011907#GP293`）。可使用 [HIBCC online validator](https://www.hibcc.org/) 進行驗證。

### 3. 硬編碼檔案路徑
**錯誤：**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**修正：** 將路徑存於設定檔或環境變數，於執行時讀取。

### 4. 忽視條碼位置衝突
將條碼放置於現有文字或簽章之外。使用 PDF 座標系統（原點在左下角），並以列印樣本測試。

### 5. 未使用實體掃描器測試
列印已簽署的 PDF，並使用工作流程中相同的硬體掃描。驗證在不同列印品質下的可讀性。

## 醫療保健的實務應用

| 情境 | 建議條碼 | 適用原因 |
|----------|--------------------|--------------|
| **藥品分銷** | QR Code | 高資料容量，智慧手機廣泛掃描。 |
| **庫存管理** | Data Matrix | 佔位小，適合密集貨架標籤。 |
| **法規遵循（FDA 21 CFR Part 11）** | QR + Data Matrix | 雙格式提供冗餘與稽核能力。 |
| **醫療器材追蹤** | Aztec Code | 尺寸緊湊，適用於有限空間的包裝。 |

## 效能考量與最佳實踐

### 批次處理模式
```java
List<String> filesToSign = getFileList();
for (String filePath : filesToSign) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // Sign and save
    } finally {
        if (signature != null) signature.dispose();
    }
}
```

- 為每個檔案建立新的 `Signature` 實例，以降低記憶體使用量。  
- 使用固定執行緒池（`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`）進行平行處理，但需監控堆積大小，因每個 `Signature` 會將整個 PDF 載入記憶體。

### 保持函式庫更新
GroupDocs 的新版本可提升處理速度最高 **20 %**，並加入新的 HIBC 合規功能。建議每季檢查相依性。

### 快取範本
一次載入 PDF 範本，為每種條碼變體克隆後再簽署。此方式減少 I/O，提升大量工作流程的速度。

## 常見問答

**Q: GroupDocs.Signature 能簽署除 PDF 之外的檔案類型嗎？**  
A: 可以，它同樣支援 DOCX、XLSX、PPTX、PNG、JPEG 與 TIFF，使用相同的條碼簽署 API。

**Q: 如何排除 “Invalid barcode content” 錯誤？**  
A: 確認您的 HIBC 字串符合 HIBCC 語法，使用線上驗證工具，並確保使用正確的 `QrCodeTypes` 常數對應所選格式。

**Q: 各 HIBC 格式的最大資料容量為何？**  
A: QR ≈ 4,296 個字母數字字元，Aztec ≈ 3,832 個數字 / 3,067 個字母數字，Data Matrix ≈ 3,116 個數字 / 2,335 個字母數字。為確保掃描可靠性，建議將碼長度控制在 200 個字元以內。

**Q: 能在同一 PDF 中嵌入多種條碼類型嗎？**  
A: 完全可以。建立不同位置的 `QrCodeSignOptions` 物件，分別呼叫 `signature.sign()`。只要確保它們不重疊即可。

**Q: 執行時簽署需要網際網路連線嗎？**  
A: 不需要。只要 JAR 在 classpath 且授權已啟用，所有操作皆在本機完成。

## 其他資源

- [GroupDocs.Signature for Java 文件](https://docs.groupdocs.com/signature/java/)  
- [API 參考指南](https://reference.groupdocs.com/signature/java/)  
- [最新發行下載](https://releases.groupdocs.com/signature/java/)  
- [購買授權](https://purchase.groupdocs.com/buy)  
- [取得免費試用](https://releases.groupdocs.com/signature/java/)  
- [申請臨時授權](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs 論壇](https://forum.groupdocs.com/c/signature/)  

---

**最後更新：** 2026-09-15  
**測試環境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs  

## 相關教學

- [在 Java 中建立條碼簽章 PDF – GroupDocs 指南](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [在 Java 中建立條碼簽章 – 更新 PDF 條碼](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [如何使用 Java 與 GroupDocs.Signature 讀取 QR 代碼 PDF](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)
