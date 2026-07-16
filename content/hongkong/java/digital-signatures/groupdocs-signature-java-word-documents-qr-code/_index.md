---
categories:
- Digital Signatures
date: '2026-06-26'
description: 了解如何使用 GroupDocs.Signature for Java 以程式方式在 Word 文件中建立 QR Code 簽章。逐步教學、程式碼範例、最佳實踐與效能技巧。
keywords:
- create qr code signature
- programmatically sign word
- qr code digital signature
- add qr to word
- groupdocs signature java
lastmod: '2026-06-26'
linktitle: Java 在 Word 中的 QR Code 簽章
schemas:
- author: GroupDocs
  dateModified: '2026-06-26'
  description: Learn how to create QR code signature in Word documents programmatically
    with GroupDocs.Signature for Java. Step‑by‑step tutorial, code examples, best
    practices, and performance tips.
  headline: Create QR Code Signature in Word Documents Using Java
  type: TechArticle
- description: Learn how to create QR code signature in Word documents programmatically
    with GroupDocs.Signature for Java. Step‑by‑step tutorial, code examples, best
    practices, and performance tips.
  name: Create QR Code Signature in Word Documents Using Java
  steps:
  - name: The library reads the source document.
    text: The library reads the source document.
  - name: Generates the QR code based on `QrCodeSignOptions`.
    text: Generates the QR code based on `QrCodeSignOptions`.
  - name: Inserts the graphic at the specified coordinates.
    text: Inserts the graphic at the specified coordinates.
  - name: Saves the modified file to the path you provided.
    text: Saves the modified file to the path you provided.
  type: HowTo
- questions:
  - answer: Yes. GroupDocs.Signature supports PDF, Excel, PowerPoint, images, and
      many other formats. Just change the `setFileFormat` to the desired output type.
    question: Can I sign PDFs instead of Word documents?
  - answer: Use the library’s `SearchQrCodeSignatures` method to locate QR codes and
      validate the embedded data against your backend service.
    question: How do I verify a QR code signature after it’s been added?
  - answer: Standard QR codes hold up to **4 296 alphanumeric characters**, but for
      reliable scanning keep payloads under **500 characters**. For larger payloads
      store a reference ID and fetch details server‑side.
    question: What is the maximum data I can store in a QR code?
  - answer: Yes. You can set size, position, foreground/background colors, and even
      add a logo overlay. Stick to high‑contrast colors for best scan results.
    question: Can I customize the QR code’s visual appearance?
  - answer: For documents over 50 pages, expect a few seconds per file. Use batch
      processing, reuse the `Signature` instance, and monitor JVM heap size.
    question: How should I handle large‑document signing efficiently?
  type: FAQPage
tags:
- java
- word-documents
- qr-code
- digital-signature
- groupdocs
title: 使用 Java 在 Word 文件中建立 QR Code 簽章
type: docs
url: /zh-hant/java/digital-signatures/groupdocs-signature-java-word-documents-qr-code/
weight: 1
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 在 Word 文件中使用 Java 建立 QR Code 簽章

是否曾花費數小時手動簽署文件，卻仍在尋找更快、更可靠的方式？您只需幾行 Java 程式碼，即可在 Word 文件中**建立 QR code 簽章**。無論是自動化合約工作流程、管理法律文件，或是構建以行動裝置為先的批准入口，QR code 簽章都能提供即時、可掃描的驗證，適用於任何智慧手機。在本教學中，您將學習如何設定 GroupDocs.Signature for Java、配置 QR code 選項，並將 URL、時間戳記或 JSON 資料等豐富資訊嵌入 Word 檔案。完成後，您即可大規模簽署文件、減少人工操作，並提升合規性。

## 快速解答
- **需要哪個函式庫？** GroupDocs.Signature for Java (v23.12+)。  
- **需要多少行程式碼？** 兩行 QR 產生程式碼加上少量設定行。  
- **我也可以簽署 PDF 嗎？** 可以 – 同一套 API 可用於 PDF、Excel、PowerPoint 以及影像。  
- **需要商業授權嗎？** 僅在正式環境需要；開發階段可使用免費試用或臨時授權。  
- **可以儲存什麼資料？** 最多約 4 k 字元（URL、JSON、ID），但為確保掃描可靠性，建議保持在 500 字元以下。

## 什麼是建立 QR code 簽章？

**建立 QR code 簽章**是一種可掃描的 2‑D 條碼，嵌入於文件中，用以表示數位簽章或驗證資料。使用者掃描 QR code 後，會讀取並驗證編碼資料（通常是 URL 或 token），從而證明文件的真偽，且不需特別軟體。

## 為何使用 GroupDocs.Signature for Java 來加入 QR code？

GroupDocs.Signature 支援**超過 50 種輸入與輸出格式**，可在不將整個文件載入記憶體的情況下處理數百頁檔案，並提供流暢的 API，讓您**以程式方式在毫秒內簽署 Word**檔案。此函式庫亦內建 QR、Aztec、DataMatrix 與 PDF417 條碼產生功能，成為現代行動優先驗證的一站式解決方案。

## 前置條件

### 必要的函式庫與相依性
- **GroupDocs.Signature for Java** 版本 **23.12** 或更新（唯一的外部相依性）。

### 環境設定需求
- **JDK 8+**（建議在正式環境使用 Java 11 或 17）。
- **IDE**（自行選擇，如 IntelliJ IDEA、Eclipse、VS Code）。
- **建置工具** – Maven 或 Gradle（以下範例兩者皆適用）。

### 知識前提
- 基本的 Java 語法與檔案 I/O 處理。
- 熟悉 Maven/Gradle 的相依性聲明（我們將示範完整片段）。

## 設定 GroupDocs.Signature for Java

選擇您的建置系統，並依照下列方式加入相依性。以下佔位符代表原始程式碼區塊，請保持不變。

**Maven**

```java
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

**Gradle**

```java
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

**Direct Download**

偏好手動管理？直接從[GroupDocs.Signature for Java 版本發布](https://releases.groupdocs.com/signature/java/)下載 JAR，並加入專案的 classpath。

### 取得授權
- **免費試用：** 適合原型開發；核心功能皆可使用。  
- **臨時授權：** 短期開發可取得完整功能。  
- **商業授權：** 正式部署時必須取得。

**專業提示：** 先使用免費試用，然後在進入正式環境前申請臨時授權。這樣可在不預付費用的情況下驗證工作流程。

### 基本初始化

`Signature` 物件是所有簽署操作的入口。它實作 `AutoCloseable`，因此您可以安全地使用 try‑with‑resources 區塊。

```java
```java
Signature signature = new Signature("path/to/your/document");
```
```

## 實作指南：使用 QR code 簽署 Word 文件

以下逐步說明每個步驟，並在需要時加入定義錨點與直接回答。

### 如何為 Word 檔案初始化 Signature 物件？

在 try‑with‑resources 區塊內使用 `new Signature("source.docx")` 載入來源文件；此物件會為修改做準備，且在區塊結束時自動釋放資源。

```java
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleDocX.docx";
Signature signature = new Signature(filePath);
```
```

`Signature` 類別在記憶體中代表單一文件，提供新增、搜尋與驗證簽章的方法。它支援 `.docx`、`.doc` 以及許多其他格式。

### 如何設定 QR code 簽章選項？

建立 `QrCodeSignOptions` 實例，設定編碼文字、條碼類型與位置。以下程式碼示範最小配置。

```java
```java
QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100); // X-axis position in pixels
signOptions.setTop(100);  // Y-axis position in pixels
```
```

`QrCodeSignOptions` 類別封裝產生與放置 QR code 簽章所需的所有設定，包括編碼文字、條碼類型、尺寸、顏色，以及文件內的座標位置。

#### 自訂外觀
您還可以進一步調整尺寸、邊距與顏色：

```java
```java
QrCodeSignOptions signOptions = new QrCodeSignOptions("https://yourapp.com/verify/doc-12345");
```
```

**為何重要：** 150 px 的正方形 QR code，前景為黑色、背景為白色，可在螢幕與列印時取得超過 99 % 的掃描成功率。

### 如何設定已簽署文件的輸出選項？

在呼叫 `sign` 之前，先定義目標格式與覆寫行為。

```java
```java
WordProcessingSaveOptions saveOptions = new WordProcessingSaveOptions();
saveOptions.setFileFormat(WordProcessingSaveFileFormat.Odt);
saveOptions.setOverwriteExistingFiles(true);
```
```

`WordProcessingSaveOptions` 類別定義已簽署的 Word 文件如何儲存，您可以指定輸出格式（DOCX、ODT 等）、是否覆寫現有檔案，以及其他檔案層級的偏好設定。

如果需要開源格式，可切換為 `OutputType.ODT`：

```java
```java
saveOptions.setFileFormat(WordProcessingSaveFileFormat.Docx);
```
```

### 如何使用 QR code 簽署並儲存文件？

`sign` 方法會套用 QR code 並一次寫入輸出檔案。

```java
```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SaveSignedOutputType/SampleDocX.odt";
signature.sign(outputFilePath, signOptions, saveOptions);
```
```

`Signature` 物件的 `sign` 方法接受目標路徑、已配置的簽章選項，以及可選的儲存選項，然後將 QR code 嵌入文件並將結果寫入指定位置。

**What happens:**
1. 函式庫讀取來源文件。  
2. 根據 `QrCodeSignOptions` 產生 QR code。  
3. 在指定座標插入圖形。  
4. 將修改後的檔案儲存至您提供的路徑。

### 簽署過程中應如何處理錯誤？

將簽署邏輯包在 try‑catch 區塊中，以捕捉檔案遺失、路徑無效或授權問題。

```java
```java
try {
    signature.sign(outputFilePath, signOptions, saveOptions);
    System.out.println("Document signed successfully!");
} catch (Exception e) {
    System.err.println("Signing failed: " + e.getMessage());
}
```
```

捕捉 `Exception` 可確保任何執行時問題（如檔案遺失、路徑無效或授權問題）都能優雅地回報，避免應用程式在正式環境中當機。

## 常見使用情境與實務應用

### 自動化合約管理
某 SaaS 平台每月簽署**超過 500 份合約**，透過產生包含合約 ID 與驗證 URL 的唯一 QR code。收件人掃描後即可在入口網站查看合約狀態，省去手動 email 來回。

### 員工證書發放
人力資源部門在培訓證書的 QR code 中嵌入員工 ID 與發證日期。掃描 QR 後即可即時對照內部資料庫驗證真偽，將詐騙率降低**超過 80 %**。

### 批准工作流程自動化
每位批准者的 QR code 內存放其員工編號、角色與時間戳記。系統在稽核時讀取 QR，提供防篡改的痕跡，且無需額外資料庫查詢。

### 發票與收據簽署
財務團隊在發票上加入指向付款入口的 QR code。掃描後，QR 會導向付款者至安全的付款頁面，將處理時間縮短**30 %**，並降低發票詐騙風險。

## 生產環境最佳實踐

### 安全性考量
- **絕不要嵌入明文密碼**；請使用可在伺服器端解析的 token 或參考 ID。  
- **所有 URL 必須使用 HTTPS**；避免使用 HTTP，以防止中間人攻擊。  
- **設定 token 有效期限**（例如 24 小時有效的 JWT），以應對時間敏感的文件。

### 效能最佳化
- **批次處理：** 保持單一 `Signature` 實例存活，遍歷檔案以避免 JVM 重複啟動。  
- **記憶體管理：** 對於大於 50 MB 的文件，請逐一處理，並在每個檔案完成後釋放 `Signature` 物件。  
- **放置位置重要：** 將 QR code 放在頁面底部，可減少版面重排並提升速度。

```java
```java
List<String> documents = getDocumentPaths();
for (String docPath : documents) {
    Signature sig = new Signature(docPath);
    // Configure and sign
    sig.dispose();
}
```
```

### QR code 放置技巧
- **列印安全性：** QR code 與頁邊至少保留 0.5 英吋，以免被裁切。  
- **尺寸建議：** 最小 150 × 150 px，確保列印媒介上的掃描可靠性。  
- **多頁文件：** 迴圈處理每頁，並為每個位置建立新的 `QrCodeSignOptions`。

```java
```java
for (Document doc : documents) {
    Signature sig = new Signature(doc.getPath());
    sig.sign(outputPath, signOptions, saveOptions);
    sig.dispose();
}
```
```

## 進階設定選項

### 如何在單一文件中加入多個 QR code？
為每個位置建立獨立的 `QrCodeSignOptions` 物件，並重複呼叫 `sign`。

```java
```java
// First QR code
QrCodeSignOptions sign1 = new QrCodeSignOptions("Approver 1");
sign1.setLeft(100);
sign1.setTop(100);

// Second QR code
QrCodeSignOptions sign2 = new QrCodeSignOptions("Approver 2");
sign2.setLeft(300);
sign2.setTop(100);

// Apply both
signature.sign(outputPath, sign1, saveOptions);
signature.sign(outputPath, sign2, saveOptions);
```
```

### 支援哪些其他條碼類型？
除了 QR，您也可以透過變更 `setEncodeType()` 產生 **Aztec**、**DataMatrix** 或 **PDF417** 條碼。

### 如何根據頁面大小計算動態位置？
透過 `Signature.getDocumentInfo()` 取得頁面尺寸，並以程式方式計算座標。

```java
```java
// Get document info
DocumentInfo docInfo = signature.getDocumentInfo();
int pageWidth = docInfo.getWidth();
int pageHeight = docInfo.getHeight();

// Center the QR code
int qrSize = 100;
signOptions.setLeft((pageWidth - qrSize) / 2);
signOptions.setTop((pageHeight - qrSize) / 2);
```
```

`Signature.getDocumentInfo()` 會回傳包含頁面尺寸等中繼資料的 `DocumentInfo` 物件，可用於根據每頁實際大小計算簽章的精確座標。

## 常見問題排除

### QR code 未顯示
- 確認 `setLeft`/`setTop` 位於頁面範圍內（A4 約 595 × 842 px，72 DPI）。  
- 確保前景與背景顏色對比足夠（黑底白字）。  
- 若條碼過小導致掃描困難，請增大寬度/高度。

### 初始化 Signature 時出現 “File not found”
- 開發期間使用絕對路徑，或使用 `Paths.get(...)` 檢查相對路徑是否正確。  
- 確認來源檔案未被其他程序鎖定。

### 輸出檔案損毀
- 再次確認 `setFileFormat` 與目標副檔名相符。  
- 在簽署前關閉可能仍佔用檔案的任何串流。

### QR code 含有錯誤資料
- 在簽署前先印出傳入 `QrCodeSignOptions` 的字串，以確認編碼正確。  
- 除非明確設定 UTF-8 編碼，否則避免使用非 ASCII 字元。

### 大型文件效能緩慢
- 以批次方式處理文件（參見程式碼區塊 10）。  
- 盡量避免將 QR code 放在複雜的表格內，會導致大量版面重新計算。

## 常見問與答

**Q: 我可以簽署 PDF 而非 Word 文件嗎？**  
A: 可以。GroupDocs.Signature 支援 PDF、Excel、PowerPoint、影像及許多其他格式。只需將 `setFileFormat` 改為目標輸出類型即可。

**Q: 加入 QR code 簽章後，如何驗證？**  
A: 使用函式庫的 `SearchQrCodeSignatures` 方法尋找 QR code，並將嵌入的資料與後端服務驗證。

**Q: QR code 最多能儲存多少資料？**  
A: 標準 QR code 最多可容納 **4 296 個英數字元**，但為確保掃描可靠性，建議將有效負載控制在 **500 個字元** 以內。若需更大資料，請儲存參考 ID，並在伺服器端取得詳細資訊。

**Q: 我可以自訂 QR code 的視覺外觀嗎？**  
A: 可以。您可以設定尺寸、位置、前景/背景顏色，甚至加入標誌覆蓋。請使用高對比度顏色以獲得最佳掃描效果。

**Q: 如何有效率地簽署大型文件？**  
A: 超過 50 頁的文件每個大約需要數秒。請使用批次處理、重複利用 `Signature` 實例，並監控 JVM 堆積大小。

**Q: QR 簽章在轉換為 PDF 後仍會保留嗎？**  
A: 完全會。QR code 以圖形形式嵌入，於不同格式間轉換時仍保持完整，只要確保解析度足夠。

**Q: 我可以簽署儲存在雲端（如 S3）的文件嗎？**  
A: 可以。先將檔案下載至暫存本機路徑，完成簽署後再上傳回 S3。此函式庫僅支援本機檔案操作。

**Q: 簽署後若有人修改文件會怎樣？**  
A: QR 圖形本身不會變動，但無法偵測篡改。建議結合基於雜湊的驗證或數位憑證，以實現更完整的完整性檢查。

**Q: 開發與正式環境需要不同的授權嗎？**  
A: 開發階段可使用免費試用或臨時授權。正式部署則需依照 GroupDocs 條款取得商業授權。

**Q: 沒有 Java 環境的收件人也能掃描這些 QR code 嗎？**  
A: 可以。QR code 採用開放標準，任何智慧手機相機或 QR 讀取應用程式皆可解碼。Java 只在*建立*簽章時使用。

## 資源

- [GroupDocs.Signature for Java 版本發布](https://releases.groupdocs.com/signature/java/)
- [GroupDocs.Signature for Java 文件說明](https://docs.groupdocs.com/signature/java/)
- [GroupDocs.Signature API 參考文件](https://reference.groupdocs.com/signature/java/)
- [最新 GroupDocs.Signature 版本發布](https://releases.groupdocs.com/signature/java/)
- [購買 GroupDocs.Signature](https://purchase.groupdocs.com/buy)
- [GroupDocs 簽章免費試用](https://releases.groupdocs.com/signature/java/)
- [申請臨時授權](https://purchase.groupdocs.com/temporary-license/)
- [GroupDocs 論壇支援](https://forum.groupdocs.com/c/signature/)

## 結論

現在您已擁有完整、可投入生產的路線圖，能在 Word 文件中使用 Java 與 GroupDocs.Signature **建立 QR code 簽章**。從基礎設定到批次處理，從安全最佳實踐到進階條碼類型，所有需求皆已涵蓋。先從免費試用開始，嘗試不同的資料負載，並將簽署步驟整合至現有的文件產生流程。祝開發順利，簽署安全！

---

**最後更新：** 2026-06-26  
**測試環境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs  

{{< blocks/products/products-backtop-button >}}

## 相關教學

- [Java QR Code 簽章函式庫 - 完整 GroupDocs 教學](/signature/java/qr-code-signatures/)
- [在 Java 中載入與儲存文件 - 完整 GroupDocs.Signature 教學](/signature/java/document-loading-saving/)
- [如何在 Java 中加入數位簽章](/signature/java/digital-signatures/groupdocs-signature-java-digital-signing-guide/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}