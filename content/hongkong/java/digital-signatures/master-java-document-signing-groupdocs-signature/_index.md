---
categories:
- Java Development
- Document Management
date: '2026-08-25'
description: 了解如何使用 GroupDocs.Signature 在 Java 中為 PDF 文件添加條碼。本分步指南說明如何加入 GS1DotCode
  條碼、提取圖像以及避免常見問題。
keywords:
- how to add barcode
- groupdocs signature java
- pdf document barcode
lastmod: '2026-08-25'
linktitle: 在 Java 中為 PDF 添加條碼
og_description: 了解如何使用 GroupDocs.Signature 在 Java 中為 PDF 添加條碼。分步教學、程式碼範例以及 GS1DotCode
  條碼的故障排除技巧。
og_image_alt: Guide showing Java code to embed GS1DotCode barcode into a PDF using
  GroupDocs.Signature
og_title: 如何在 Java 中為 PDF 添加條碼 – 完整指南
schemas:
- author: GroupDocs
  dateModified: '2026-08-25'
  description: Learn how to add barcode to PDF documents in Java using GroupDocs.Signature.
    This step‑by‑step guide shows how to add GS1DotCode barcodes, extract images,
    and avoid common pitfalls.
  headline: How to Add Barcode to PDF in Java
  type: TechArticle
- description: Learn how to add barcode to PDF documents in Java using GroupDocs.Signature.
    This step‑by‑step guide shows how to add GS1DotCode barcodes, extract images,
    and avoid common pitfalls.
  name: How to Add Barcode to PDF in Java
  steps:
  - name: Validate GS1 payloads before encoding.
    text: Validate GS1 payloads before encoding.
  - name: Choose barcode dimensions that balance scan reliability with layout constraints.
    text: Choose barcode dimensions that balance scan reliability with layout constraints.
  - name: Combine barcode signatures with cryptographic signatures for full security
      coverage.
    text: Combine barcode signatures with cryptographic signatures for full security
      coverage.
  type: HowTo
- questions:
  - answer: GS1DotCode is a compact 2‑D dot matrix that stores up to **3,116 characters**
      in a smaller footprint than QR codes, making it ideal for tiny labels and high‑speed
      printing.
    question: What is GS1DotCode and why is it different from QR codes?
  - answer: The free trial is limited to evaluation and adds a watermark to output
      files. Production use requires a purchased or temporary 30‑day license.
    question: Can I use a free trial for production deployments?
  - answer: Set `setPageNumber(pageIndex)` on the `BarcodeSignOptions` object, then
      adjust `setLeft()` and `setTop()` to place it precisely.
    question: How do I position the barcode on a specific page?
  - answer: 'Yes. Provide the password when constructing the `Signature` object: `new
      Signature("file.pdf", "password")`.'
    question: Does GroupDocs.Signature support password‑protected PDFs?
  - answer: Aim for at least **108 pt × 108 pt** (1.5 in × 1.5 in). Larger sizes improve
      readability, especially on low‑resolution printers.
    question: What is the minimum barcode size for reliable scanning?
  type: FAQPage
tags:
- java
- pdf-signing
- barcodes
- groupdocs
- document-security
title: 如何在 Java 中為 PDF 添加條碼
type: docs
url: /zh-hant/java/digital-signatures/master-java-document-signing-groupdocs-signature/
weight: 1
---

# 如何在 Java 中為 PDF 添加條碼

## 介紹

是否曾在 Java 應用程式中為文件真偽問題苦惱？您並不孤單。無論是建立庫存系統、管理合約，或處理供應鏈文件，都很可能需要一種可靠的方式，自動為 PDF 加簽與驗證。

傳統的數位簽章固然優秀，但有時您需要更專門的解決方案——例如能與掃描系統及自動化工作流程無縫配合的條碼簽章。這時 GS1DotCode 條碼就派上用場。

**您將學習：**
- 如何在 Java 中使用 GS1DotCode 條碼為 PDF 文件簽章
- 如何提取並儲存條碼簽章圖像
- 何時（以及為何）使用條碼簽章而非傳統方法
- 常見陷阱及避免方式

完成本指南後，您將擁有一個即插即用的解決方案，可整合至任何 Java 專案。

## 快速解答
- **什麼函式庫可在 Java 中為 PDF 添加條碼？** GroupDocs.Signature for Java.  
- **支援哪種條碼格式？** GS1DotCode，一種緊湊的 2‑D 點陣。  
- **需要付費授權嗎？** 免費試用可用於測試；正式環境需商業授權。  
- **我可以將條碼提取為圖像嗎？** 可以，使用 `BarcodeSignature` API。  
- **需要哪個 Java 版本？** JDK 8 或更高。

## 什麼是「如何添加條碼」？
*How to add barcode* 指的是將機器可讀的條碼圖形以程式方式嵌入 PDF 檔案，使條碼成為文件內容流的一部分。這包括產生條碼圖像、在頁面上定位，並儲存修改後的 PDF，確保條碼仍可搜尋與列印。

## 為何選擇 GS1DotCode 條碼？
GS1DotCode 設計用於空間受限的情況。與水平延伸的線性條碼不同，DotCode 產生 2‑D 點陣，可在小面積內容納大量資訊。這使其非常適合：

- **小型產品標籤**，每一毫米都很重要  
- **高速列印**於生產線（此格式專為此設計）  
- **供應鏈追蹤**，需要編碼複雜資料結構  

此格式在緊湊空間內可容納多達 **3,116 個字元**，即使在高速或部分損壞的情況下也能可靠讀取。若您從事零售或物流，合作夥伴很可能已使用 GS1 標準——因此您使用相同語言。

> **專業提示：** 當您需要在小於 1 英吋 × 1 英吋的標籤上嵌入超過 20 個字元時，請使用 GS1DotCode。

## 前置條件

在開始編寫程式碼之前，請確認您的環境符合以下需求。

### 必要的函式庫與相依性
- **GroupDocs.Signature for Java** 23.12 或更新版本（支援 **30+** 種文件格式）  
- Maven 或 Gradle 用於相依性管理  

### 環境設定
- **JDK 8** 或更新版本已安裝並在 `PATH` 中設定  
- IDE，例如 IntelliJ IDEA、Eclipse 或 NetBeans  
- 用於實驗的範例 PDF 檔案（任何未受保護的 PDF 均可）  

### 知識前置條件
- 基本的 Java 語法（變數、方法、物件）  
- 熟悉 Maven 或 Gradle 的相依性聲明  
- 了解 Java 的檔案 I/O（例如 `FileInputStream`）  

如果缺少上述任一項，請先暫停並安裝；後續步驟假設它們已就緒。

## 設定 GroupDocs.Signature for Java

### Maven
若使用 Maven，請在 `pom.xml` 中加入以下相依性：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

Maven 會自動下載此函式庫及所有必要的傳遞相依性。

### Gradle
對於 Gradle 使用者，請在 `build.gradle` 檔案中加入此行：

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

Gradle 以相同的自動方式解析套件。

### 直接下載
若偏好手動管理，請從官方發行頁面下載 JAR 檔案：[GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/)。將 JAR 放置於專案的 classpath 中。

**專業提示：** Maven 或 Gradle 可簡化未來升級——只需提升版本號。

### 取得授權
GroupDocs 提供三種授權選項：

- **免費試用** – 無需信用卡，輸出會加上浮水印  
- **臨時授權** – 30 天完整功能評估  
- **商業授權** – 移除試用限制並授予正式使用權  

取得授權檔後，將其放入專案的 resources 資料夾，並在建立任何 `Signature` 物件之前載入。

`License.setLicense` 載入 GroupDocs 授權檔，啟用完整功能且不受試用限制。

執行以下程式碼片段以驗證函式庫正確載入：

```java
import com.groupdocs.signature.Signature;

public class InitializeGroupDocs {
    public static void main(String[] args) {
        // Create an instance of Signature
        Signature signature = new Signature("path/to/your/document.pdf");
        
        System.out.println("Initialization successful!");
    }
}
```

若看到「Initialization successful!」即表示設定完成。否則，請再次檢查 classpath 與授權檔路徑。

## 實作指南

我們將說明兩個核心功能：(1) 使用 GS1DotCode 條碼為 PDF 簽章，(2) 將該條碼提取為圖像檔案。

### 功能 1：使用 GS1DotCode 條碼簽署文件

#### 如何在 Java 中使用 GS1DotCode 條碼簽署 PDF？

使用 `new Signature("source.pdf")` 載入目標 PDF，設定包含 GS1 格式資料的 `BarcodeSignOptions` 物件，然後呼叫 `sign()` 產生嵌入條碼的新 PDF。此操作會直接將條碼寫入 PDF 內容流，確保在列印與重新掃描時仍保留條碼。

此流程包含三個簡潔步驟：建立 `Signature` 實例、設定 `BarcodeSignOptions`，以及呼叫 `sign()`。以下程式碼示範每個步驟。

##### 1. 初始化簽章物件
`Signature` 類別是 GroupDocs.Signature 中所有文件處理操作的入口點。

```java
import com.groupdocs.signature.Signature;

String sourceFilePath = "YOUR_DOCUMENT_DIRECTORY/document.pdf";
final Signature signature = new Signature(sourceFilePath);
```

> **為何重要：** `Signature` 物件抽象化檔案處理，能有效串流大型 PDF，無需將整個檔案載入記憶體。

##### 2. 設定條碼選項
`BarcodeSignOptions` 讓您指定條碼類型、編碼資料、位置與尺寸。

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;

BarcodeSignOptions gs1DotCodeOptions = new BarcodeSignOptions("(01)04912345123459(15)970331(30)128(10)ABC123", BarcodeTypes.GS1DotCode);
gs1DotCodeOptions.setLeft(100); // Set barcode position
gs1DotCodeOptions.setTop(100);
gs1DotCodeOptions.setHeight(150);
gs1DotCodeOptions.setWidth(200);
```

> **重點：**  
> - 編碼字串遵循 GS1 應用識別碼 (AI)，例如 `(01)` 代表 GTIN，`(15)` 代表有效日期等。  
> - `setLeft()` 與 `setTop()` 使用點 (72 pts = 1 in)。  
> - 為確保可靠掃描，建議的最小尺寸為 **108 pt × 108 pt**（1.5 in × 1.5 in）。

##### 3. 簽署文件
將設定好的選項加入清單（可結合多種簽章類型），然後呼叫 `sign()`。

```java
import java.util.ArrayList;
import java.util.List;

List<com.groupdocs.signature.options.sign.SignOptions> listOptions = new ArrayList<>();
listOptions.add(gs1DotCodeOptions);
signature.sign("YOUR_OUTPUT_DIRECTORY/signed_document_with_gs1dotcode.pdf", listOptions);
```

> **效能說明：** 在批次操作中重複使用同一個 `Signature` 實例可減少物件建立開銷，提升吞吐量。

### 功能 2：將條碼簽章內容儲存為檔案

#### 如何在 Java 中從已簽署的 PDF 提取條碼圖像？

`BarcodeSignature` 代表從已簽署文件中提取的條碼簽章物件，提供其資料與圖像內容的存取。

建立 `BarcodeSignature` 實例（或透過 `search()` 取得），使用 `getContent()` 讀取其 Base64 編碼的圖像資料，解碼後寫入 PNG 檔案。如此即可得到可於 UI 顯示或傳送至標籤印表機的獨立圖像。

##### 1. 模擬條碼簽章建立
在實際情況下，您會從搜尋結果取得 `BarcodeSignature`；此處為說明目的手動建立實例。

```java
import com.groupdocs.signature.domain.signatures.BarcodeSignature;
import java.io.FileOutputStream;

String base64String = "SampleBase64EncodedData";
BarcodeSignature barcodeSignature = new BarcodeSignature(base64String);
```

##### 2. 將內容儲存為檔案
使用 try‑with‑resources 區塊解碼 Base64 字串，並將產生的位元組寫入磁碟。

```java
int imageNumber = 1;
String formatExtension = ".png";  // Assume PNG format

try (FileOutputStream outputStream = new FileOutputStream("YOUR_OUTPUT_DIRECTORY/barcode_image" + imageNumber + formatExtension)) {
    byte[] byteArray = barcodeSignature.getContent();
    if (byteArray != null) {
        outputStream.write(byteArray);
    }
}
```

> **注意：** 若簽章建立時未嵌入圖像，`getContent()` 可能回傳 `null`。寫入前務必檢查是否為 `null`。

## 常見問題與解決方案

### 問題：條碼無法掃描
**症狀：** 條碼在 PDF 檢視器中看起來正常，但掃描器回報錯誤。  
**解決方案：**  
- 將條碼尺寸提升至至少 **108 pt × 108 pt**。  
- 確保印表機解析度 **≥ 300 dpi**。  
- 確認 GS1 資料字串符合正確的 AI 語法；缺少括號會導致掃描器失效。

### 問題：大型 PDF 發生 OutOfMemoryError
**症狀：** 處理超過 **50 MB** 的文件時觸發堆積空間失敗。  
**解決方案：**  
- 以較大堆積啟動 JVM，例如 `-Xmx2g`。  
- 將文件分批處理。  
- 在每個檔案處理完畢後，明確釋放 `Signature` 物件：`signature.dispose()`。

### 問題：條碼顯示模糊
**症狀：** 輸出 PDF 中的條碼呈現像素化。  
**解決方案：**  
- 使用較大尺寸；函式庫會在可能時渲染向量圖形，縮小後會產生雜訊。  
- 避免光柵轉向量的轉換，讓 GroupDocs 直接從向量定義渲染。

### 問題：授權例外
**症狀：** 出現 “License not found” 或 “Trial limitations exceeded” 等錯誤。  
**解決方案：**  
- 將授權檔放置於 classpath 根目錄（`src/main/resources`）。  
- 在任何 `Signature` 實例化之前呼叫 `License.setLicense("GroupDocs.Signature.lic")`。  
- 對於臨時授權，確認其到期日（自發行日起 30 天）。

## 何時使用此方法

### 合適的使用情境
- **供應鏈追蹤** – 直接在出貨文件上嵌入產品編號、批號與有效日期。  
- **自動化標籤列印** – 為每張 PDF 發票即時產生條碼。  
- **受規範產業** – 許多零售與醫療環境必須遵循 GS1 標準。

### 何時考慮其他方案
- 若僅需加密完整性，標準 PKI 數位簽章更為適合。  
- 若僅需簡單視覺註記，文字簽章或圖像印章即可。  
- 當文件大小受限時，避免加入高解析度條碼圖像；可改用 QR Code，其在相同資料密度下尺寸更小。

## 安全最佳實踐

### 資料驗證
在將使用者提供的資料編碼為條碼前，務必進行清理。格式錯誤的 GS1 字串可能導致後續掃描錯誤，甚至在最壞情況下觸發舊版掃描器韌體的緩衝區溢位。

### 存取控制
實作基於角色的存取控制 (RBAC)，僅允許授權使用者呼叫簽章 API。安全存放授權檔，並限制檔案系統權限。

### 稽核日誌
記錄每一次簽章操作的詳細資訊，例如使用者 ID、時間戳、來源檔案路徑與完整的 GS1 負載。以下為日誌範例程式碼：

```java
// Simple logging example (use a proper logging framework in production)
System.out.println("Document signed by: " + userId + " at " + new Date());
System.out.println("Barcode data: " + barcodeData);
```

### 防篡改偵測
將條碼簽章與加密數位簽章結合。條碼提供機器可讀資料，數位簽章則保證完整性與不可否認性。

## 實務應用

### 1. 供應鏈管理
每張裝箱單皆附加編碼出貨 GTIN、批號與目的地的 GS1DotCode 條碼。各檢查點的掃描器自動更新 ERP 系統，將人工輸入錯誤降低 **98 %**。

### 2. 庫存控制
貨物到達時，接收的 PDF 會以包含採購單號與項目數量的條碼簽章。倉庫人員掃描條碼，即時更新庫存資料庫。

### 3. 零售銷售點
列印帶條碼的發票讓收銀員可掃描發票處理退貨，免於手動輸入交易編號，平均每筆退貨可縮短 **30 秒** 結帳時間。

### 4. 醫療文件
以 GS1DotCode 條碼簽署的處方單嵌入患者 ID、藥品代碼與劑量說明。藥局掃描條碼，即可消除導致不良藥物事件的抄寫錯誤。

## 效能考量

### 記憶體管理
GroupDocs.Signature 會串流 PDF 資料，但仍需及時關閉資源：

```java
try (Signature signature = new Signature(sourceFilePath)) {
    // Do your signing operations here
} // Signature automatically disposed here
```

使用 try‑with‑resources 可確保即使發生例外，`Signature` 物件也會釋放檔案句柄。

### 批次處理技巧
- 當多個文件的負載相同時，重複使用同一個 `BarcodeSignOptions` 實例。  
- 使用 `ExecutorService` 平行簽署 CPU 密集工作負載；在每檔案小於 5 MB 的情況下，典型 8 核心伺服器每分鐘可簽署約 **150 份 PDF**。  
- 限制外部授權驗證呼叫頻率，以避免速率限制。

### 檔案格式最佳化
- 儲存時優先使用 PDF/A‑1b 以利歸檔；它會壓縮串流，檔案大小可減少最高 **40 %**。  
- 條碼尺寸僅保留必要大小；1.5 in × 1.5 in 的條碼大約會在 2 MB PDF 中增加 **15 KB**。

## 結論

您現在已擁有完整、可投入生產的工作流程，可在 Java 中為 PDF 檔案加入 GS1DotCode 條碼簽章、提取條碼圖像，並將此流程整合至更大的文件管理管線。請記得：

1. 在編碼前驗證 GS1 負載。  
2. 選擇兼顧掃描可靠性與版面限制的條碼尺寸。  
3. 結合條碼簽章與加密簽章，以達到完整的安全防護。

下一步：探索 GroupDocs.Signature 提供的其他簽章類型——QR Code、文字印章與數位憑證，皆使用一致的 API 介面。

---

## 常見問答

**問：什麼是 GS1DotCode，且它與 QR Code 有何不同？**  
**答：**GS1DotCode 是一種緊湊的 2‑D 點陣，可在比 QR Code 更小的占位空間內儲存最多 **3,116 個字元**，非常適合微小標籤與高速列印。

**問：我可以在正式環境使用免費試用嗎？**  
**答：**免費試用僅限於評估，且會在輸出檔案加上浮水印。正式使用需購買授權或使用 30 天的臨時授權。

**問：如何將條碼定位於特定頁面？**  
**答：**在 `BarcodeSignOptions` 物件上設定 `setPageNumber(pageIndex)`，再調整 `setLeft()` 與 `setTop()` 以精確放置。

**問：GroupDocs.Signature 是否支援受密碼保護的 PDF？**  
**答：**支援。建立 `Signature` 物件時提供密碼，例如 `new Signature("file.pdf", "password")`。

**問：如何驗證條碼簽章是否正確加入？**  
**答：**`Signature.search()` 會在文件中搜尋簽章，回傳符合條件的簽章物件集合。使用 `Signature.search()` 搭配 `BarcodeSearchOptions`。回傳的 `BarcodeSignature` 物件包含編碼資料與圖像內容，可用於驗證。

**問：可靠掃描的最小條碼尺寸為何？**  
**答：**建議至少 **108 pt × 108 pt**（1.5 in × 1.5 in）。較大的尺寸可提升可讀性，特別是在低解析度印表機上。

**問：我可以同時簽署多個 PDF 嗎？**  
**答：**可以。建立執行緒池，為每個執行緒實例化獨立的 `Signature` 物件；只要每個執行緒處理自己的文件，函式庫即為執行緒安全。

**問：單一 PDF 能嵌入多少條碼有上限嗎？**  
**答：**沒有硬性上限，但每個條碼約增加 **15 KB** 資料。若 PDF 超過 **100 MB**，建議使用批次處理以管理記憶體使用。

**問：此函式庫能在非 Windows 平台上運作嗎？**  
**答：**GroupDocs.Signature for Java 為平台無關，可在任何具相容 JRE 的作業系統上執行，包括 Linux 與 macOS。

**最後更新：** 2026-08-25  
**測試環境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs

## 相關教學

- [如何在 Java 中使用 GroupDocs.Signature 驗證條碼簽章](/signature/java/barcode-signatures/verify-barcode-signatures-groupdocs-signature-java/)  
- [建立條碼簽章 Java – 更新 PDF 條碼](/signature/java/barcode-signatures/java-groupdocs-signature-barcode-initialize-update/)  
- [在 PDF 中加入 QR Code（Java）- 完整指南與 GroupDocs.Signature](/signature/java/qr-code-signatures/qr-code-signatures-java-groupdocs/)