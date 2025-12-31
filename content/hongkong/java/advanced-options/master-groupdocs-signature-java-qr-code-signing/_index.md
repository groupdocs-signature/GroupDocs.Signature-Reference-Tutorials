---
categories:
- Java Development
date: '2025-12-31'
description: 學習如何使用 GroupDocs.Signature for Java 在 PDF 中以 Java 產生 QR 代碼簽章。包括 Maven
  依賴設定、定位方式及上線實務技巧。
keywords: java generate qr code, groupdocs signature java, maven dependency groupdocs,
  QR code document signing Java, add QR code to PDF Java
lastmod: '2025-12-31'
linktitle: QR Code Signing Java Guide
tags:
- QR codes
- PDF signing
- digital signatures
- document security
title: Java 產生 QR Code：Java 中的 QR Code 簽署指南
type: docs
url: /zh-hant/java/advanced-options/master-groupdocs-signature-java-qr-code-signing/
weight: 1
---

# java generate qr code: Java 中的 QR Code 簽署 – 完整實作

你可能已經注意到，數位簽章現在無處不在——從合約到發票。但傳統的簽署方式往往笨重，且未必提供現代企業所需的驗證功能。這就是 **java generate qr code** 簽章的用武之地。

在本指南中，你將學會如何在 Java 中實作 QR Code 簽署、將這些簽章精確定位到所需位置，並避免大多數開發者常犯的陷阱。無論你是構建合約管理系統，或只是需要以程式方式保護 PDF，本教學都能幫你達成目標。

我們將使用 **GroupDocs.Signature for Java**（一個處理繁重工作負載的強大函式庫），但其概念同樣適用於任何 QR Code 簽署實作。

## 快速回答
- **哪個函式庫可以在 Java 中加入 QR Code 簽章？** GroupDocs.Signature for Java  
- **哪個建置工具支援 Maven 依賴？** Maven（請參考 *maven dependency groupdocs*）  
- **我可以在特定頁面上放置 QR Code 嗎？** 可以，使用對齊與頁碼選項即可  
- **生產環境需要授權嗎？** 需要，必須購買商業版 GroupDocs 授權  
- **簽署後 QR Code 仍可掃描嗎？** 當尺寸 ≥ 100 × 100 px 且使用適當邊距時，絕對可以  

## 你將學會

完成本指南後，你將能夠：

- 在 Java 專案中設定 QR Code 簽署（Maven、Gradle 或直接下載）  
- 在文件的特定位置（角落、中心、客製化對齊）加入 QR Code  
- 在問題變成生產故障前先處理常見實作議題  
- 為文件處理工作流程優化效能  
- 將這些技巧套用到真實的商業情境  

## 前置條件

在進入程式碼之前，請確保你已具備以下條件：

- **GroupDocs.Signature for Java Library** – 版本 23.12 或更新（以下會說明安裝方式）  
- **Java Development Kit** – JDK 8 或以上（大多數生產環境使用 JDK 11+）  
- **建置工具** – Maven 或 Gradle 用於相依管理  
- **基本的 Java 知識** – 能熟悉 try‑catch 區塊與檔案路徑處理  

即使你是 GroupDocs 新手，我們也會一步一步帶你完成。

## 設定開發環境

將 GroupDocs.Signature 引入專案相當簡單，請依照你的建置系統選擇適合的方式。

### 使用 Maven

將以下 **maven dependency groupdocs** 加入你的 `pom.xml` 檔案：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

加入後，執行 `mvn clean install` 下載函式庫。

### 使用 Gradle

對於 Gradle 專案，請在 `build.gradle` 中加入此行：

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

然後使用 `gradle build` 同步專案。

### 直接下載方式

想手動安裝？請從 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) 下載 JAR，並將其加入專案的 classpath。

### 授權設定（重要！）

以下是常讓人意外的地方：GroupDocs 在生產環境必須使用授權。你的選項如下：

- **免費試用** – 適合測試，功能完整，但有時間限制  
- **臨時授權** – 需要更長的評估時間？可取得 [臨時授權](https://purchase.groupdocs.com/temporary-license/) 以延長測試期  
- **商業授權** – 用於正式上線，請前往 [購買授權](https://purchase.groupdocs.com/buy)  

試用版會在文件上加上浮水印，請在示範時留意。

### 基本初始化

函式庫安裝完成後，初始化 GroupDocs.Signature 只需要指向你的文件：

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```

就這樣！現在你已擁有一個可供使用的 `Signature` 物件。接下來，我們進入真正有趣的部分——加入 QR Code。

## 了解 QR Code 簽章

在寫程式之前，先釐清 QR Code 簽章的實際作用（因為常有人搞混概念）。

QR Code 簽章不只是隨意在文件上貼上一個 QR Code，而是將可驗證資訊（例如時間戳、簽署者身分或驗證 URL）以可掃描的形式嵌入文件。使用者掃描 QR Code 後，即可在不需特殊軟體的情況下驗證文件真偽。

**什麼時候該使用 QR Code 簽章？**

- 需要行動裝置快速驗證（手機掃描）  
- 文件可能會列印成實體副本  
- 想嵌入指向驗證入口的連結  
- 需要支援離線驗證流程  

現在就開始實作吧。

## 實作指南：加入 QR Code 簽章

以下將示範如何在 PDF 中於不同位置加入 QR Code 簽章。

### 為什麼定位很重要

你可能會想：「隨便把 QR Code 放哪都行？」技術上可以，但實務上，放置位置會影響可用性與法律效力。合約通常放在右下角，發票則常放右上角，證書則多放在底部中央。

**GroupDocs.Signature** 的好處在於，你可以透過對齊選項精確指定 QR Code 的顯示位置。

### 步驟說明

#### 1. 設定檔案路徑

先定義來源文件與簽署後要儲存的路徑：

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String fileName = Paths.get(filePath).getFileName().toString();
String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignWithAlignment/" + fileName).getPath();
```

**小技巧**：使用 `Paths.get()` 取代字串拼接，可自動處理不同作業系統的路徑分隔符（Windows、Linux、Mac 都適用）。

#### 2. 初始化 Signature 物件

將初始化包在 try‑catch 區塊中，以處理可能的檔案存取問題：

```java
try {
    Signature signature = new Signature(filePath);
    // Signing logic goes here...
} catch (Exception e) {
    throw new RuntimeException("Error initializing signature: " + e.getMessage(), e);
}
```

為什麼要用 `RuntimeException` 包起來？在生產環境除錯時能提供更多上下文資訊，日後追蹤文件無法載入的原因時會很有幫助。

#### 3. 定義 QR Code 大小與位置

以下範例會在每個可能的對齊組合（左上、上中、右上…）建立 QR Code：

```java
int qrWidth = 100;
int qrHeight = 100;
List<SignOptions> listOptions = new ArrayList<>();

for (int horizontalAlignment : HorizontalAlignment.getValues()) {
    for (int verticalAlignment : VerticalAlignment.getValues()) {
        if (verticalAlignment != VerticalAlignment.None && horizontalAlignment != HorizontalAlignment.None) {
            QrCodeSignOptions options = new QrCodeSignOptions("Left-Top");
            options.setWidth(qrWidth);
            options.setHeight(qrHeight);
            options.setHorizontalAlignment(horizontalAlignment);
            options.setVerticalAlignment(verticalAlignment);
            options.setMargin(new Padding(5));
            listOptions.add(options);
        }
    }
}
```

**這段程式碼在做什麼？** 我們遍歷所有水平對齊（Left、Center、Right）與垂直對齊（Top、Center、Bottom），為每個有效組合建立 `QrCodeSignOptions`。`new Padding(5)` 為每個 QR Code 加上 5 像素的邊距，避免與文件內容重疊。

**實務調整**：在正式環境中，你通常不會在每個位置都放 QR Code，只挑選符合需求的幾個位置。例如，合約只需要右下角：

```java
QrCodeSignOptions options = new QrCodeSignOptions("Signature");
options.setWidth(100);
options.setHeight(100);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setMargin(new Padding(10));
```

#### 4. 簽署文件

最後一次性套用所有設定好的簽章：

```java
SignResult signResult = signature.sign(outputFilePath, listOptions);
```

`sign()` 方法會處理列表中的所有 QR Code，並將結果儲存至輸出路徑，回傳的 `SignResult` 物件會告訴你成功加入了多少簽章（方便記錄）。

**效能提醒**：簽署是同步執行的。若每小時需處理上百份文件，建議改為背景工作佇列，而非直接在使用者請求中執行。

## 常見陷阱與解決方案

以下整理開發者最常碰到的問題與對策。

### 問題 1：出現「File Not Found」錯誤

**症狀**：即使檔案確實存在，程式仍拋出找不到檔案的例外。

**解決方案**：檢查以下三點  
1. 是否使用絕對路徑？相對路徑會因執行環境不同而產生差異。  
2. 程式是否具備來源檔案的讀取權限與輸出目錄的寫入權限？  
3. 路徑中是否有需要跳脫的特殊字元？

```java
// Better approach: Use absolute paths
String absolutePath = new File(filePath).getAbsolutePath();
Signature signature = new Signature(absolutePath);
```

### 問題 2：QR Code 與文件內容重疊

**症狀**：QR Code 蓋住重要文字或被裁切在頁邊。

**解決方案**：增加邊距值，並策略性調整對齊方式：

```java
options.setMargin(new Padding(20)); // Increase from 5 to 20 pixels
```

若文件版面多變，建議將 QR Code 放在永遠空白的區塊（例如簽名欄位）內。

### 問題 3：大型文件導致記憶體不足

**症狀**：處理超過 10 MB 的 PDF 時拋出 `OutOfMemoryError`。

**解決方案**：確保正確釋放 `Signature` 物件，並考慮分批處理：

```java
try (Signature signature = new Signature(filePath)) {
    // Your signing code
} // Automatically closes and releases resources
```

使用 try‑with‑resources 可在例外發生時仍確保資源釋放。

### 問題 4：QR Code 內容未更新

**症狀**：所有 QR Code 都顯示相同文字，儘管你想為每個位置自訂。

**解決方案**：務必為每個位置建立 **新的** `QrCodeSignOptions` 物件，切勿重複使用同一個：

```java
// Wrong - reuses same object
QrCodeSignOptions options = new QrCodeSignOptions("Text");
options.setHorizontalAlignment(HorizontalAlignment.Left);
listOptions.add(options);
options.setHorizontalAlignment(HorizontalAlignment.Right); // Modifies existing!
listOptions.add(options);

// Correct - creates new object each time
listOptions.add(new QrCodeSignOptions("Left"));
listOptions.add(new QrCodeSignOptions("Right"));
```

## 實務應用

以下說明 QR Code 簽章在真實商業情境中的常見使用方式。

### 1. 合約管理系統

在需要具備驗證功能的法律合約上：

- 從模板產生合約 PDF  
- 加入包含合約編號、時間戳與簽署者雜湊的 QR Code 簽章  
- 將文件存入安全儲存空間  
- 使用者掃描 QR Code → 轉至驗證入口 → 顯示合約詳細資訊  

**為什麼可行**：即使是列印出的合約，法律團隊也能透過手機快速驗證真偽，且 QR Code 提供完整稽核紀錄。

### 2. 發票自動化處理

每日處理上百張發票時：

- 為每張已處理的發票加入 QR Code  
- 編碼發票號碼、供應商 ID 與處理時間戳  
- 使用右上角定位，避免干擾發票原始資料  
- 將簽署後的發票存檔以符合法規要求  

**實作小技巧**：在所有發票上保持相同的 QR Code 位置，讓自動掃描器能固定搜尋。

### 3. 證書發放

發放培訓完成證書或合規證書時：

- 產生包含受領人資訊的 PDF 證書  
- 在底部中央加入 QR Code，內含證書 ID 與驗證 URL  
- 受領人可直接掃描驗證真偽，雇主亦能即時確認資格  

**加分**：在 QR Code 下方印上小字 URL，供無法掃描者手動輸入。

### 4. 內部文件追蹤

大型企業的文件審批流程：

- 每個審批階段加入 QR Code，內含審批者 ID、時間戳與文件版本  
- 掃描即可查看完整審批歷史  
- 有助於稽核與合規追蹤  

## 生產環境最佳實踐

從原型升級到正式上線，請遵守以下原則。

### 資源管理

務必在使用完畢後關閉 `Signature` 物件，以防止記憶體泄漏：

```java
try (Signature signature = new Signature(filePath)) {
    // Your code
} // Auto‑closes
```

對於 Web 應用程式，可考慮建立文件處理池，限制同時執行的操作數量。

### 錯誤處理策略

不要只捕獲並記錄，應提供可操作的錯誤資訊：

```java
try {
    SignResult result = signature.sign(outputFilePath, listOptions);
    if (result.getSucceeded().size() < listOptions.size()) {
        logger.warn("Only {} of {} signatures applied",
                    result.getSucceeded().size(),
                    listOptions.size());
    }
} catch (Exception e) {
    logger.error("Signature failed for document: {}", filePath, e);
    // Implement retry logic or alert mechanism
}
```

### 效能優化

高併發情境下建議：

1. **批次處理** – 同時平行處理多筆文件（依記憶體容量限制併發數）  
2. **快取** – 若多次使用相同的簽章設定，請一次建立後重複使用  
3. **非同步作業** – 在使用者介面層以背景工作者執行簽署  
4. **記憶體監控** – 設定記憶體使用警示，避免突發 OOM  

### 安全考量

- 將簽署後的文件與原始檔分開儲存  
- 記錄所有簽署操作以供稽核  
- 為簽署功能實施存取控制  
- 若 QR Code 內含敏感資訊，請加密後再編碼  

## 何時使用 QR Code 簽章（以及何時不適合）

**適合使用 QR Code 簽章的情境：**

- 需要行動裝置快速驗證  
- 文件可能會列印並再次掃描  
- 想嵌入驗證入口的連結  
- 公開文件（如收據、證書）需即時驗證  

**不建議使用 QR Code 簽章的情境：**

- 需要具備法律效力的加密簽章（請改用 PKI 簽章）  
- QR Code 在列印過程中可能受損或被遮蔽  
- 完全離線且無法使用掃描設備的環境  
- 文件大小極為敏感，且不想因 QR Code 增加額外 KB  

**建議結合使用**：同時採用加密簽章與 QR Code，兼具法律效力與行動驗證便利性。

## 疑難排解指南

### 簽章未顯示

1. 輸出檔案是否真的產生？（檢查檔案系統）  
2. 是否開啟了正確的輸出檔案？  
3. `SignResult` 是否顯示成功？  
4. 對齊與邊距設定是否把 QR Code 推到頁面不可見區域？

### QR Code 無法掃描

- 保持 QR Code 大小 ≥ 100 × 100 px  
- 確保與背景有足夠對比度  
- 編碼資料少於 100 個字元以提升掃描成功率  
- 列印實體文件時使用較高 DPI  

### 效能下降

- 減少單文件的簽章數量  
- 確認未不必要地重建 `Signature` 物件  
- 監控記憶體使用，必要時改為小批次處理  

## 常見問答

**Q:** *我可以簽署除 PDF 之外的文件嗎？*  
**A:** 當然可以。GroupDocs.Signature 支援 Word（DOC/DOCX）、Excel（XLS/XLSX）、PowerPoint（PPT/PPTX）以及影像格式（JPG、PNG、TIFF）。API 在不同格式間基本相同。

**Q:** *如何自訂 QR Code 的外觀？*  
**A:** 使用 `QrCodeSignOptions` 的 `setForeColor()`、`setBackgroundColor()`、`setBorder()` 等屬性。保持簡潔以確保可掃描性。

**Q:** *能否只在多頁文件的特定頁面加入 QR Code？*  
**A:** 可以！透過 `options.setPageNumber(pageNumber);` 設定頁碼。例如：

```java
options.setPageNumber(1); // Add to first page only
```

**Q:** *QR Code 可以編碼哪些資料？*  
**A:** 任意文字、URL、JSON、XML 等皆可。建議保持在約 200 個字元以確保掃描穩定。若資料較大，可編碼指向完整資料的短 URL。

**Q:** *如何以程式方式驗證 QR Code 簽章？*  
**A:** GroupDocs.Signature 提供 `verify` 方法。例如：

```java
VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    // Signature is authentic
}
```

**Q:** *在多執行緒環境下可以使用嗎？*  
**A:** 可以，但每個執行緒必須建立獨立的 `Signature` 實例——物件本身不是執行緒安全的。高併發情況下建議使用處理佇列。

**Q:** *加入 QR Code 會影響檔案大小嗎？*  
**A:** 影響極小，通常每個 QR Code 只會增加 5‑20 KB，對大多數 PDF 來說可忽略不計。但若一次加入大量 QR Code，仍需考慮儲存空間。

## 後續步驟

現在你已掌握在 Java 中實作 **java generate qr code** 簽章的完整基礎。接下來可以探索以下方向：

1. **進階客製化** – 深入了解 QR Code 樣式設定，參考 [GroupDocs 文件](https://docs.groupdocs.com/signature/java/)  
2. **驗證系統** – 建置一個讓使用者上傳或掃描 QR Code 進行驗證的 Web 入口  
3. **工作流程整合** – 把簽署功能串接至既有的文件管理系統  
4. **行動應用** – 開發配套的手機 App，用於掃描與即時驗證  

祝開發順利，享受 QR Code 簽章為你的 Java 應用帶來的安全與便利！

## 資源與支援

- **文件說明**： [GroupDocs.Signature Java Docs](https://docs.groupdocs.com/signature/java/)  
- **API 參考**： [完整 API 參考文件](https://reference.groupdocs.com/signature/java/)  
- **下載**： [最新 Java 版本](https://releases.groupdocs.com/signature/java/)  
- **購買授權**： [購買 GroupDocs.Signature](https://purchase.groupdocs.com/buy)  
- **免費試用**： [開始免費試用](https://releases.groupdocs.com/signature/java/)  
- **臨時授權**： [取得臨時授權](https://purchase.groupdocs.com/temporary-license/)  
- **社群支援**： [GroupDocs 論壇](https://forum.groupdocs.com/c/signature/)  

---

**最後更新日期：** 2025-12-31  
**測試環境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs