---
categories:
- Java PDF Processing
date: '2026-05-21'
description: 了解如何使用 GroupDocs.Signature 於 PDF 建立 Java 條碼簽章。完整指南包含程式碼範例、疑難排解技巧，以及文件驗證的實務案例。
keywords:
- create barcode signature java
- barcode signatures java
- pdf barcode signing java
lastmod: '2026-05-21'
linktitle: Java 中的 PDF 條碼簽章
schemas:
- author: GroupDocs
  dateModified: '2026-05-21'
  description: Learn how to create barcode signature Java for PDFs using GroupDocs.Signature.
    Complete guide with code examples, troubleshooting tips, and real-world use cases
    for document authentication.
  headline: How to Create Barcode Signature Java for PDF Documents
  type: TechArticle
- questions:
  - answer: A GS1CompositeBar combines linear and 2D components to store product IDs,
      serial numbers, and other data in a single scannable symbol, widely used in
      retail and logistics.
    question: What is a GS1CompositeBar barcode?
  - answer: Yes—GroupDocs.Signature supports over 60 types, including QR, Code128,
      DataMatrix, PDF417, and Aztec. Switch the `setEncodeType()` value to change
      the format.
    question: Can I use other barcode types besides GS1CompositeBar?
  - answer: A valid GroupDocs license is required for production deployments. A free
      trial is available for development and testing.
    question: Do I need a license for production use?
  - answer: Absolutely, provided the barcode is at least 200 × 100 px and has sufficient
      contrast. Smartphone scanning apps work on‑screen; hardware scanners work on
      printed copies.
    question: Will barcode scanners read barcodes from signed PDFs?
  - answer: Wrap your code in try‑catch blocks, log full stack traces, and always
      call `signature.dispose()` in a finally block to release resources.
    question: How do I handle errors during signing?
  type: FAQPage
tags:
- barcode-signatures
- pdf-signing
- document-authentication
- java-libraries
title: 如何使用 Java 為 PDF 文件建立條碼簽章
type: docs
url: /zh-hant/java/barcode-signatures/sign-pdf-gs1compositebar-barcode-groupdocs-signature-java/
weight: 1
---

# 如何在 PDF 文件中使用 Java 建立條碼簽章

## 介紹

在本教學中，您將學習如何使用 GroupDocs.Signature 為 PDF 檔案 **create barcode signature Java**。無論您需要在合約中嵌入產品代碼、稽核 ID 或任何結構化資料，條碼簽章都能讓您加入可即時掃描的機器可讀資訊，同時保持文件的加密安全性。我們將逐步說明設定、程式碼、客製化以及最佳實踐技巧，讓您在數分鐘內即可為 PDF 添加條碼簽章。

## 快速解答
- **什麼程式庫在 Java 中加入條碼簽章？** GroupDocs.Signature for Java.
- **哪種條碼類型最適合零售？** `GS1CompositeBar`（產業標準的產品追蹤條碼）。
- **生產環境是否需要授權？** 是 – 必須購買 GroupDocs 授權。
- **我可以同時加入數位與條碼簽章嗎？** 當然可以；結合兩者可提升安全性與可掃描性。
- **此程式碼是否相容於 Java 11 及以上版本？** 是，API 支援 JDK 8 以上。

## 什麼是 create barcode signature java？
`create barcode signature java` 指的是使用 Java 程式碼以程式化方式將條碼嵌入 PDF 的過程。GroupDocs.Signature 提供簡易的 API，可產生條碼影像、定位於頁面，並一次性儲存已簽署的文件。

## 為什麼使用條碼簽章？
條碼簽章在合法簽署的 PDF 中提供 **機器可讀的中繼資料**。它們可即時視覺驗證、簡化供應鏈掃描，並讓下游系統在不開啟檔案的情況下提取結構化資料。支援超過 60 種條碼格式，且 GS1CompositeBar 能在單一緊湊符號中編碼產品識別碼、序號與批次碼——非常適合零售、醫療與金融領域。

## 前置條件

- **Java 開發套件 (JDK)：** JDK 8 或更新版本（Java 11、17、21 都可）。
- **建置工具：** Maven 或 Gradle – 依您偏好選擇。
- **IDE：** IntelliJ IDEA、Eclipse 或 VS Code。
- **GroupDocs.Signature 程式庫：** 如下加入相依性。
- **授權：** 開發可使用免費試用版；生產環境需購買授權。

### 將 GroupDocs.Signature 加入您的專案

**For Maven users**, add this to your `pom.xml`:

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**For Gradle users**, add this to your `build.gradle`:

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**關於授權：** GroupDocs 提供免費試用版，適合測試與開發。您可從其 [releases page](https://releases.groupdocs.com/signature/java/) 下載。當您準備好投入生產時，需要購買授權或向 [GroupDocs website](https://purchase.groupdocs.com/buy) 申請臨時授權。欲深入了解 API 用法，請參閱 [API Reference](https://reference.groupdocs.com/signature/java/)，並參考 [Developer Guide](https://docs.groupdocs.com/signature/java/) 取得步驟說明，亦可在 [GroupDocs Forum](https://forum.groupdocs.com/) 提問。相同的購買連結亦列於 [purchase page](https://purchase.groupdocs.com/buy)。

## 如何在 Java 中設定 GroupDocs.Signature？

`Signature` 類別代表一個文件，提供套用簽章、搜尋內容與管理資源的方法。建立 `Signature` 實例以開啟 PDF 並為簽署做準備。`Signature` 類別是 GroupDocs.Signature 的核心元件，負責文件載入、資源處理與簽署工作流程，確保所有操作安全且高效。

```java
import com.groupdocs.signature.Signature;

// Point to your PDF file
Signature signature = new Signature("path/to/your/document.pdf");
```

**重要提示：** 使用完畢後務必釋放 `Signature` 物件——這會關閉檔案句柄並釋放記憶體。

## 如何設定條碼簽章選項？

`BarcodeSignOptions` 類別定義您即將嵌入的條碼的所有面向，從資料內容到視覺樣式。它是所有條碼相關設定（如類型、尺寸、顏色與位置）的容器。以下為最小化設定，建立包含 GTIN 與序號的 GS1CompositeBar 條碼，並示範如何設定邊距與背景色以提升可讀性。

```java
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

// Create barcode with GS1 format data
BarcodeSignOptions options = new BarcodeSignOptions("(01)03212345678906/(21)A1B2C3D4E5F6G7H8");
options.setEncodeType(BarcodeTypes.GS1CompositeBar);
```

字串 `"(01)03212345678906/(21)A1B2C3D4E5F6G7H8"` 符合 GS1 標準：
- `(01)` = GTIN（全球產品識別碼）
- `03212345678906` = 實際產品代碼
- `(21)` = 序號識別碼
- `A1B2C3D4E5F6G7H8` = 唯一序號

您可以將其替換為 QR Code、Code128、DataMatrix 等任何文字。支援超過 60 種條碼類型——完整清單請參閱 GroupDocs 文件。

## 如何定位與自訂條碼？

位置與樣式皆透過同一個 `BarcodeSignOptions` 物件控制。使用 `setTop`、`setLeft`、`setWidth` 與 `setHeight` 來定義精確座標與尺寸。設定 `setAllPages(true)` 可自動將條碼加入所有頁面，而 `setPageNumber(1)` 則指定特定頁面。您亦可旋轉條碼、加入背景色或調整邊距，以確保條碼不與現有內容重疊。

```java
// Set position and apply to all pages
options.setTop(200); // Set vertical position
options.setAllPages(true);
```

若需更精確的版面配置，您也可以將條碼錨定於特定頁面、旋轉或加入背景色：

```java
options.setLeft(100);        // 100 pixels from left edge
options.setTop(200);         // 200 pixels from top
options.setWidth(300);       // Barcode width in pixels
options.setHeight(100);      // Barcode height in pixels
options.setPageNumber(1);    // Only sign page 1 (removes setAllPages)
```

透過其他屬性可進行視覺客製化（前景/背景顏色、邊距、文字標籤）：

```java
options.setMargin(new Padding(10));           // Add padding around barcode
options.setBackground(new Background());       // Set background color
options.setForeColor(Color.BLACK);            // Barcode color
options.setBackgroundColor(Color.WHITE);      // Background color
```

## 如何使用條碼簽署文件？

`Signature` 實例的 `sign` 方法套用先前設定的選項，並將已簽署的文件寫入磁碟。它會回傳 `SignResult` 物件，告知已套用的簽章數量以及是否有警告發生。此方法處理所有低階 PDF 操作，您無需直接使用 PDF 程式庫。

```java
try {
    SignResult signResult = signature.sign(outputPath, options);
    System.out.println("Document signed successfully!");
    System.out.println("Signed document saved to: " + outputPath);
} finally {
    if (signature != null) {
        signature.dispose();
    }
}
```

外層的 try‑finally 區塊確保即使發生例外，`Signature` 物件仍會被釋放，避免檔案句柄洩漏。

```java
if (signResult.getSucceeded().size() > 0) {
    System.out.println("Successfully added " + signResult.getSucceeded().size() + " signature(s)");
}
```

## 完整範例

將上述所有步驟整合，以下是一個載入 PDF、加入 GS1CompositeBar 條碼，並儲存已簽署檔案的單一方法：

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

public class BarcodeSigningExample {
    
    public void signPdfWithBarcode(String inputPath, String outputPath) {
        Signature signature = null;
        
        try {
            // Initialize signature
            signature = new Signature(inputPath);
            
            // Configure barcode
            BarcodeSignOptions options = new BarcodeSignOptions(
                "(01)03212345678906/(21)A1B2C3D4E5F6G7H8"
            );
            options.setEncodeType(BarcodeTypes.GS1CompositeBar);
            options.setTop(200);
            options.setAllPages(true);
            
            // Sign and save
            SignResult result = signature.sign(outputPath, options);
            
            System.out.println("Signing completed: " + result.getSucceeded().size() + " signature(s) added");
            
        } catch (Exception e) {
            System.err.println("Error signing document: " + e.getMessage());
            e.printStackTrace();
        } finally {
            if (signature != null) {
                signature.dispose();
            }
        }
    }
}
```

此方法已具備生產環境可用性：會驗證輸入、管理資源，並回報結果。

## 如何同時加入數位與條碼簽章？

為了最高安全性，請先加入加密的數位簽章，然後再疊加條碼。數位簽章保證文件完整性，條碼則提供快速視覺驗證與機器可讀資料。第一步使用 `DigitalSignOptions` 類別，接著如上示範套用 `BarcodeSignOptions`。

```java
// First, add digital signature
DigitalSignOptions digitalOptions = new DigitalSignOptions("certificate.pfx");
digitalOptions.setPassword("cert_password");
signature.sign(outputPath, digitalOptions);

// Then, add barcode on top
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("DATA");
barcodeOptions.setEncodeType(BarcodeTypes.QR);
signature.sign(outputPath, barcodeOptions);
```

最終產生的 PDF 同時具備法律效力（數位簽章）與任何條碼掃描器即時可讀的特性。

## 使用不同條碼類型

切換條碼格式只需更改一個 enum 值。以下範例將 GS1CompositeBar 換成 QR Code：

```java
// Define barcode sign options with sample text
BarcodeSignOptions options = new BarcodeSignOptions("Sample Text");

// Assign specific barcode type
options.setEncodeType(BarcodeTypes.GS1CompositeBar);
```

以下示範將其改為 Code128 線性條碼：

```java
options.setEncodeType(BarcodeTypes.QR);           // QR code
options.setEncodeType(BarcodeTypes.Code128);      // Code 128
options.setEncodeType(BarcodeTypes.DataMatrix);   // Data Matrix
```

請記得每種條碼都有其資料容量限制——QR Code 可容納數千字元，而 Code39 僅支援英數字。

## 真實案例

### 供應鏈管理
在出貨清單上嵌入 GS1CompositeBar 可讓倉庫人員在不開啟 PDF 的情況下掃描訂單號、目的地與批次碼。

```java
BarcodeSignOptions options = new BarcodeSignOptions(
    "(01)" + gtin + "/(21)" + serialNumber + "/(10)" + batchNumber
);
options.setEncodeType(BarcodeTypes.GS1CompositeBar);
```

### 醫療文件
同意書上的 QR Code 可掃描後自動歸檔至正確的病人紀錄。

```java
String patientData = "PATIENT_ID:" + patientId + "|DOC_TYPE:CONSENT|DATE:" + dateString;
BarcodeSignOptions options = new BarcodeSignOptions(patientData);
options.setEncodeType(BarcodeTypes.QR);
```

### 金融服務
條碼中編碼的交易 ID 讓稽核人員只需簡單掃描即可驗證合規性。

```java
String complianceData = "TXN:" + transactionId + "|AGENT:" + agentId + "|BRANCH:" + branchCode;
BarcodeSignOptions options = new BarcodeSignOptions(complianceData);
options.setEncodeType(BarcodeTypes.PDF417);
```

### 製造品質控制
含有批號與檢查員 ID 的條碼簽署檢驗報告，使根因分析即時完成。

```java
String qcData = "BATCH:" + batchNumber + "|INSPECTOR:" + inspectorId + "|RESULT:" + passFailStatus;
BarcodeSignOptions options = new BarcodeSignOptions(qcData);
options.setEncodeType(BarcodeTypes.DataMatrix);
```

## 常見實作問題

### 問題 1：「File is already in use」例外
**解答：** 若先前的 `Signature` 實例未釋放，檔案會保持鎖定。請始終將簽署程式碼包在 try‑finally 區塊中，並呼叫 `signature.dispose()`。

```java
Signature signature = null;
try {
    signature = new Signature(filePath);
    // ... your code ...
} finally {
    if (signature != null) {
        signature.dispose();
    }
}
```

### 問題 2：條碼未顯示於 PDF
**解答：** 確認 `setTop`/`setLeft` 的值在頁面範圍內，增大條碼的寬度/高度，並確保前景/背景色與頁面背景形成對比。

```java
// Make sure dimensions are reasonable
options.setTop(100);      // Not 10000
options.setLeft(100);
options.setWidth(300);    // At least 200 pixels for readability
options.setHeight(100);

// Ensure contrast
options.setForeColor(Color.BLACK);
options.setBackgroundColor(Color.WHITE);
```

### 問題 3：「Invalid Barcode Data」例外
**解答：** GS1 條碼必須使用嚴格的括號表示法。請使用正確的應用識別碼（例如 `(01)`、`(21)`），並避免使用不支援的字元。

```java
// Correct:
"(01)03212345678906/(21)ABC123"

// Incorrect:
"03212345678906ABC123"
```

### 問題 4：大型 PDF 的 OutOfMemoryError
**解答：** 增加 JVM 記憶體上限（`-Xmx4G`），對於非常大的文件，考慮逐頁簽署而非使用 `setAllPages(true)`。

```bash
java -Xmx2G -jar your-application.jar
```

### 問題 5：條碼掃描失敗
**解答：** 確保條碼至少為 200 × 100 px，使用高對比度顏色，且不受 PDF 壓縮扭曲。

```java
// Increase size
options.setWidth(400);
options.setHeight(150);

// Maximize contrast
options.setForeColor(Color.BLACK);
options.setBackgroundColor(Color.WHITE);

// Add quiet zone (blank space around barcode)
options.setMargin(new Padding(10));
```

## 安全性與驗證

### 條碼簽章是否安全？
單獨的條碼並未經過加密保護，任何人都可能產生新的條碼。將其與數位簽章結合，可同時保證真偽與可掃描性。雙簽章模式（先數位後條碼）提供法律可執行性與操作便利性。

### 驗證條碼資料
掃描後，請驗證文件的數位簽章仍然有效，且條碼負載符合預期模式。可使用 GroupDocs 的 `search()` API 搭配 `BarcodeSearchOptions` 自動擷取並驗證條碼內容。

```java
public boolean validateScannedBarcode(String scannedData, String documentPath) {
    // Verify digital signature first
    if (!verifyDigitalSignature(documentPath)) {
        return false;
    }
    
    // Validate barcode format
    if (!scannedData.matches("(01)\\d{14}/(21)[A-Z0-9]+")) {
        return false;
    }
    
    // Check against database
    String productId = extractProductId(scannedData);
    return database.productExists(productId);
}
```

## 效能考量

### 資源管理
每次操作後務必釋放 `Signature` 物件，以避免記憶體洩漏：

```java
signature.dispose();
```

處理大量檔案時，請為每個文件建立並釋放新的 `Signature`：

```java
for (String filePath : documentPaths) {
    Signature signature = null;
    try {
        signature = new Signature(filePath);
        // ... signing logic ...
    } finally {
        if (signature != null) {
            signature.dispose();
        }
    }
}
```

### 批次處理
對於小批次（< 100 個檔案），順序處理最為簡單：

```java
for (String path : paths) {
    signDocument(path);
}
```

對於較大工作負載，可使用平行處理加速——但需監控 I/O 壓力，將執行緒數限制在 4‑8 個：

```java
paths.parallelStream().forEach(path -> signDocument(path));
```

### 大型 PDF 的記憶體最佳化
增大堆疊大小，逐頁處理，並在每一步後清除參考。這可防止超過 50 MB 的文件發生 `OutOfMemoryError`。

### 快取條碼選項
若在多個檔案中重複使用相同的條碼設定，可快取 `BarcodeSignOptions` 實例：

```java
// Create once, reuse many times
private static BarcodeSignOptions createStandardBarcodeOptions(String data) {
    BarcodeSignOptions options = new BarcodeSignOptions(data);
    options.setEncodeType(BarcodeTypes.GS1CompositeBar);
    options.setTop(200);
    options.setAllPages(true);
    return options;
}
```

## 進階功能

### 同一文件的多重簽章
透過多次呼叫 `sign` 並傳入不同的選項物件，可在同一文件加入多個條碼（或與數位簽章混合）：

```java
// Add QR code in top-left
BarcodeSignOptions qrOptions = new BarcodeSignOptions("https://example.com");
qrOptions.setEncodeType(BarcodeTypes.QR);
qrOptions.setTop(50);
qrOptions.setLeft(50);
signature.sign(outputPath, qrOptions);

// Add GS1 barcode in bottom-right
BarcodeSignOptions gs1Options = new BarcodeSignOptions("(01)03212345678906");
gs1Options.setEncodeType(BarcodeTypes.GS1CompositeBar);
gs1Options.setTop(700);
gs1Options.setLeft(400);
signature.sign(outputPath, gs1Options);
```

### 動態條碼內容
從文件中繼資料、時間戳記或資料庫查詢產生條碼資料：

```java
// Extract data from PDF or database
String orderId = extractOrderIdFromPdf(filePath);
String timestamp = LocalDateTime.now().format(DateTimeFormatter.ISO_DATE_TIME);
String barcodeData = String.format("ORDER:%s|TIME:%s", orderId, timestamp);

BarcodeSignOptions options = new BarcodeSignOptions(barcodeData);
```

### 與 Spring Boot 整合
公開一個 REST 端點，接收 PDF、加入條碼，並回傳已簽署的檔案：

```java
@Service
public class DocumentSigningService {
    public void signWithBarcode(MultipartFile file, String barcodeData) {
        // ... implementation ...
    }
}
```

### REST API 範例
一個最小化的控制器，將請求委派給簽署服務：

```java
@PostMapping("/sign-document")
public ResponseEntity<byte[]> signDocument(
    @RequestParam("file") MultipartFile file,
    @RequestParam("barcode") String barcodeData
) {
    // Sign document and return as byte array
}
```

## 常見問答

**Q: 什麼是 GS1CompositeBar 條碼？**  
A: GS1CompositeBar 結合線性與 2D 元件，於單一可掃描符號中儲存產品 ID、序號與其他資料，廣泛應用於零售與物流。

**Q: 我可以使用除 GS1CompositeBar 之外的其他條碼類型嗎？**  
A: 可以——GroupDocs.Signature 支援超過 60 種，包括 QR、Code128、DataMatrix、PDF417 與 Aztec。只需切換 `setEncodeType()` 的值即可變更格式。

**Q: 生產環境是否需要授權？**  
A: 生產部署必須擁有有效的 GroupDocs 授權。開發與測試可使用免費試用版。

**Q: 條碼掃描器能讀取已簽署的 PDF 中的條碼嗎？**  
A: 完全可以，只要條碼至少為 200 × 100 px 且具足夠對比度。智慧手機掃描應用可直接在螢幕上使用，硬體掃描器則適用於列印的文件。

**Q: 簽署過程中如何處理錯誤？**  
A: 將程式碼包在 try‑catch 區塊中，記錄完整堆疊資訊，並在 finally 區塊中始終呼叫 `signature.dispose()` 以釋放資源。

**Q: 我可以簽署其他文件格式嗎？**  
A: 可以——GroupDocs.Signature 亦支援 DOCX、XLSX、PPTX、影像等多種格式。只需更改輸入檔案的副檔名，API 皆保持不變。

**Q: 有檔案大小限制嗎？**  
A: 沒有硬性限制，但超過 50 MB 的文件可能需要更大的 JVM 堆疊，並以逐頁方式處理以維持記憶體效率。

**Q: 如何簽署儲存在雲端的 PDF？**  
A: 先將檔案下載至暫存本機路徑，套用簽章後再上傳回雲端儲存桶。完成後清除暫存檔案。

## 結論

您現在已擁有一套完整且可投入生產的 **create barcode signature java** PDF 文件指南。透過結合加密的數位簽章與機器可讀的條碼，您可在供應鏈、醫療、金融與製造等應用場景中同時達成法律效力與營運效率。請嘗試不同的條碼類型，將程式碼整合至現有服務，並探索大規模部署的批次處理方式。

---

**最後更新：** 2026-05-21  
**測試環境：** GroupDocs.Signature 23.10 for Java  
**作者：** GroupDocs  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY" + "/sample.pdf";
String fileName = new java.io.File(filePath).getName();
String outputPath = "YOUR_OUTPUT_DIRECTORY" + "/SignedWithBarcodeGS1CompositeBar/" + fileName;
```

```java
String documentDir = System.getenv("DOCUMENT_DIR");
String outputDir = System.getenv("OUTPUT_DIR");
```

```java
Signature signature = new Signature(filePath);
```

## 相關教學

- [在 Java 中建立條碼簽章 – 更新 PDF 條碼](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)
- [在 Java 中驗證條碼與 QR Code - 完整文件安全指南](/signature/java/search-verification/verify-barcode-qr-code-signatures-groupdocs-java/)
- [使用 Java 的 HIBC 條碼 PDF 簽署 - 完整醫療文件解決方案](/signature/java/barcode-signatures/sign-pdfs-hibc-lic-codes-groupdocs-java/)