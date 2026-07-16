---
categories:
- Java Development
date: '2026-05-21'
description: 了解如何在 PDF 中使用 GroupDocs.Signature for Java 生成 qr code java 簽名。包括 Maven
  設定、定位技巧以及生產最佳實踐。
keywords:
- generate qr code java
- java generate qr code
- groupdocs signature java
lastmod: '2026-05-21'
linktitle: QR Code 簽署 Java 指南
schemas:
- author: GroupDocs
  dateModified: '2026-05-21'
  description: Learn how to generate qr code java signatures in PDFs using GroupDocs.Signature
    for Java. Includes Maven setup, positioning tips, and production best practices.
  headline: 'generate qr code java: Complete QR Code Signing Guide'
  type: TechArticle
- description: Learn how to generate qr code java signatures in PDFs using GroupDocs.Signature
    for Java. Includes Maven setup, positioning tips, and production best practices.
  name: 'generate qr code java: Complete QR Code Signing Guide'
  steps:
  - name: Use absolute paths or ensure the working directory is correct.
    text: Use absolute paths or ensure the working directory is correct.
  - name: Confirm read permissions for the source and write permissions for the output
      folder.
    text: Confirm read permissions for the source and write permissions for the output
      folder.
  - name: Escape any special characters in the path.
    text: Escape any special characters in the path.
  - name: '**Batch Processing** – process documents in parallel, but cap concurrency
      based on RAM.'
    text: '**Batch Processing** – process documents in parallel, but cap concurrency
      based on RAM.'
  - name: '**Caching** – reuse identical `QrCodeSignOptions` objects across documents.'
    text: '**Caching** – reuse identical `QrCodeSignOptions` objects across documents.'
  - name: '**Async Operations** – move signing to background workers for responsive
      APIs.'
    text: '**Async Operations** – move signing to background workers for responsive
      APIs.'
  - name: '**Memory Monitoring** – set alerts for spikes and tune batch size accordingly.'
    text: '**Memory Monitoring** – set alerts for spikes and tune batch size accordingly.'
  - name: Verify the output file is actually created.
    text: Verify the output file is actually created.
  - name: Confirm you’re opening the correct output file.
    text: Confirm you’re opening the correct output file.
  - name: Check `SignResult` for a success count.
    text: Check `SignResult` for a success count.
  type: HowTo
- questions:
  - answer: GroupDocs.Signature for Java
    question: What library adds QR code signatures in Java?
  - answer: Maven (see *maven dependency groupdocs*)
    question: Which build tool supports the Maven dependency?
  - answer: Yes, using alignment and page‑number options
    question: Can I position QR codes on specific pages?
  - answer: Yes, a commercial GroupDocs license is required
    question: Do I need a license for production?
  - answer: Absolutely, when sized ≥ 100 × 100 px and placed with proper margins
    question: Is the QR code scannable after signing?
  type: FAQPage
tags:
- QR codes
- PDF signing
- digital signatures
- document security
title: 生成 qr code java：完整 QR Code 簽署指南
type: docs
url: /zh-hant/java/advanced-options/master-groupdocs-signature-java-qr-code-signing/
weight: 1
---

# 生成 QR Code Java：完整 QR Code 簽署指南

在本教學中，您將學會如何使用 GroupDocs.Signature for Java 在 PDF 文件中 **生成 QR Code Java** 簽名。我們將逐步說明如何添加 QR Code、精確定位，以及避免大多數開發者常犯的錯誤。無論您是構建合約管理平台還是安全發票流程，此指南都提供了可直接投入生產的解決方案。

## 快速答覆
- **哪個程式庫在 Java 中添加 QR Code 簽名？** GroupDocs.Signature for Java  
- **哪個建置工具支援 Maven 依賴？** Maven（請參閱 *maven dependency groupdocs*）  
- **我可以在特定頁面上定位 QR Code 嗎？** 可以，使用對齊與頁碼選項  
- **生產環境需要授權嗎？** 需要，必須擁有商業版 GroupDocs 授權  
- **簽署後 QR Code 能被掃描嗎？** 當尺寸 ≥ 100 × 100 px 且使用適當邊距時，絕對可以  

## 您將學到的內容

完成本指南後，您將能夠：

- 在 Java 專案中設定 QR Code 簽署（Maven、Gradle 或直接下載）  
- 在文件的精確位置（角落、中心、客製對齊）添加 QR Code  
- 在問題變成生產故障前處理常見實作議題  
- 為高吞吐量文件工作流程優化效能  
- 將這些技術應用於真實商業情境  

## 前置條件

在開始編寫程式碼之前，請確保您已具備：

- **GroupDocs.Signature for Java** – 版本 23.12 或更新（以下會說明安裝方式）  
- **Java Development Kit** – JDK 8 或以上（大多數生產環境使用 JDK 11+）  
- **建置工具** – Maven 或 Gradle 用於管理相依性  
- **基本 Java 知識** – 能熟悉 try‑catch 區塊與檔案路徑處理  

即使您是 GroupDocs 新手，我們也會一步一步帶您完成。

## 設定開發環境

將 GroupDocs.Signature 引入專案相當簡單，請依照您的建置系統選擇適合的方法。

### 使用 Maven

將以下 **maven dependency groupdocs** 加入 `pom.xml` 檔案：

``` 
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```
```

加入後，執行 `mvn clean install` 以下載程式庫。

### 使用 Gradle

對於 Gradle 專案，將此行加入 `build.gradle`：

``` 
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```
```

然後使用 `gradle build` 同步專案。

### 直接下載方式

想手動安裝？請從 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) 下載 JAR，並將其加入專案的 classpath。

### 授權設定（重要！）

以下是常讓使用者感到意外的地方：GroupDocs 需要授權才能在生產環境使用。可選方案：

- **免費試用** – 完整功能，時間有限  
- **臨時授權** – 需要更長測試時間？可取得 [temporary license](https://purchase.groupdocs.com/temporary-license/) 進行延長測試  
- **商業授權** – 生產部署時請 [purchase a license](https://purchase.groupdocs.com/buy)  

試用版會加上浮水印，請依需求規劃示範環境。

## 基本初始化

`Signature` 是 GroupDocs.Signature for Java 的主要入口類別，用於載入與操作文件以進行簽署。安裝程式庫後，初始化非常簡單，只需指向您的文件：

``` 
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
Signature signature = new Signature(filePath);
```
```

即可建立可供使用的 `Signature` 物件。

## 了解 QR Code 簽名

QR Code 簽名會將可驗證資料（例如時間戳、簽署者身分或驗證 URL）嵌入文件內的可掃描 QR 圖片。掃描後，QR Code 會導向驗證入口或顯示內嵌的中繼資料，讓使用者無需特殊軟體即可快速行動驗證。

**何時應使用 QR Code 簽名？**

- 手機快速驗證（使用手機掃描）  
- 可能列印的實體文件  
- 嵌入驗證入口的連結  
- 支援離線驗證工作流程  

## 實作指南：添加 QR Code 簽名

以下示範如何在 PDF 中於不同位置加入 QR Code 簽名。

### 為何定位很重要

正確的定位可確保 QR Code 易於掃描、符合合規標準，且不會遮蔽重要內容。合約常放在右下角；發票則適合右上角；證書則在底部居中較為美觀。

### 步驟式實作

#### 1. 設定檔案路徑

定義來源文件與簽署後檔案的存放位置：

``` 
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.pdf";
String fileName = Paths.get(filePath).getFileName().toString();
String outputFilePath = new File("YOUR_OUTPUT_DIRECTORY", "SignWithAlignment/" + fileName).getPath();
```
```

**小技巧：** 使用 `Paths.get()` 取代字串串接，可自動處理作業系統的路徑分隔符。

#### 2. 初始化 Signature 物件

將初始化包在 try‑catch 區塊中，以處理可能的檔案存取問題：

``` 
```java
try {
    Signature signature = new Signature(filePath);
    // 簽署邏輯寫在這裡...
} catch (Exception e) {
    throw new RuntimeException("Error initializing signature: " + e.getMessage(), e);
}
```
```

`RuntimeException` 能在除錯時提供更多上下文資訊，省下大量時間。

#### 3. 定義 QR Code 大小與位置

`QrCodeSignOptions` 用於設定將放置於文件的 QR 圖片，可設定尺寸、邊距與對齊方式。

``` 
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
```

此迴圈會為每種水平（左、置中、右）與垂直（上、置中、下）對齊建立 QR Code 設定，並加上 5 像素的邊距，避免貼到頁面邊緣。

在大多數生產情境下，您只會選擇單一位置，例如合約的右下角：

``` 
```java
QrCodeSignOptions options = new QrCodeSignOptions("Signature");
options.setWidth(100);
options.setHeight(100);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setMargin(new Padding(10));
```
```

#### 4. 簽署文件

一次性套用所有已配置的簽名：

``` 
```java
SignResult signResult = signature.sign(outputFilePath, listOptions);
```
```

`sign()` 方法會處理列表中的每個 QR Code，並將結果寫入指定的輸出路徑。回傳的 `SignResult` 物件會告訴您成功加入的簽名數量，方便記錄。

**效能說明：** 簽署為同步操作。若每小時需處理上百份文件，建議將此流程放入背景工作佇列，而非直接在使用者請求中執行。

## 常見陷阱與解決方案

### 問題 1：「找不到檔案」錯誤

**症狀：** 即使檔案確實存在仍拋出檔案未找到例外。  

**解決方案：** 檢查以下三點：  
1. 使用絕對路徑或確認工作目錄正確。  
2. 確認來源檔案具讀取權限，輸出資料夾具寫入權限。  
3. 逃脫路徑中的特殊字元。

``` 
```java
// 更佳做法：使用絕對路徑
String absolutePath = new File(filePath).getAbsolutePath();
Signature signature = new Signature(absolutePath);
```
```

### 問題 2：QR Code 與文件內容重疊

**症狀：** QR Code 蓋住重要文字或被裁切在頁邊。  

**解決方案：** 增大邊距值，並選擇不會佔用文字區域的對齊方式：

``` 
```java
options.setMargin(new Padding(20)); // 從 5 像素提升至 20 像素
```
```

### 問題 3：大型文件的記憶體問題

**症狀：** 處理超過 10 MB 的 PDF 時拋出 `OutOfMemoryError`。  

**解決方案：** 盡快釋放 `Signature` 物件，並分批處理大型檔案：

``` 
```java
try (Signature signature = new Signature(filePath)) {
    // 簽署程式碼寫在此處
} // 自動關閉並釋放資源
```
```

使用 try‑with‑resources 可確保即使發生例外也會正確清理。

### 問題 4：QR Code 內容未更新

**症狀：** 所有 QR Code 顯示相同文字，即使嘗試自訂。  

**解決方案：** 為每個位置 **建立新的** `QrCodeSignOptions` 物件，切勿重複使用同一個實例：

``` 
```java
// 錯誤範例 – 重複使用同一物件
QrCodeSignOptions options = new QrCodeSignOptions("Text");
options.setHorizontalAlignment(HorizontalAlignment.Left);
listOptions.add(options);
options.setHorizontalAlignment(HorizontalAlignment.Right); // 會修改已加入的物件
listOptions.add(options);

// 正確範例 – 每次建立新物件
listOptions.add(new QrCodeSignOptions("Left"));
listOptions.add(new QrCodeSignOptions("Right"));
```
```

## 實務應用

### 1. 合約管理系統

工作流程：產生合約 PDF → 加入包含合約編號、時間戳、簽署者雜湊的 QR Code → 安全儲存 → 使用者掃描 QR → 入口顯示合約詳細資訊。此方式讓法務團隊能即時驗證列印版合約的真偽。

### 2. 發票處理自動化

在每張處理過的發票右上角加入 QR Code，編碼發票號、供應商 ID 與處理時間戳。固定位置讓掃描器快速定位，提高稽核效率。

### 3. 證書認證

在證書底部居中放置 QR Code，內含驗證 URL 與證書 ID。收件人可掃描確認憑證，亦提供印刷版 URL 供非行動裝置使用。

### 4. 內部文件追蹤

於多階段審批過程中，每完成一次簽核即嵌入 QR Code，內含審批者 ID、時間戳與版本號。掃描後即可看到完整審批歷史，滿足合規稽核需求。

## 生產環境最佳實踐

### 資源管理

務必關閉 `Signature` 物件以防止記憶體泄漏：

``` 
```java
try (Signature signature = new Signature(filePath)) {
    // 您的程式碼
} // 自動關閉
```
```

對於 Web 應用，可考慮建立處理池以限制同時執行的作業數量。

### 錯誤處理策略

提供可操作的錯誤資訊，避免靜默捕獲：

``` 
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
    // 實作重試或警示機制
}
```
```

### 效能優化

高吞吐量環境建議：

1. **批次處理** – 並行處理文件，但依記憶體容量限制併發數。  
2. **快取** – 在多份文件間重用相同的 `QrCodeSignOptions` 物件。  
3. **非同步作業** – 將簽署移至背景工作者，以提升 API 回應速度。  
4. **記憶體監控** – 設定警示，根據使用情形調整批次大小。

### 安全考量

- 將簽署後的文件與原始檔分開儲存。  
- 為每一次簽署操作寫入日誌，以建立稽核追蹤。  
- 嚴格控管簽署端點的存取權限。  
- 必要時對 QR Code 內的敏感資料進行加密。

## 何時使用 QR Code 簽名（以及何時不適合）

**適合使用 QR Code 簽名的情境：**  

- 需要行動裝置快速驗證。  
- 文件可能列印且需再次掃描。  
- 必須嵌入驗證 URL 或 ID。  
- 工作流程包含離線驗證步驟。  

**不建議使用 QR Code 簽名的情境：**  

- 法律上必須使用具 PKI 的加密簽章（請改用加密簽名）。  
- QR Code 在列印或搬運過程中容易受損或被遮蔽。  
- 完全離線且無法使用掃描設備的環境。  
- 文件大小受嚴格限制（每個 QR Code 會增加約 5‑20 KB）。  

**最佳做法：** 同時結合加密簽章與 QR Code，兼顧法律效力與行動驗證便利性。

## 疑難排解指南

### 簽名未出現在文件中

1. 確認輸出檔案確實已產生。  
2. 確認開啟的是正確的輸出檔案。  
3. 檢查 `SignResult` 的成功計數。  
4. 確認對齊與邊距設定未將 QR Code 推到頁面外。

### QR Code 無法掃描

- 保持 QR 大小 ≥ 100 × 100 px。  
- 使用高對比度（深色碼面對淺色背景）。  
- 編碼資料少於 100 個字元，以提升掃描可靠度。  
- 實體列印時解析度至少 300 dpi。

### 效能下降

- 減少每份文件的 QR Code 數量。  
- 盡可能重用 `Signature` 實例。  
- 監控記憶體使用情形，必要時改為較小批次處理。

## 常見問答

**Q：** *我可以簽署除 PDF 之外的文件嗎？*  
**A：** 可以。GroupDocs.Signature 支援 Word（DOC/DOCX）、Excel（XLS/XLSX）、PowerPoint（PPT/PPTX）以及影像格式（JPG、PNG、TIFF）。API 在所有支援類型上保持一致。

**Q：** *如何自訂 QR Code 的外觀？*  
**A：** 使用 `QrCodeSignOptions` 的 `setForeColor()`、`setBackgroundColor()`、`setBorder()` 等屬性。保持自訂簡潔，以免影響掃描。

**Q：** *能否在多頁文件的特定頁面加入 QR Code？*  
**A：** 完全可以。透過 `options.setPageNumber(pageNumber);` 設定頁碼。例如：

``` 
```java
options.setPageNumber(1); // 僅在第一頁加入
```
```

**Q：** *QR Code 可以編碼什麼資料？*  
**A：** 任意文字、URL、JSON 或 XML，建議不超過 200 個字元以確保掃描穩定。若資料較大，可編碼指向完整資料的短網址。

**Q：** *如何以程式方式驗證 QR Code 簽名？*  
**A：** GroupDocs.Signature 提供 `verify` 方法。例如：

``` 
```java
VerificationResult result = signature.verify(verifyOptions);
if (result.isValid()) {
    // 簽名有效
}
```
```

`Signature` 類別是對文件套用簽名的主要入口。

**Q：** *可以在多執行緒環境使用嗎？*  
**A：** 可以，但每個執行緒必須建立獨立的 `Signature` 物件——實例本身不是執行緒安全的。建議使用處理佇列以因應高併發需求。

**Q：** *加入 QR Code 會對檔案大小產生多少影響？*  
**A：** 影響極小，通常每個 QR Code 只會增加約 5‑20 KB，對大多數 PDF 來說可忽略不計。但若一次簽署上千頁文件，仍需考慮累積效應。

---

**最後更新：** 2026-05-21  
**測試環境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs  

## 資源

- [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/)  
- [temporary license](https://purchase.groupdocs.com/temporary-license/)  
- [purchase a license](https://purchase.groupdocs.com/buy)  
- [GroupDocs documentation](https://docs.groupdocs.com/signature/java/)  
- [GroupDocs.Signature Java Docs](https://docs.groupdocs.com/signature/java/)  
- [Complete API Reference](https://reference.groupdocs.com/signature/java/)  
- [Latest Java Release](https://releases.groupdocs.com/signature/java/)  
- [Buy GroupDocs.Signature](https://purchase.groupdocs.com/buy)  
- [Start Your Free Trial](https://releases.groupdocs.com/signature/java/)  
- [Get Temporary License](https://purchase.groupdocs.com/temporary-license/)  
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/)

## 相關教學

- [Java QR Code Signature Library - Complete GroupDocs Tutorial](/signature/java/qr-code-signatures/)
- [Extract QR Code Data in Java - Complete Guide with GroupDocs](/signature/java/qr-code-signatures/detect-qr-code-mecard-signatures-groupdocs-java/)
- [Remove QR Code from PDF Java - Complete Guide with GroupDocs](/signature/java/signature-management/delete-qr-code-signatures-groupdocs-java/)