---
categories:
- Document Signing
- Healthcare Integration
date: '2026-05-16'
description: 了解如何使用 GroupDocs.Signature for Java 創建 Data Matrix PDF 並添加 QR code PDF。一步一步的醫療文件簽署指南。
keywords:
- create data matrix pdf
- add qr code pdf
- HIBC barcode Java
lastmod: '2026-05-16'
linktitle: HIBC PDF 簽署 Java 指南
schemas:
- author: GroupDocs
  dateModified: '2026-05-16'
  description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  headline: Create Data Matrix PDF with HIBC Barcode in Java
  type: TechArticle
- description: Learn how to create data matrix PDF and add QR code PDF using GroupDocs.Signature
    for Java. Step‑by‑step guide for healthcare document signing.
  name: Create Data Matrix PDF with HIBC Barcode in Java
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
- java
- pdf-signing
- hibc
- healthcare
- barcode
- pharmaceutical
title: 使用 Java 創建帶 HIBC 條碼的 Data Matrix PDF
type: docs
url: /zh-hant/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/
weight: 1
---

# 建立含 HIBC 條碼的 Data Matrix PDF（Java）

如果您正在開發製藥或醫療保健物流軟件，可能已經遇到紙本追蹤、簽名遺失以及稽核噩夢的問題。**建立 Data Matrix PDF** 嵌入 HIBC LIC 條碼可透過提供防篡改、機器可讀的追蹤，解決印刷、掃描及法規審查等挑戰。在本教學中，您將會看到如何 **加入 QR code PDF** 支援，以及 Aztec 與 Data Matrix 格式，使用 GroupDocs.Signature for Java。

## 快速解答
- **什麼程式庫在 Java 中處理 HIBC 條碼？** GroupDocs.Signature for Java。  
- **哪種條碼格式最緊湊？** Data Matrix – 適用於小尺寸標籤。  
- **我可以在同一個 PDF 中同時加入 QR 與 Data Matrix 嗎？** 可以，只需建立不同的 `QrCodeSignOptions`。  
- **執行時需要網際網路連線嗎？** 不需要，程式庫安裝後即可完全離線運作。  
- **建議使用哪個 Java 版本？** Java 11+ 以獲得正式環境的效能。

## 什麼是 HIBC 條碼 PDF 簽署？
`Signature` 類別（屬於 GroupDocs.Signature for Java）代表 PDF 文件，並提供將 HIBC 條碼嵌入為數位簽章的方法。透過以 HIBC 條碼簽署 PDF，您可建立可驗證且防篡改的紀錄，供供應鏈任何階段掃描使用。

## 為何同時使用 Data Matrix 與 QR 條碼？
GroupDocs.Signature 支援 **超過 50 種輸入與輸出格式**，且能在不將整個檔案載入記憶體的情況下處理數百頁的 PDF。將 Data Matrix 用於密集且面積小的標籤，並使用 QR 於較大空間的文件，可在可讀性、資料容量（QR 最多可容納 4,296 個字元）以及列印空間效率之間取得最佳平衡。

## 前置條件
- **JDK 11 或以上**（Java 8 仍可使用，但建議使用 Java 11+ 以獲得最佳效能）。  
- **IDE** 如 IntelliJ IDEA、Eclipse 或具 Java 擴充功能的 VS Code。  
- **Maven 或 Gradle** 用於相依性管理（以下範例）。  
- **範例 PDF**（例如 `sample.pdf`）以測試實作。  
- **有效的 GroupDocs.Signature 授權**（開發可使用免費試用，正式環境需購買授權）。

## 設定 GroupDocs.Signature for Java

### Maven 設定
Add the dependency to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 設定
For Gradle projects, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下載方式
您也可以直接從 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) 下載 JAR 檔，並手動加入專案的 classpath。此方式在受限網路環境下運作良好。

### 取得授權
向 GroupDocs 申請免費試用或臨時授權，以移除浮水印並解鎖全部功能。正式上線需購買授權。

### 基本初始化
The `Signature` class is the entry point for all signing operations. It loads the PDF, applies the barcode, and writes the signed file.

```java
import com.groupdocs.signature.Signature;

class InitializeSignature {
    public static void main(String[] args) {
        Signature signature = new Signature("sample.pdf");
        // Proceed with signing operations...
    }
}
```

## 如何建立含 HIBC 條碼的 Data Matrix PDF？

載入來源 PDF，為 Data Matrix 格式配置 `QrCodeSignOptions` 物件，然後呼叫 `sign()`——這就是嵌入符合 HIBC 標準的 Data Matrix 條碼所需的全部步驟。以下步驟將逐步說明所需的程式碼。`QrCodeSignOptions` 定義條碼簽章的設定，例如類型、內容、尺寸與位置。

1. **匯入所需的類別** – 取得簽章引擎與 Data Matrix 設定的存取權。

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
```

2. **建立 `Signature` 物件**，使用來源與目標檔案的絕對路徑。

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

4. **將簽章套用** 至 PDF。

```java
signature.sign(destinFilePath, hibcLic_QR);
```

5. **釋放資源**，以關閉檔案句柄並避免記憶體洩漏。

```java
finally {
    if (signature != null) signature.dispose();
}
```

### 完整範例
Here’s the full flow in a single block (the placeholders represent the exact code you’ll paste from the earlier snippets):

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

#### 直接答案（40–70 字）
要 **建立 Data Matrix PDF**，先以來源 PDF 建立 `Signature`，將 `QrCodeSignOptions` 設為 `QrCodeTypes.HIBCLICDataMatrix` 並提供正確格式的 HIBC 字串，最後呼叫 `signature.sign(outputPath, options)`。程式庫會將簽署後的 PDF 寫入目標位置，保留版面配置並將條碼嵌入為防篡改簽章。

## 如何使用 GroupDocs.Signature 在 PDF 中加入 QR 條碼？

載入 PDF，為 QR 格式配置 `QrCodeSignOptions`，然後呼叫 `sign()`。此兩行程式碼模式適用於任何尺寸的 PDF，且會自動縮放 QR 圖片以達到最佳可讀性。`QrCodeSignOptions` 設定 QR 條碼簽章，包括內容與視覺屬性。它會根據您設定的座標定位條碼，確保不與現有內容重疊，且列印後仍可掃描。

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

> **直接答案：** 在 `QrCodeSignOptions` 中使用 `QrCodeTypes.HIBCLICQR`，設定 HIBC 內容字串，使用 `setLeft()` 與 `setTop()` 位置條碼，最後呼叫 `signature.sign(outputPath, options)`。QR 條碼即時嵌入，可供手機或掃描器捕捉。

## 常見錯誤須避免

### 1. 忘記釋放資源
**錯誤範例：**  

```java
Signature signature = new Signature("sample.pdf");
signature.sign(destinFilePath, options);
// Oops, no dispose() call
```  

**修正方式：** 將 `Signature` 的使用包在 try‑with‑resources 區塊，或在 finally 中明確呼叫 `close()`。

### 2. 使用不正確的 HIBC 格式字串
**錯誤範例：** 使用像 “12345” 這樣的通用字串。  
**修正方式：** 依照 HIBCC 標準（例如 `A123PROD30917/75#422011907#GP293`），並使用 [HIBCC online validator](https://www.hibcc.org/) 進行驗證。

### 3. 硬編碼檔案路徑
**錯誤範例：**  
```java
String sourceFilePath = "C:/Users/John/Documents/test.pdf";
```  

**修正方式：** 將路徑存於設定檔或環境變數，於執行時讀取。

### 4. 忽視條碼位置衝突
將條碼放置於現有文字或簽章之外。使用 PDF 座標系統（原點位於左下角），並以列印樣本測試。

### 5. 未使用實體掃描器測試
列印簽署後的 PDF，並使用工作流程中相同的硬體掃描。驗證不同列印品質下的可讀性。

## 醫療保健領域的實務應用

| 情境 | 建議條碼 | 適用原因 |
|----------|--------------------|--------------|
| **藥品分銷** | QR 條碼 | 資料容量大，手機普遍可掃描。 |
| **庫存管理** | Data Matrix | 佔位小，適合密集貨架標籤。 |
| **法規遵循（FDA 21 CFR Part 11）** | QR + Data Matrix | 雙格式提供冗餘與稽核能力。 |
| **醫療器材追蹤** | Aztec 條碼 | 尺寸緊湊，適用於空間受限的包裝。 |

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
- 使用固定執行緒池（`Executors.newFixedThreadPool(Runtime.getRuntime().availableProcessors() - 1)`）進行平行處理，但需監控堆積大小，因為每個 `Signature` 會將整個 PDF 載入記憶體。

### 保持函式庫更新
GroupDocs 的新版本可提升處理速度最高 **20 %**，並加入新的 HIBC 合規功能。建議每季檢查相依性更新。

### 快取模板
先載入 PDF 模板一次，為每種條碼變體複製一份，再對複製件簽署。此方式減少 I/O 並加速大量工作流程。

## 常見問題

**Q: GroupDocs.Signature 能簽署除 PDF 之外的檔案類型嗎？**  
A: 可以，它亦支援 DOCX、XLSX、PPTX、PNG、JPEG 與 TIFF，使用相同的條碼簽章 API。

**Q: 如何排除 “Invalid barcode content” 錯誤？**  
A: 確認您的 HIBC 字串符合 HIBCC 語法，使用線上驗證工具，並確保使用正確的 `QrCodeTypes` 常數對應所選格式。

**Q: 各 HIBC 格式的最大資料容量為何？**  
A: QR ≈ 4,296 個英數字元，Aztec ≈ 3,832 個數字 / 3,067 個英數字元，Data Matrix ≈ 3,116 個數字 / 2,335 個英數字元。建議將條碼長度控制在 200 個字元以確保掃描可靠性。

**Q: 能在同一個 PDF 中嵌入多種條碼類型嗎？**  
A: 完全可以。為不同位置建立獨立的 `QrCodeSignOptions` 物件，分別呼叫 `signature.sign()`。只要確保條碼不重疊即可。

**Q: 執行時簽署需要網路連線嗎？**  
A: 不需要。只要 JAR 放在 classpath 並啟用授權，所有操作皆在本機完成。

## 其他資源

- [GroupDocs.Signature for Java 文件說明](https://docs.groupdocs.com/signature/java/)  
- [API 參考指南](https://reference.groupdocs.com/signature/java/)  
- [最新發行下載](https://releases.groupdocs.com/signature/java/)  
- [購買授權](https://purchase.groupdocs.com/buy)  
- [取得免費試用](https://releases.groupdocs.com/signature/java/)  
- [申請臨時授權](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs 論壇](https://forum.groupdocs.com/c/signature/)

---

**最後更新：** 2026-05-16  
**測試環境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs  

```java
signature.sign(destinFilePath, hibcLic_DM);
```

## 相關教學

- [在 Java 中建立條碼簽章 PDF – GroupDocs 指南](/signature/java/barcode-signatures/create-sign-pdfs-groupdocs-barcode-java/)
- [在 Java 中建立條碼簽章 – 更新 PDF 條碼](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [如何使用 Java 與 GroupDocs.Signature 讀取 QR 條碼 PDF](/signature/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/)