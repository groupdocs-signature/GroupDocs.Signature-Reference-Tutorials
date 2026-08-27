---
categories:
- Java Development
date: '2026-06-11'
description: 了解如何使用 Java 為 PDF 和文件添加 digital signatures。完整指南，包含程式碼範例、故障排除技巧，以及安全最佳實踐。
keywords:
- add digital signature java
- implement digital signatures java
- java document signing library
- groupdocs signature java
- digital certificate handling java
lastmod: '2025-01-02'
linktitle: Digital Signatures in Java
schemas:
- author: GroupDocs
  dateModified: '2026-06-11'
  description: Learn how to add digital signatures to PDF and documents using Java.
    Complete guide with code examples, troubleshooting tips, and security best practices.
  headline: How to Add Digital Signatures to Documents in Java
  type: TechArticle
- description: Learn how to add digital signatures to PDF and documents using Java.
    Complete guide with code examples, troubleshooting tips, and security best practices.
  name: How to Add Digital Signatures to Documents in Java
  steps:
  - name: '**Incorrect password** – verify with OpenSSL: `openssl pkcs12 -info -in
      yourcert.pfx`.'
    text: '**Incorrect password** – verify with OpenSSL: `openssl pkcs12 -info -in
      yourcert.pfx`.'
  - name: '**Expired certificate** – check the validity using `keytool -list -v -keystore
      yourcert.pfx`.'
    text: '**Expired certificate** – check the validity using `keytool -list -v -keystore
      yourcert.pfx`.'
  - name: '**Wrong file format** – only `.pfx` or `.p12` (which contain private keys)
      are accepted.'
    text: '**Wrong file format** – only `.pfx` or `.p12` (which contain private keys)
      are accepted.'
  - name: '**File permission problems** – ensure the Java process can read the certificate
      file.'
    text: '**File permission problems** – ensure the Java process can read the certificate
      file.'
  - name: Store `.pfx` files in a secure vault (AWS Secrets Manager, Azure Key Vault,
      or HashiCorp Vault).
    text: Store `.pfx` files in a secure vault (AWS Secrets Manager, Azure Key Vault,
      or HashiCorp Vault).
  - name: Load the password at runtime from environment variables or the vault’s API.
    text: Load the password at runtime from environment variables or the vault’s API.
  - name: Restrict file system permissions so only the service account can read the
      certificate.
    text: Restrict file system permissions so only the service account can read the
      certificate.
  - name: Rotate certificates at least 30 days before expiration and update the stored
      secret accordingly.
    text: Rotate certificates at least 30 days before expiration and update the stored
      secret accordingly.
  - name: '**Automated Contract Workflows** – When a contract reaches the “approved”
      state in your BPM system, trigger the signing service to embed the legal department’s
      certificate and email the signed copy to the vendor.'
    text: '**Automated Contract Workflows** – When a contract reaches the “approved”
      state in your BPM system, trigger the signing service to embed the legal department’s
      certificate and email the signed copy to the vendor.'
  - name: '**Invoice Approval Systems** – After finance signs off an invoice, automatically
      add a digital signature before sending it to the customer, providing cryptographic
      proof of authenticity.'
    text: '**Invoice Approval Systems** – After finance signs off an invoice, automatically
      add a digital signature before sending it to the customer, providing cryptographic
      proof of authenticity.'
  type: HowTo
- questions:
  - answer: iText focuses solely on PDF and requires you to handle low‑level cryptography
      yourself, while GroupDocs.Signature supports 30+ formats, offers ready‑made
      visual stamps, and abstracts certificate handling, reducing development time
      dramatically.
    question: What’s the main difference between GroupDocs.Signature and iText for
      PDF signing?
  - answer: Yes. Add the Maven dependency, create a `@Service` bean that wraps the
      signing logic, and inject it wherever you need to sign documents. This keeps
      your controllers thin and your signing code reusable.
    question: Can I integrate GroupDocs.Signature into a Spring Boot microservice?
  - answer: The library uses standard PKI algorithms (RSA/ECDSA) and follows the same
      specifications as browsers and Adobe Reader. Security depends on the quality
      of your certificate; always use a CA‑issued certificate and protect the private
      key.
    question: How secure are signatures created with GroupDocs.Signature?
  - answer: Absolutely. As long as the signing certificate is trusted, Adobe Reader,
      Foxit, and modern browsers will validate the signature correctly. Self‑signed
      certificates will display a warning but remain technically valid.
    question: Will signed documents work across different PDF readers?
  - answer: Yes—simply omit the `ImageFilePath` and set size parameters to zero. The
      resulting signature is invisible but still cryptographically sound, perfect
      for backend automation where visual cues aren’t required.
    question: Is it possible to sign documents without a visible signature image?
  type: FAQPage
tags:
- digital-signatures
- document-security
- java-libraries
- pdf-signing
title: 如何在 Java 中為文件添加 Digital Signatures
type: docs
url: /zh-hant/java/digital-signatures/groupdocs-signature-java-digital-signing-guide/
weight: 1
---

# 如何在 Java 中為文件添加數位簽章

## 介紹

實作 **在 Java 中添加數位簽章** 功能可能感覺像在雷區中行走。你必須同時處理憑證格式、簽章位置以及嚴格的安全政策——同時保持使用者體驗流暢。一步走錯，就會得到無效的簽章或在 Adobe Reader 中驗證失敗的文件。

幸運的是，你不需要重新發明輪子或與底層密碼學糾纏。無論你是構建合約管理平台、需要簽署收據的電子商務結帳，或是內部人力資源工作流程，可靠的 Java 函式庫都能為你節省開發時間並避免常見的陷阱。

在本指南中，我們將逐步說明 **GroupDocs.Signature for Java**，這是一個商業函式庫，抽象化了數位簽章的繁重工作。你將學會如何：

- 正確設定函式庫並配置憑證  
- 使用專業的視覺印章簽署 PDF、Word、Excel 及 PowerPoint 檔案  
- 驗證簽章並處理常見錯誤，例如不受信任的憑證或記憶體瓶頸  
- 在生產環境中套用最佳實踐的安全措施  

完成後，你將擁有一個即插即用的實作，可依需求擴充至應用程式處理的任何文件類型。

## 快速解答
- **哪個函式庫可以在 Java 中添加數位簽章？** GroupDocs.Signature for Java。  
- **支援多少種文件格式？** 超過 30 種格式，包括 PDF、DOCX、XLSX、PPTX 以及影像檔案。  
- **生產環境需要授權嗎？** 是——商業授權會移除浮水印並解鎖全部功能。  
- **能否在不發生記憶體不足錯誤的情況下簽署大型 PDF（100 頁以上）？** 可以——只要調整 JVM 堆積大小並使用 `setAllPages(false)` 選項。  
- **支援時間戳記嗎？** 絕對支援；你可以附加受信任的時間戳記授權機構（TSA）憑證，以確保長期有效性。

## 什麼是「在 Java 中添加數位簽章」？

`add digital signature java` 指的是使用 Java API 以程式方式將加密簽章嵌入數位文件的過程。簽章將簽署者的身分（由數位憑證驗證）與文件內容綁定，確保完整性、不可否認性以及跨平台的法律效力。

## 為什麼要在 Java 中實作數位簽章？

GroupDocs.Signature 支援 **30+ 種輸入與輸出格式**，且可在不將整個檔案載入記憶體的情況下處理高達 **500 MB** 的檔案，提供相較於手動使用 PDFBox 實作 **2‑5 倍的速度提升**。此量化效益轉化為更快的交易時間與高流量工作負載的伺服器成本降低。

## 前置條件

在開始之前，請確認你已具備以下項目：

* **Java Development Kit (JDK) 8+** – 建議使用 JDK 11，以獲得更完善的 TLS 支援。  
* **IDE** – IntelliJ IDEA、Eclipse 或具備 Java 擴充功能的 VS Code。  
* **GroupDocs.Signature for Java** – 我們將示範三種將其加入專案的方法。  
* **有效的數位憑證**，格式為 **PFX** 或 **P12**（需要私鑰與密碼）。  

可選但有幫助：

* 熟悉 **Maven** 或 **Gradle** 以管理相依性。  
* 用於測試簽署流程的 PDF、DOCX 或 XLSX 範例檔案。

## 如何安裝 GroupDocs.Signature for Java？

GroupDocs.Signature 只需在建置設定中簡單加入即可。使用符合你建置工具的程式碼片段，將佔位版本替換為最新穩定版，然後執行建置指令即可從 Maven Central 取得函式庫。

**Maven（加入至 pom.xml）：**  
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```  

**Gradle（加入至 build.gradle）：**  
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```  

**手動安裝（若未使用建置工具）：**  
從官方發布頁面下載 JAR — [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) — 並將其加入 classpath。

> **專業提示：** 永遠使用最新的穩定版。截至本文撰寫時，版本 23.12 為最新，但較新的版本通常包含安全修補與效能提升。

## 如何取得並套用 GroupDocs 授權？

GroupDocs.Signature 在生產環境使用時需要授權。授權會移除浮水印並解鎖完整功能，確保簽署的文件符合企業政策。

* **免費試用：** 在[暫時授權頁面](https://purchase.groupdocs.com/temporary-license/)取得 30 天的臨時授權。  
* **付費授權：** 從[GroupDocs 購買頁面](https://purchase.groupdocs.com/buy)購買開發者或企業授權。  

若未取得有效授權，簽署的文件會顯示可見的浮水印，僅適用於評估用途。

## 如何初始化 Signature 物件？

`Signature` 類別是所有文件操作的入口點。它在記憶體中代表單一檔案，提供簽署、驗證與提取簽章的方法。建立 `Signature` 實例會載入目標檔案並為後續處理做好準備。

```java
Signature signature = new Signature("path/to/input.pdf");
```

**這段程式碼在做什麼？**  
此行程式碼建立一個 `Signature` 實例，載入目標文件。路徑可以是絕對或相對路徑，只要確保檔案存在即可。此物件可在多次簽署或驗證操作中重複使用，降低批次處理的開銷。

## 如何設定數位簽章選項？

數位簽章選項封裝了產生有效 PKI 簽章所需的所有設定，包括憑證資訊、視覺外觀與放置規則。正確的配置可確保產生的簽章在加密上可靠，且在文件類型上具備適當的視覺呈現。

### 如何設定憑證資訊？

`DigitalSignOptions` 類別保存所有與憑證相關的設定。以下是此類別的首次定義示例。

`DigitalSignOptions` 定義了加密參數——憑證檔案、密碼以及可選的中繼資料——函式庫使用這些資訊建立有效的 PKI 簽章。

```java
DigitalSignOptions options = new DigitalSignOptions();
options.setCertificatePath("YOUR_DOCUMENT_DIRECTORY/certificate.pfx");
options.setCertificatePassword("yourPassword");
options.setReason("Approved Contract");
options.setContact("legal@yourcompany.com");
options.setLocation("New York, USA");
```

**重點說明：**  
* 絕不要硬編碼密碼；應從環境變數或祕密管理服務載入。  
* 使用 `setReason`、`setContact` 與 `setLocation` 為審核者提供檢視簽章屬性時的上下文資訊。

### 如何自訂簽章的視覺外觀？

`SignatureOptions`（`DigitalSignOptions` 的子類別）控制頁面上的呈現。它允許你附加圖像、調整尺寸，並在頁面上定位視覺印章。

`SignatureOptions` 讓你附加圖像、調整尺寸，並在頁面上定位視覺印章。

```java
options.setImageFilePath("YOUR_DOCUMENT_DIRECTORY/signature.png");
options.setAllPages(true);
options.setWidth(150);
options.setHeight(0); // Auto‑scale based on image aspect ratio
```

* **ImageFilePath：** 指向手寫簽名或公司標誌的 PNG 或 JPG 圖檔。透明 PNG 效果最佳。  
* **AllPages：** 若合約需要每頁都有簽章，設為 `true`；否則設為 `false` 僅在最後一頁簽署。  
* **Width/Height：** 以像素為單位；高度 **50‑80** 像素在大多數商業文件中看起來較為專業。

## 如何控制對齊與內邊距？

對齊設定決定印章在頁面上的位置，而內邊距則在視覺元素周圍留出緩衝，以避免貼近頁邊。適當的對齊提升可讀性，並確保簽章不會干擾現有內容。

`AlignmentOptions` 提供垂直與水平放置的常數，如 `Bottom`、`Right`、`Top` 與 `Center`。

```java
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
options.setPadding(10);
```

* **Padding：** 為印章提供呼吸空間；設定為 **10** 像素可防止圖像貼近頁邊。  
* **實務範例：** 在發票範本中，你可能使用 `Top`/`Left` 將批准者的簽名放在標頭附近。

## 如何為 Office 文件加入簽名欄位？

在簽署 DOCX 或 XLSX 檔案時，可見的簽名欄位提升最終使用者的可讀性。函式庫會建立 Microsoft 風格的簽名欄位，顯示簽署者的姓名、職稱與電子郵件，與原生 Office 體驗相同。

`SignatureLineOptions` 會建立 Microsoft 風格的簽名欄位，顯示簽署者的姓名、職稱與電子郵件。

```java
options.setSignatureLineText("John Doe", "Chief Legal Officer", "j.doe@yourcompany.com");
```

* 此功能在 PDF 中會被忽略，但對於在 Microsoft Office 開啟的 Word 與 Excel 檔案則相當重要。

## 如何實際簽署文件？

使用 `Signature` 實例載入來源檔案，套用完整配置的 `DigitalSignOptions`，然後呼叫 `sign()`。函式庫會將新檔案寫入輸出路徑，原始檔案保持不變。對於大型 PDF（50 頁以上），預期處理時間為 2‑5 秒；可考慮在 Web 服務中以非同步方式執行。

```java
Signature signature = new Signature("SAMPLE_WORDPROCESSING/contract.docx");
DigitalSignOptions options = new DigitalSignOptions();
// ...configure options as shown earlier...
signature.sign("OUTPUT_FOLDER/signed_contract.docx", options);
```

**效能說明：**  
對於超過 100 頁的文件，請增加 JVM 堆積大小（`-Xmx2g`）或停用 `setAllPages(true)` 以限制記憶體使用。

## 如何排除常見問題？

簽署失敗時，最常見的問題與憑證處理、視覺位置或記憶體限制有關。先辨識症狀，然後依照下方的檢查清單快速解決問題。

### 為何會看到「Invalid Certificate」或「Cannot Load Certificate」錯誤？

這些例外通常源於以下四種原因：

1. **密碼不正確** – 可使用 OpenSSL 驗證：`openssl pkcs12 -info -in yourcert.pfx`。  
2. **憑證已過期** – 使用 `keytool -list -v -keystore yourcert.pfx` 檢查有效期限。  
3. **檔案格式錯誤** – 只接受包含私鑰的 `.pfx` 或 `.p12`。  
4. **檔案權限問題** – 確認 Java 程序能讀取憑證檔案。

### 為何簽章未出現在頁面上？

* **AllPages** 標誌可能為 `false`，因此你查看的頁面沒有印章。  
* **Image 路徑** 可能拼寫錯誤；可列印 `options.getImageFilePath()` 以確認。  
* **對齊設定** 可能將印章推至螢幕外；可暫時切換為 `Center` 進行除錯。

### 為何 Adobe Reader 顯示「Signature Invalid」？

* **憑證未受信任** – 自簽憑證會觸發警告。生產環境請使用 CA 簽發的憑證。  
* **憑證鏈不完整** – 確保 `.pfx` 包含中繼與根憑證。  
* **缺少時間戳記** – 若未附加 TSA 憑證，簽章在憑證過期後可能被視為無效。GroupDocs 支援透過 `setTimeStampOptions()` 加入時間戳記。

### 如何避免在處理大型 PDF 時發生 OutOfMemoryError？

* 增加 JVM 堆積大小（`-Xmx4g` 或更高）。  
* 僅簽署必要的頁面（`setAllPages(false)`）。  
* 若環境受限，將檔案分批處理或以串流方式處理。

## 如何在生產環境安全管理憑證？

絕不要在原始碼中嵌入憑證或密碼。請遵循以下步驟：

1. 將 `.pfx` 檔案存放於安全保管庫（如 AWS Secrets Manager、Azure Key Vault 或 HashiCorp Vault）。  
2. 在執行時從環境變數或保管庫 API 載入密碼。  
3. 限制檔案系統權限，僅允許服務帳號讀取憑證。  
4. 在憑證到期前至少 30 天進行輪換，並相應更新存放的祕密。

```java
String certPath = System.getenv("CERT_PATH");
String certPassword = System.getenv("CERT_PASSWORD");
options.setCertificatePath(certPath);
options.setCertificatePassword(certPassword);
```

## 如何記錄簽章操作以符合稽核要求？

稽核日誌提供不可否認的證據。請為每次簽署事件記錄以下欄位：

* 簽署前的文件名稱與雜湊值  
* 簽署者身分（憑證主體）  
* 操作時間戳記（建議使用 UTC）  
* 結果狀態（成功/失敗）及錯誤細節（若有）

```java
logger.info("Signing document {} with certificate {} at {}", docPath, options.getCertificatePath(), Instant.now());
```

## 如何驗證已套用的簽章？

驗證可確保文件在簽署後未被竄改。使用 `verify()` 方法，該方法會回傳 `VerificationResult`，其中包含有效性狀態、簽署者資訊以及任何時間戳記資訊。驗證成功即證明文件的完整性與真實性。

```java
VerificationResult result = signature.verify("OUTPUT_FOLDER/signed_contract.docx");
if (result.isValid()) {
    logger.info("Signature is valid and trusted.");
} else {
    logger.warn("Signature verification failed: {}", result.getErrorMessage());
}
```

## 如何在單一文件中加入多個簽章？

可能需要批准者與見證人兩個簽章。可多次呼叫 `sign()`，每次使用不同的 `DigitalSignOptions` 實例，分別配置各自的憑證與視覺設定。函式庫會保留既有簽章，同時加入新簽章。

```java
// First signature (approver)
signature.sign("output.docx", approverOptions);
// Second signature (witness)
signature.sign("output.docx", witnessOptions);
```

## 如何為不同文件類型建立工廠方法？

可建立輔助方法，根據檔案副檔名回傳預先配置好的 `DigitalSignOptions`，以避免程式碼重複。此方法集中管理憑證載入、視覺預設值與頁面選擇邏輯，適用於 PDF、Word、Excel 以及其他支援的格式。

```java
public DigitalSignOptions getOptionsFor(String extension) {
    DigitalSignOptions opts = new DigitalSignOptions();
    // common settings
    if (extension.equalsIgnoreCase("pdf")) {
        opts.setImageFilePath("signatures/pdf_stamp.png");
    } else if (extension.equalsIgnoreCase("docx")) {
        opts.setSignatureLineText("Jane Smith", "Finance Manager", "j.smith@company.com");
    }
    return opts;
}
```

## 如何驗證文件是否已簽署？

在套用新簽章之前，先檢查是否已有簽章，以避免重複簽署。使用 `getSignatures()` 方法；若回傳的集合非空，則決定是要追加新簽章還是中止操作。

```java
List<SignatureInfo> existing = signature.getSignatures();
if (!existing.isEmpty()) {
    logger.warn("Document already contains {} signatures.", existing.size());
}
```

## 實務應用（真實案例）

1. **自動化合約工作流程** – 當合約在 BPM 系統中進入「已批准」狀態時，觸發簽署服務嵌入法務部的憑證，並將簽署副本電郵給供應商。  
2. **發票批准系統** – 財務簽核發票後，自動加入數位簽章再寄送給客戶，提供加密的真實性證明。  
3. **文件驗證入口網站** – 提供自助服務平台，使用者上傳 PDF，你使用公司憑證簽署，並回傳防篡改的檔案以符合合規需求。  
4. **合規性高的產業** – 如醫療（HIPAA）或金融（SOX），數位簽章透過證明簽署者與簽署時間，滿足稽核需求。  
5. **內部政策發佈** – 用自動化流程取代人工在 HR 政策上蓋章，使用 CHRO 的憑證簽署最終 PDF，確保每位員工收到經驗證的副本。

## 效能考量

| 文件大小 | 平均處理時間 | 推薦設定 |
|----------|--------------|----------|
| 1‑5 頁 | 約 0.5 秒 | 預設選項 |
| 5‑50 頁 | 1‑3 秒 | 如有需要，增加堆積並設定 `setAllPages(true)` |
| 50‑200 頁 | 3‑10 秒 | 設定 `setAllPages(false)`、非同步執行、增大堆積 |

**最佳化建議：**  
* 在批次簽署多個檔案時，重複使用單一 `Signature` 實例。  
* 快取已載入的 `DigitalSignOptions` 物件；重複載入憑證會增加開銷。  
* 對於 Web 服務，可將簽署呼叫包裝於 `CompletableFuture`，或推送至訊息佇列，以保持 UI 響應。

## 專業提示（進階用法）

* **長期有效的時間戳記** – 使用 `setTimeStampOptions()` 附加 TSA 憑證，確保簽章在憑證過期後仍然有效。  
* **隱形簽章** – 省略 `ImageFilePath` 並將 `Width`/`Height` 設為 `0`，即可建立加密上有效但不可見的簽章，適用於不需要視覺印章的後端流程。  
* **自訂 QR Code 簽章** – GroupDocs 可嵌入包含簽署者中繼資料的 QR Code；適合需要透過行動裝置快速驗證的供應鏈文件。

## 常見問答

**Q: GroupDocs.Signature 與 iText 在 PDF 簽署上的主要差異是什麼？**  
A: iText 僅專注於 PDF，且需自行處理底層加密；而 GroupDocs.Signature 支援 30+ 種格式，提供即用的視覺印章，並抽象化憑證處理，大幅縮短開發時間。

**Q: 能否將 GroupDocs.Signature 整合到 Spring Boot 微服務中？**  
A: 可以。加入 Maven 相依性，建立包裝簽署邏輯的 `@Service` Bean，並在需要簽署文件的地方注入它。這樣可讓控制器保持簡潔，簽署程式碼可重用。

**Q: 使用 GroupDocs.Signature 建立的簽章有多安全？**  
A: 函式庫使用標準 PKI 演算法（RSA/ECDSA），遵循與瀏覽器及 Adobe Reader 相同的規範。安全性取決於憑證品質；請始終使用 CA 簽發的憑證並保護私鑰。

**Q: 簽署的文件能在不同的 PDF 閱讀器上正常運作嗎？**  
A: 完全可以。只要簽署憑證受信任，Adobe Reader、Foxit 以及現代瀏覽器都會正確驗證簽章。自簽憑證會顯示警告，但在技術上仍然有效。

**Q: 是否可以在不使用可見簽章圖像的情況下簽署文件？**  
A: 可以——只要省略 `ImageFilePath` 並將尺寸參數設為零。產生的簽章雖不可見，仍具加密效力，適合不需要視覺提示的後端自動化。

## 結論

現在你已擁有使用 GroupDocs.Signature 進行 **在 Java 中添加數位簽章** 的完整生產就緒路線圖。我們涵蓋了從環境設定與憑證處理、視覺自訂、效能調校，到多重簽章與時間戳記等進階情境的全部內容。

**後續步驟：**  
1. 使用自己的憑證與文件範本測試範例程式碼。  
2. 透過將憑證搬移至祕密管理服務，並設定適當的 JVM 記憶體限制，強化部署安全性。  
3. 擴充輔助方法以支援批次處理，或整合至現有的工作流程引擎。

欲深入了解，請參考以下官方文件與社群論壇。

---

**最後更新：** 2026-06-11  
**測試環境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs  

**資源：**  
- [GroupDocs.Signature Documentation](https://docs.groupdocs.com/signature/java/)  
- [Support Forum](https://forum.groupdocs.com/c/signature/)  

{< /blocks/products/pf/tutorial-page-section >}
{< /blocks/products/pf/main-container >}
{< /blocks/products/pf/main-wrap-class >}
{< blocks/products/products-backtop-button >}
```java
import com.groupdocs.signature.Signature;

public class SignatureSetup {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // Your signing logic goes here
    }
}
```
```java
import com.groupdocs.signature.options.sign.DigitalSignOptions;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

DigitalSignOptions options = new DigitalSignOptions("YOUR_DOCUMENT_DIRECTORY/CertificatePfx");
options.setPassword("1234567890"); // Ensure your certificate password is secure
options.setReason("Sign"); // Reason for signing, e.g., "Contract Approval"
options.setContact("JohnSmith"); // Contact information of the signer
options.setLocation("Office1"); // Location where document is signed
```
```java
options.setImageFilePath("YOUR_DOCUMENT_DIRECTORY/ImageHandwrite");
options.setAllPages(true); // Apply signature to all pages of the document
options.setWidth(0); // Auto-width based on content
options.setHeight(60); // Height in pixels
```
```java
options.setVerticalAlignment(VerticalAlignment.Bottom);
options.setHorizontalAlignment(HorizontalAlignment.Right);
Padding padding = new Padding();
padding.setBottom(10); // Bottom padding for aesthetic spacing
padding.setRight(10); // Right padding to prevent clipping at edges
options.setMargin(padding);
```
```java
import com.groupdocs.signature.domain.signatures.DigitalSignatureAppearance;

options.setAppearance(new DigitalSignatureAppearance("John Smith", "Title", "jonny@test.com"));
```
```java
try {
    Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SAMPLE_WORDPROCESSING");
    String outputFilePath = "YOUR_OUTPUT_DIRECTORY/DigitalAppearance.docx";
    signature.sign(outputFilePath, options);
} catch (GroupDocsSignatureException e) {
    throw new RuntimeException(e.getMessage());
}
```
```java
// BAD - Don't do this
options.setPassword("1234567890");

// GOOD - Load from environment variable
String certPassword = System.getenv("CERT_PASSWORD");
if (certPassword == null) {
    throw new RuntimeException("CERT_PASSWORD environment variable not set");
}
options.setPassword(certPassword);
```
```java
logger.info("Document signed: {}, SignedBy: {}, Timestamp: {}", 
    documentName, signerEmail, LocalDateTime.now());
```
```java
// Verify the signature immediately after signing
List<DigitalSignature> signatures = signature.verify();
if (signatures.isEmpty()) {
    throw new RuntimeException("Signature verification failed");
}
```
```java
signature.sign(outputPath, approverOptions);
signature = new Signature(outputPath); // Reload the signed document
signature.sign(finalOutputPath, witnessOptions);
```
```java
public DigitalSignOptions getOptionsForDocType(String docType) {
    DigitalSignOptions options = new DigitalSignOptions(certPath);
    if (docType.equals("contract")) {
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        // Contract-specific settings
    } else if (docType.equals("invoice")) {
        options.setVerticalAlignment(VerticalAlignment.Top);
        // Invoice-specific settings
    }
    return options;
}
```
```java
List<DigitalSignature> existingSignatures = signature.search(DigitalSignature.class);
if (!existingSignatures.isEmpty()) {
    System.out.println("Document already signed by: " + 
        existingSignatures.get(0).getContactInfo());
}
```

## 相關教學

- [Digital Signature in Java - Complete Guide to Certificate Loading and Document Signing](/signature/java/digital-signatures/digital-signature-loading-signing-groupdocs-java/)
- [How to Verify Digital Certificates in Java - Complete Guide with Code Examples](/signature/java/digital-signatures/java-certificate-verification-groupdocs-signature/)
- [Java Document Signing Tutorial - Add Text Signatures with Event Handling](/signature/java/event-handling/java-text-signing-groupdocs-signature-event-handling/)