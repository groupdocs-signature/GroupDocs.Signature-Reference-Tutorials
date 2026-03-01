---
categories:
- Java Development
- Document Processing
date: '2026-03-01'
description: 學習如何使用 Java 及 GroupDocs.Signature 讀取 QR 碼 PDF 檔案。逐步指南、程式碼範例、故障排除與實務案例。
keywords: read qr code pdf, Java barcode verification PDF, GroupDocs barcode search
  tutorial, extract barcode data from PDF Java, Java PDF barcode scanner
lastmod: '2026-03-01'
linktitle: Search PDF Barcodes Java
tags:
- barcode-search
- pdf-processing
- groupdocs
- java-tutorial
- document-verification
title: 如何使用 Java 與 GroupDocs.Signature 讀取 QR 碼 PDF
type: docs
url: /zh-hant/java/barcode-signatures/java-pdf-barcode-search-groupdocs-signature-api/
weight: 1
---

# 如何使用 Java 讀取 QR code PDF

## 介紹

是否曾需要從數百張 PDF 發票、運送標籤或庫存文件中擷取條碼資訊？手動逐頁掃描既繁瑣又容易出錯。無論您是要建立自動化文件處理系統，還是驗證產品真偽，在 PDF 中有效找出條碼都是一大挑戰。

在本指南中，您將學會如何使用 **GroupDocs.Signature API** 高效 **讀取 QR code PDF** 文件。這個功能強大的 API 能把原本需要數小時的手動工作，縮減為幾行程式碼。您可以掃描整份文件、定位特定條碼類型（如 QR code 或 Code128），並自動擷取其資料。

**您將學到的內容：**
- 在數分鐘內為 Java 設定 GroupDocs.Signature  
- 在 PDF 文件中搜尋條碼簽章  
- 設定搜尋選項以取得精確、目標化的結果  
- 處理不同條碼類型（QR code、EAN、Code128 等）  
- 疑難排解常見問題並優化效能  

讓我們開始吧！

## 快速答覆
- **GroupDocs.Signature 能從 PDF 讀取 QR code 嗎？** 能，支援 QR、Data Matrix、PDF417 以及多種 1D 條碼。  
- **正式環境需要授權嗎？** 需要商業授權；提供免費試用供評估。  
- **需要哪個 Java 版本？** Java 8+（建議使用 Java 11+）。  
- **如何限制搜尋特定頁面？** 使用 `BarcodeSearchOptions.setAllPages(false)` 並設定 `setPageNumber()`。  
- **API 在批次處理時是否為執行緒安全？** 是，只要每個執行緒建立獨立的 `Signature` 實例即可。

## 為什麼要在 PDF 中搜尋條碼？

在進入技術細節之前，先說明此功能在實務上的重要性：

**常見商業情境**
- **發票處理** – 自動從供應商發票中擷取訂單編號或追蹤碼。  
- **庫存管理** – 掃描產品目錄，擷取 SKU 條碼以更新資料庫。  
- **運輸與物流** – 驗證運送清單中的包裹追蹤碼。  
- **文件驗證** – 透過檢查內嵌的安全條碼來驗證已簽署文件。  
- **醫療紀錄** – 從醫療文件中擷取患者 ID 或處方碼。  

GroupDocs.Signature API 會處理所有繁重工作——您不必擔心影像處理、條碼解碼演算法或 PDF 呈現的複雜性，一切皆內建完成。

## 前置條件

在開始本教學前，請先確保以下項目已備妥：

### 必要的函式庫與相依性

您需要在 Java 專案中加入 GroupDocs.Signature 函式庫。以下示範如何使用 Maven 或 Gradle 加入：

**Maven:**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle:**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

**備註：** 請隨時於 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) 查看最新版本。使用最新版本可確保取得錯誤修正與新功能。

### 環境設定

- **JDK 8 或以上** – GroupDocs.Signature 最低需求為 Java 8（建議使用 Java 11+ 以獲得更佳效能）。  
- **IDE** – 任何文字編輯器皆可，但 IntelliJ IDEA 或 Eclipse 能提供自動完成與除錯功能，讓開發更順暢。  
- **PDF 文件** – 準備一份含條碼的測試 PDF（發票、運送標籤或產品目錄皆可）。

### 知識前置條件

您應該熟悉以下概念：
- 基本的 Java 語法與物件導向概念  
- 使用 `try‑catch` 區塊處理例外  
- 在 IDE 中使用外部函式庫  

若您對第三方 Java 函式庫不熟悉，別擔心，我們會一步步帶您完成。

## 為 Java 設定 GroupDocs.Signature

只需幾分鐘即可完成 GroupDocs.Signature 的設定。以下為完整流程：

### 步驟 1：加入相依性

使用 Maven 或 Gradle 加入函式庫（請參考上方程式碼）。加入相依性後，重新整理專案以下載 JAR 檔。

### 步驟 2：取得授權

GroupDocs 提供多種授權方式：

- **免費試用** – 適合測試。可從 [GroupDocs releases](https://releases.groupdocs.com/signature/java/) 下載。  
- **臨時授權** – 透過 [Temporary License Page](https://purchase.groupdocs.com/temporary-license/) 取得 30 天完整存取權。  
- **商業授權** – 正式上線時，請於 [GroupDocs Purchase](https://purchase.groupdocs.com/) 購買授權。  

**專業小技巧：** 先使用免費試用建立概念驗證，若 API 符合需求再升級授權。

### 步驟 3：基本初始化

以下示範如何建立 `Signature` 物件以處理 PDF：

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed.pdf"; // Replace with your PDF path
Signature signature = new Signature(filePath);
```

`Signature` 類別是主要入口點。它會將 PDF 載入記憶體，並提供搜尋、驗證與擷取簽章資料（含條碼）的各種方法。

**重要提醒：** 請確認檔案路徑正確且 PDF 確實存在。常見新手錯誤是 Windows 路徑未跳脫反斜線（正確寫法 `C:\\Documents\\file.pdf`，而非 `C:\Documents\file.pdf`）。

## 實作指南

接下來的重點是撰寫程式碼，搜尋 PDF 中的條碼。

### 在文件中搜尋條碼簽章

本節說明如何掃描 PDF 並找出所有條碼簽章，並以易於理解的步驟說明每段程式碼。

#### 步驟 1：初始化 Signature 物件

先載入 PDF 文件：

```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/sample_signed.pdf"; // Replace with actual file path
Signature signature = new Signature(filePath);
```

**程式說明**  
`Signature` 類別會開啟 PDF 並為後續處理作好準備。可類比為在文字編輯器中開啟檔案——將文件載入記憶體以便操作。

**實務提醒**  
若處理使用者上傳的 PDF，務必先驗證檔案路徑與檔案是否存在，才能建立 `Signature` 物件，避免之後出現難以理解的錯誤。

#### 步驟 2：建立 BarcodeSearchOptions

設定條碼搜尋方式：

```java
import com.groupdocs.signature.options.search.BarcodeSearchOptions;

// Configure options for searching barcodes
BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setAllPages(true); // Search every page in the document
```

**關鍵設定選項**

- `setAllPages(true)`: 掃描所有頁面。若只想檢查特定頁面，請設為 `false` 並搭配 `setPageNumber()`。  
- **為什麼重要**：若您只在第 1 頁的發票上放置條碼，搜尋全部頁面會浪費資源；若是多頁的運送清單，則需要 `setAllPages(true)`。

**專業小技巧**：您也可以依條碼類型過濾（請參考下方 **支援的條碼類型** 章節），在已知格式時可加速搜尋。

#### 步驟 3：執行搜尋並處理結果

現在執行搜尋並處理回傳結果：

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.util.List;

try {
    // Execute the barcode search
    List<BarcodeSignature> signatures = signature.search(BarcodeSignature.class, options);
    
    // Check if any barcodes were found
    if (signatures.isEmpty()) {
        System.out.println("No barcode signatures found in the document.");
    } else {
        System.out.println("Found " + signatures.size() + " barcode signature(s):\n");
        
        // Loop through each barcode and display details
        for (BarcodeSignature barcodeSignature : signatures) {
            System.out.println("----------------------------------------");
            System.out.println("Barcode Type: " + barcodeSignature.getEncodeType().getTypeName());
            System.out.println("Barcode Text: " + barcodeSignature.getText());
            System.out.println("Page Number: " + barcodeSignature.getPageNumber());
            System.out.println("Position: X=" + barcodeSignature.getLeft() + 
                             ", Y=" + barcodeSignature.getTop());
            System.out.println("Size: Width=" + barcodeSignature.getWidth() + 
                             ", Height=" + barcodeSignature.getHeight());
            System.out.println("----------------------------------------\n");
        }
    }
} catch (Exception e) {
    System.err.println("Error searching for barcodes: " + e.getMessage());
    e.printStackTrace();
} finally {
    // Always dispose of the signature object to free resources
    if (signature != null) {
        signature.dispose();
    }
}
```

**程式說明**

1. **執行搜尋** – `signature.search()` 會掃描 PDF，回傳 `BarcodeSignature` 物件清單。  
2. **空集合檢查** – 確認真的找到條碼，避免 NullPointerException。  
3. **資料擷取** – 針對每個條碼，我們會取得：  
   - **Type** – 條碼格式（QR Code、Code128、EAN13 等）  
   - **Text** – 解碼後的資料（訂單號、追蹤碼、SKU 等）  
   - **Location** – 頁碼與 X/Y 座標  
   - **Dimensions** – 寬度與高度（可用於驗證）  
4. **錯誤處理** – `try‑catch` 可防止因 PDF 損毀、檔案缺失等問題導致程式崩潰。  
5. **資源釋放** – `finally` 區塊確保 `Signature` 物件正確釋放，釋放記憶體。

**實務應用**  
假設您在處理運送標籤，會取 `getText()`（追蹤號碼）存入資料庫。頁碼則可告訴您在批次文件中哪一張標籤對應哪筆出貨。

### 依條碼類型過濾

您可以透過指定條碼類型來加速搜尋：

```java
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSearchOptions options = new BarcodeSearchOptions();
options.setEncodeType(BarcodeTypes.QR); // Only search for QR codes
options.setAllPages(true);
```

**何時使用過濾**  
若您知道發票只會出現 Code128 條碼，使用類型過濾可在大型文件上減少 30‑50 % 的處理時間。

## 支援的條碼類型

GroupDocs.Signature 能偵測多種條碼格式，以下列出可搜尋的類型：

**1D 條碼（線性）**
- **Code128** – 常見於運送與包裝  
- **Code39** – 用於汽車與防衛產業  
- **EAN13/EAN8** – 零售商品條碼（您在每件商品上都會看到）  
- **UPC‑A/UPC‑E** – 北美零售標準  
- **Interleaved2of5** – 倉儲與配送  

**2D 條碼（矩陣）**
- **QR Code** – 最流行的條碼，用於 URL、Wi‑Fi 密碼、付款資訊等  
- **Data Matrix** – 小尺寸物件（電子元件）常用的緊湊格式  
- **PDF417** – 政府身分證、登機證、駕照等  
- **Aztec Code** – 交通票證  

**依類型過濾**（前述範例）可讓您聚焦於所需的特定格式。

## 真實案例

以下是開發者在實務中使用條碼搜尋的情境：

### 1. 自動化發票處理
**情境** – 會計部門每日收到超過 500 份供應商 PDF 發票。  
**解決方案** – 為每份 PDF 掃描 Code39 條碼（含發票號碼），自動比對 ERP 系統中的採購單，省去人工輸入與錯誤。

```java
// Pseudo-code workflow
for (PDF invoice : invoiceBatch) {
    List<BarcodeSignature> barcodes = searchBarcodes(invoice);
    String invoiceNumber = barcodes.get(0).getText();
    updateERPSystem(invoiceNumber, invoice);
}
```

### 2. 倉庫庫存更新
**情境** – 倉庫收到的貨物附有 PDF 裝箱單，內含 EAN13 SKU 條碼。  
**解決方案** – 從裝箱單擷取所有條碼，自動更新庫存數量，並標記異常項目供人工審核。

### 3. 文件驗證
**情境** – 法律文件內嵌 QR Code，內含加密簽章以驗證真偽。  
**解決方案** – 在已簽署合約中搜尋 QR Code，解碼簽章資料，並對照受信任的憑證機構驗證，確保文件未被竄改。

### 4. 醫療紀錄管理
**情境** – 醫院的 PDF 檢驗報告內含 Code128 條碼，代表檢體 ID。  
**解決方案** – 自動擷取檢體 ID，將實驗結果連結至病患的醫院資訊系統（HIS）。

## 常見問題與解決方案

以下列出您可能會遇到的問題與對應的解法：

### 問題 1：「找不到條碼」（實際上確實存在）

**可能原因**
- 條碼影像品質太低（模糊、像素不足）  
- PDF 為影像型，但條碼尺寸過小  
- 搜尋的條碼類型不正確  

**解決方式**
1. **檢查影像解析度** – 條碼至少需要 200 DPI 才能可靠偵測。若是掃描文件，建議使用 300 DPI 以上。  
2. **移除類型過濾** – 先不設定 `setEncodeType()`，搜尋所有條碼類型，之後再根據結果縮小範圍。  
3. **驗證條碼品質** – 用 Adobe Acrobat 放大檢視；若您看起來已模糊，API 也會難以辨識。

### 問題 2：大型 PDF 出現 `OutOfMemoryError`

**原因** – 載入 500 頁以上、解析度高的 PDF 會佔用大量記憶體。  

**解決方式**
1. **分批處理頁面** – 不使用 `setAllPages(true)`，改為一次處理 50 頁：

```java
for (int startPage = 1; startPage <= totalPages; startPage += 50) {
    BarcodeSearchOptions options = new BarcodeSearchOptions();
    options.setPageNumber(startPage);
    options.setPagesSetup(new PagesSetup());
    options.getPagesSetup().setLastPage(Math.min(startPage + 49, totalPages));
    
    List<BarcodeSignature> batchResults = signature.search(BarcodeSignature.class, options);
    // Process results...
}
```

2. **增加 JVM 堆積大小** – 在執行指令加入 `-Xmx4g`，分配 4 GB 記憶體（依需求調整）。

### 問題 3：多頁文件效能緩慢

**原因** – 逐頁搜尋所有頁面會花費時間，特別是 PDF417 等複雜條碼。  

**解決方式**
1. **平行處理** – 若條碼固定在特定頁（例如發票第 1 頁），僅搜尋該頁即可。  
2. **快取結果** – 若同一文件會被多次處理，將條碼資料快取起來，避免重複掃描。  
3. **使用 SSD** – 讀取大型 PDF 時 I/O 速度很關鍵，SSD 可比 HDD 快 60‑70 %。

### 問題 4：偽陽性（將隨機圖形誤判為條碼）

**原因** – 表格、格線或線條圖案可能被誤認為條碼。  

**解決方式** – 透過檢查解碼後文字的長度與格式來驗證結果：

```java
for (BarcodeSignature barcode : signatures) {
    String text = barcode.getText();
    
    // Example: Invoice numbers are always 10 digits
    if (text.matches("\\d{10}")) {
        // Valid invoice number
        processBarcode(barcode);
    } else {
        System.out.println("Skipping invalid barcode: " + text);
    }
}
```

## 大文件效能最佳化技巧

需要一次處理上千份 PDF？以下提供優化建議：

### 1. 批次處理策略

不要一次只處理單一檔案，使用執行緒池同時處理多份 PDF：

```java
ExecutorService executor = Executors.newFixedThreadPool(4); // 4 parallel threads

for (String pdfPath : pdfFiles) {
    executor.submit(() -> {
        try (Signature sig = new Signature(pdfPath)) {
            List<BarcodeSignature> results = sig.search(BarcodeSignature.class, options);
            // Process results...
        } catch (Exception e) {
            e.printStackTrace();
        }
    });
}

executor.shutdown();
executor.awaitTermination(1, TimeUnit.HOURS);
```

**效能提升** – 在四核心機器上，處理 1 000 份檔案的時間可從約 2 小時縮減至約 30 分鐘。

### 2. 縮小搜尋範圍

若業務邏輯允許，可限制搜尋區域：

```java
// Only search the top‑right corner where barcodes are typically placed
options.setRectangle(new Rectangle(400, 50, 150, 150)); // X, Y, Width, Height
```

**效能提升** – 在條碼位置固定的文件上，可提升 40‑60 % 的速度。

### 3. 監控記憶體使用

長時間執行的批次程序請監控堆積使用情況，必要時手動觸發垃圾回收：

```java
Runtime runtime = Runtime.getRuntime();
long usedMemory = runtime.totalMemory() - runtime.freeMemory();

if (usedMemory > (runtime.maxMemory() * 0.8)) {
    System.gc(); // Suggest garbage collection
}
```

## 最佳實踐

以下為上線前的建議做法：

### 1. 必須釋放 Signature 物件

使用 try‑with‑resources（Java 7 以上）自動關閉資源：

```java
try (Signature signature = new Signature(filePath)) {
    // Your search code here...
} // Automatically disposed
```

### 2. 驗證輸入檔案

處理前先檢查檔案是否存在且為有效的 PDF：

```java
File pdfFile = new File(filePath);
if (!pdfFile.exists() || !pdfFile.canRead()) {
    throw new FileNotFoundException("PDF not found or not readable: " + filePath);
}

// Optional: Verify it's actually a PDF (check magic bytes)
```

### 3. 記錄條碼偵測結果

為除錯與稽核目的，將偵測結果寫入日誌：

```java
Logger logger = Logger.getLogger(BarcodeSearcher.class.getName());

for (BarcodeSignature barcode : signatures) {
    logger.info(String.format("Detected %s barcode '%s' on page %d at (%.2f, %.2f)",
        barcode.getEncodeType().getTypeName(),
        barcode.getText(),
        barcode.getPageNumber(),
        barcode.getLeft(),
        barcode.getTop()));
}
```

### 4. 處理多種條碼格式

不同產業使用不同標準，請讓程式具備彈性：

```java
switch (barcode.getEncodeType().getTypeName()) {
    case "QR":
        // QR codes might contain URLs or JSON data
        processQRCode(barcode.getText());
        break;
    case "Code128":
        // Code128 typically contains alphanumeric order/tracking numbers
        processTrackingNumber(barcode.getText());
        break;
    default:
        logger.warning("Unexpected barcode type: " + barcode.getEncodeType());
}
```

### 5. 使用真實文件測試

不要只用完美的範例 PDF 測試，務必使用實際上線文件：
- 帶有咖啡漬的掃描發票  
- 含雜訊的傳真運送標籤  
- 以手機拍照後轉成 PDF 的低解析度檔案  

這樣才能發現在示範環境中不會出現的邊緣案例。

## 常見問答

**Q: 沒有授權可以讀取 QR code PDF 嗎？**  
A: 免費試用可用於評估讀取 QR code PDF，但正式上線必須購買商業授權。

**Q: API 支援受密碼保護的 PDF 嗎？**  
A: 支援。建立 `Signature` 物件時可傳入密碼，例如 `new Signature(filePath, "password")`。

**Q: 如何提升低解析度掃描的偵測率？**  
A: 提高原始掃描的 DPI（最低 200 DPI），並使用條碼類型過濾以減少偽陽性。

**Q: 搜尋是否為執行緒安全，可平行處理？**  
A: 每個執行緒應使用自己的 `Signature` 實例；在此使用方式下 API 為執行緒安全。

**Q: 本教學驗證使用的 GroupDocs.Signature 版本為何？**  
A: 以 GroupDocs.Signature 23.12 為驗證基礎。

## 結論

您已學會如何使用 Java 以及 GroupDocs.Signature API **讀取 QR code PDF** 文件。以下為本篇重點回顧：

✅ **設定** – 加入 GroupDocs.Signature 相依性與授權方式  
✅ **實作** – 完整程式碼示範搜尋、擷取與處理條碼資料  
✅ **條碼類型** – 了解支援的 1D 與 2D 格式  
✅ **真實案例** – 發票處理、庫存管理、文件驗證、醫療紀錄等應用  
✅ **疑難排解** – 解決記憶體錯誤、偽陽性與效能瓶頸  
✅ **效能** – 大規模文件處理的最佳化技巧  

GroupDocs.Signature API 讓 PDF 解析與條碼偵測的複雜度全部抽象化，讓您專注於業務邏輯。無論是自動化發票處理、驗證運送標籤，或是擷取庫存資料，您現在都有一套可靠的解決方案。

---

**最後更新：** 2026-03-01  
**測試版本：** GroupDocs.Signature 23.12  
**作者：** GroupDocs