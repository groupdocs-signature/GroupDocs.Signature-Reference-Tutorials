---
categories:
- Java Document Processing
date: '2026-05-11'
description: Learn how to check file extension java and validate document formats
  using GroupDocs.Signature. Complete guide with code examples, troubleshooting tips,
  and best practices for document type checking.
keywords:
- check file extension java
- validate document type java
- java upload file validation
- how to detect file format java
lastmod: '2025-01-02'
linktitle: Java File Format Detection Guide
schemas:
- author: GroupDocs
  dateModified: '2026-05-11'
  description: Learn how to check file extension java and validate document formats
    using GroupDocs.Signature. Complete guide with code examples, troubleshooting
    tips, and best practices for document type checking.
  headline: Java File Format Detection - Validate and Check Document Types
  type: TechArticle
- questions:
  - answer: Change the `<version>` tag in your `pom.xml` to the desired version, then
      run `mvn clean install`. Always review the [release notes](https://releases.groupdocs.com/signature/java/)
      for breaking changes.
    question: How do I update my GroupDocs.Signature library version in Maven?
  - answer: Yes. The library performs content‑based validation, so a file renamed
      from `.exe` to `.pdf` will be rejected as not a valid PDF during processing.
      `getSupportedFileTypes()` only lists formats the library can handle; you still
      need to attempt opening the file to verify its true type.
    question: Can GroupDocs.Signature detect file formats even if the extension is
      wrong?
  - answer: The free trial gives immediate access but includes evaluation watermarks
      and some feature limits. A temporary license provides full feature access for
      30 days without watermarks, ideal for thorough testing in a production‑like
      environment.
    question: What's the difference between a free trial and temporary license?
  - answer: 'Return a concise error like “Unsupported format. Supported extensions
      are: .pdf, .docx, .xlsx, .png, .jpg.” Log the incident for security monitoring
      and consider notifying the user with a UI tooltip that lists allowed types.'
    question: How should I handle unsupported file formats in my application?
  - answer: Yes, but you must supply the password when creating the `Signature` instance.
      Format detection itself does not require the password, but any subsequent processing
      (e.g., adding a signature) will.
    question: Does GroupDocs.Signature work with encrypted or password‑protected files?
  type: FAQPage
tags:
- file-validation
- java-libraries
- document-management
- format-detection
title: Java File Format Detection - Validate and Check Document Types
type: docs
url: /zh-hant/java/advanced-options/groupdocs-signature-java-file-format-support/
weight: 1
---

# 檢查檔案副檔名 java – Java 檔案格式偵測：驗證與檢查文件類型

在處理文件之前，最常見的任務之一是 **檢查檔案副檔名 java**。  

是否曾經上傳檔案，結果因為格式不符合預期而導致應用程式崩潰？你並不孤單。於 Java 中偵測與驗證檔案格式對於構建穩健的文件處理應用程式至關重要——但它比僅檢查副檔名更為複雜（副檔名很容易被偽造或不正確）。

在本指南中，你將學習如何使用 GroupDocs.Signature 這個強大的函式庫，在 Java 中可靠地偵測檔案格式，遠超過簡單的副檔名檢查。無論你是在建構文件管理系統、驗證使用者上傳，或是與雲端儲存服務整合，都能掌握實用技巧，自信處理多樣的文件類型。

**你將學到的內容：**
- 如何以程式方式取得 Java 中支援的檔案格式
- 何時使用函式庫偵測與內建 Java 方法的取捨
- 驗證檔案類型時的常見陷阱（以及如何避免）
- 真實案例的整合情境與效能最佳化建議
- 格式偵測問題的除錯策略

完成後，你將擁有可直接套用於 Java 應用程式的實作範例。現在就先確保已備妥所有必要資源。

## 快速回答
- **檢查檔案副檔名 java 最快的方法是什麼？** 使用 `Signature.getSupportedFileTypes()` 取得完整清單，並將檔案的副檔名與之比對。
- **使用 GroupDocs.Signature 是否需要授權？** 開發階段可使用免費試用版；正式授權則會移除所有評估限制。
- **可以在不讀取整個檔案的情況下驗證上傳嗎？** 可以——GroupDocs.Signature 只檢查檔案標頭，成本遠低於載入整個文件。
- **GroupDocs.Signature 支援多少種格式？** 超過 50 種輸入與輸出格式，包含 PDF、DOCX、XLSX、PPTX、JPG、PNG 等等。
- **是否需要快取格式清單？** 快取可消除重複的反射開銷，提升高併發服務的吞吐量。

## 前置條件

在深入檔案格式偵測之前，請先確保以下環境已就緒：

### 必要函式庫與版本
- **GroupDocs.Signature Library**：版本 23.12 或更新（本教學使用最新穩定版）
- **Java Development Kit**：JDK 1.8 以上（建議使用 JDK 11+ 以獲得更佳效能）
- **建置工具**：Maven 3.x 或 Gradle 6.x 以管理相依性

### 環境設定需求
你應該熟悉：
- 基本的 Java 程式概念（類別、迴圈、import）
- 使用 Maven 或 Gradle 管理相依性
- 從 IDE 或命令列執行 Java 應用程式

**小技巧：** 若處理大型文件或計畫同時處理多筆檔案，請為 JVM 配置足夠的堆積記憶體（稍後會說明最佳化方式）。

環境就緒後，接下來說明如何在專案中加入 GroupDocs.Signature。

## 為 Java 設定 GroupDocs.Signature

將 GroupDocs.Signature 引入專案相當簡單——選擇你慣用的建置工具並依照以下步驟操作。

### 使用 Maven

在 `pom.xml` 中加入以下相依性：

```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

加入相依性後，執行 `mvn clean install` 下載函式庫。

### 使用 Gradle

在 `build.gradle` 中加入此行：

```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

然後同步 Gradle 專案或執行 `gradle build`。

### 直接下載方式

不使用建置工具嗎？你可以直接從 [GroupDocs.Signature for Java releases](https://releases.groupdocs.com/signature/java/) 下載 JAR，手動加入 classpath。（說實話，使用 Maven 或 Gradle 能省下不少麻煩。）

### 授權取得步驟

GroupDocs.Signature 提供彈性的授權方案：

- **免費試用**：適合測試——立即開始，無需信用卡，請前往 [no credit card required](https://releases.groupdocs.com/signature/java/)
- **臨時授權**：需要更長時間評估？可申請 30 天的臨時授權，無限制使用
- **正式購買**：準備上線時，請至 [GroupDocs Purchase Page](https://purchase.groupdocs.com/buy) 取得永久授權

**專業提示：** 先以免費試用探索全部功能；若需要延長評估時間，臨時授權會移除浮水印與限制。

### 基本初始化與設定

`Signature` 是 GroupDocs.Signature 所有操作的核心入口，負責文件載入、格式處理與簽章處理。

以下示範如何在 Java 應用程式中初始化 GroupDocs.Signature：

```java
import com.groupdocs.signature.Signature;

// Create an instance of Signature class
Signature signature = new Signature("sample.pdf");
```

此程式碼會為指定文件建立 `Signature` 物件。實際處理文件時會使用此模式，但若僅要取得支援的格式，並不需要特定檔案（稍後會示範）。

設定完成後，接下來實作偵測與取得支援檔案格式的核心功能。

## 實作指南

以下將把理論落實為實作。我們會建立一個簡易工具，取得所有支援的檔案格式——相當於為文件處理管線建立「相容性檢查器」。

### 為什麼這很重要

在實作文件處理功能之前，你必須先了解函式庫支援哪些檔案類型。此實作會動態取得資訊，優點包括：
- 不必手動硬編碼過時的副檔名清單
- 可即時驗證使用者上傳是否屬於支援格式
- 為 UI 建立檔案類型過濾器提供快速參考

### 步驟說明

**1. 匯入必要類別**

`FileType` 是格式偵測的入口，內含所有支援文件類型的中繼資料。

```java
import com.groupdocs.signature.domain.documentpreview.FileType;
import java.util.List;
```

`FileType` 為 GroupDocs.Signature 為每種支援格式所定義的描述子，提供副檔名、MIME 類型與說明等屬性。

**2. 建立取得類別**

以下為完整實作：

```java
public class GetSupportedFileFormats {
    public static void run() {
        // Retrieve a list of supported file types from the FileType utility.
        List<FileType> supportedFileTypes = FileType.getSupportedFileTypes();

        // Iterate over each FileType object and print its extension to the console.
        for (FileType fileType : supportedFileTypes) {
            System.out.print("\n" + fileType.getExtension());
        }
    }
}
```

**程式說明：**
- `getSupportedFileTypes()`：此靜態方法查詢函式庫內部註冊表，回傳 `FileType` 物件的完整清單
- 迴圈遍歷每種格式，輸出其副檔名（如 `.pdf`、`.docx`、`.xlsx`）
- 每個 `FileType` 物件亦包含其他可存取的中繼資料（稍後會說明）

### 超出基本副檔名

`FileType` 物件提供的不僅是副檔名，還能取得更豐富的資訊：

```java
for (FileType fileType : supportedFileTypes) {
    System.out.println("Extension: " + fileType.getExtension());
    System.out.println("Format: " + fileType.getFileFormat());
    // Additional properties available depending on version
}
```

當你需要顯示使用者友善的格式名稱或依類別（文件、試算表、影像）分組時，此功能相當有用。

## 何時使用此方式

並非所有情境都需要函式庫偵測。以下列出 GroupDocs.Signature 格式偵測最適合的情境：

### 完美使用案例

**1. 建立文件上傳驗證器**  
使用者上傳檔案時，必須在伺服器端驗證格式（永遠不要只信任前端驗證）。此方法可在處理前比對完整支援清單。

**2. 動態檔案類型過濾**  
建立檔案挑選器或上傳介面時，動態產生允許的格式清單，避免維護靜態陣列與函式庫功能不同步。

**3. 多格式文件處理管線**  
若文件來源多元（電子郵件附件、雲端儲存、使用者上傳），需要可靠的格式偵測以將檔案導向正確的處理程序。

**4. 與雲端儲存服務整合**  
同步 AWS S3、Google Drive 或 Azure Blob 時，先驗證文件相容性再下載與處理，可節省頻寬與運算時間。

### 內建 Java 可能已足夠的情況

對於較簡單的需求，Java 內建方法或許足以應付：
- **僅檢查副檔名**：`file.getName().endsWith(".pdf")`
- **MIME 類型偵測**：`Files.probeContentType(path)`
- **基本驗證**：當你能控制上傳來源且信任副檔名時

**重要提醒：** 內建方法易被偽造。例如將 `malicious.exe` 改名為 `document.pdf` 仍會通過副檔名檢查，但會在真正的格式驗證階段失敗。GroupDocs.Signature 會進行更深入的內容檢查。

## 常見問題與除錯

以下列出可能遭遇的問題與快速解決方案。

### 問題 1：回傳空或 Null 清單

**徵兆：** `getSupportedFileTypes()` 回傳空清單或 null。

**可能原因與解決方式：**
- **函式庫未正確初始化**：確認 Maven/Gradle 相依性已正確加入並同步
- **版本相容性**：確保使用 23.12 或更新版本（舊版 API 可能不同）
- **Classpath 問題**：若手動加入 JAR，請確認已正確放入 classpath

**快速修正：**
```java
List<FileType> formats = FileType.getSupportedFileTypes();
if (formats == null || formats.isEmpty()) {
    System.err.println("Error: No file types loaded. Check library initialization.");
    return;
}
```

### 問題 2：缺少預期的格式

**徵兆：** 你預期支援的格式未出現在清單中。

**可能原因：**
- 需要額外外掛的特殊格式（某些 CAD 或醫療影像格式需額外模組）
- 該格式在較新版本才加入，請檢查發行說明
- 該格式僅支援讀取，簽章功能可能不支援（GroupDocs.Signature 主要用於加入簽章）

**除錯方式：**
```java
// Check for specific format
boolean hasPDF = supportedFileTypes.stream()
    .anyMatch(ft -> ft.getExtension().equalsIgnoreCase(".pdf"));
System.out.println("PDF supported: " + hasPDF);
```

### 問題 3：大量呼叫導致效能下降

**徵兆：** 重複呼叫 `getSupportedFileTypes()` 使應用程式變慢。

**解決方案：** 快取結果！此清單在執行期間不會變動：

```java
public class FormatCache {
    private static List<FileType> cachedFormats = null;
    
    public static List<FileType> getSupportedFormats() {
        if (cachedFormats == null) {
            cachedFormats = FileType.getSupportedFileTypes();
        }
        return cachedFormats;
    }
}
```

此模式確保在應用程式生命週期內只查詢一次。

### 問題 4：授權相關限制

**徵兆：** 出現評估警告或格式支援受限。

**解決方案：**
- 在呼叫任何 GroupDocs 方法前先套用授權
- 確認授權檔案路徑正確
- 若使用時限授權，檢查到期日

```java
try {
    License license = new License();
    license.setLicense("path/to/GroupDocs.Signature.lic");
} catch (Exception e) {
    System.err.println("License error: " + e.getMessage());
}
```

## 檔案格式偵測最佳實踐

遵循以下原則，打造穩健且易於維護的偵測機制。

### 1. 早期驗證、快速失敗

在處理流程的最前端檢查檔案格式：

```java
public boolean validateFileFormat(String filePath) {
    String extension = getFileExtension(filePath);
    List<FileType> supported = FormatCache.getSupportedFormats();
    
    boolean isSupported = supported.stream()
        .anyMatch(ft -> ft.getExtension().equalsIgnoreCase(extension));
    
    if (!isSupported) {
        throw new UnsupportedFormatException(
            "File format " + extension + " is not supported"
        );
    }
    return true;
}
```

可避免在不支援的檔案上浪費資源。

### 2. 提供清晰的使用者回饋

拒絕檔案時，告訴使用者哪些格式**被**支援：

```java
public String getSupportedFormatsMessage() {
    List<FileType> formats = FormatCache.getSupportedFormats();
    String extensions = formats.stream()
        .map(FileType::getExtension)
        .collect(Collectors.joining(", "));
    
    return "Supported formats: " + extensions;
}
```

### 3. 不僅信任副檔名

即使副檔名為 `.pdf`，內容仍可能不是有效的 PDF。GroupDocs.Signature 會驗證實際內容，但仍建議結合多種檢查方式：

```java
// First check extension (fast)
if (!hasValidExtension(file)) {
    return false;
}

// Then validate with library (more thorough)
try (Signature signature = new Signature(file)) {
    // If initialization succeeds, format is valid
    return true;
} catch (Exception e) {
    return false;
}
```

### 4. 優雅處理例外

檔案驗證可能因多種原因失敗，請妥善捕捉例外：

```java
public ValidationResult validateDocument(String path) {
    try {
        // Your validation logic
        return ValidationResult.success();
    } catch (UnsupportedFormatException e) {
        return ValidationResult.failure("Unsupported format: " + e.getMessage());
    } catch (IOException e) {
        return ValidationResult.failure("File access error: " + e.getMessage());
    } catch (Exception e) {
        return ValidationResult.failure("Unexpected error: " + e.getMessage());
    }
}
```

### 5. 監控格式支援變化

升級 GroupDocs.Signature 時，請檢查發行說明，留意：
- 新增支援的格式
- 已棄用的格式
- 格式偵測行為的變更

建議加入單元測試，驗證關鍵格式仍受支援：

```java
@Test
public void testEssentialFormatsSupported() {
    List<String> required = Arrays.asList(".pdf", ".docx", ".xlsx");
    List<FileType> supported = FileType.getSupportedFileTypes();
    
    for (String format : required) {
        assertTrue(
            supported.stream().anyMatch(ft -> ft.getExtension().equals(format)),
            format + " should be supported"
        );
    }
}
```

## 效能考量

即使檔案格式偵測看似微不足道，於大量文件或高併發情境下仍需優化。

### 記憶體管理

**快取策略：** 如前所述，將支援格式清單快取起來：

```java
// Good: Load once, reuse many times
private static final List<FileType> SUPPORTED_FORMATS = 
    FileType.getSupportedFileTypes();

// Bad: Loads list every time method is called
public boolean isSupported(String ext) {
    return FileType.getSupportedFileTypes().stream()
        .anyMatch(ft -> ft.getExtension().equals(ext));
}
```

**為何重要：** 讀取格式清單涉及反射與函式庫初始化，僅執行一次即可節省 CPU 與記憶體分配。

### 資源使用指引

**高併發情境建議：**
- 使用執行緒安全的快取（上述範例因為是不可變集合而具備執行緒安全性）
- 若應用程式不一定需要格式偵測，可採用懶加載
- 處理文件時，務必及時關閉 `Signature` 物件以釋放資源

```java
try (Signature signature = new Signature(filePath)) {
    // Process document
} // Automatically closed, resources freed
```

### 批次處理最佳化

若一次驗證多筆檔案，可考慮平行化：

```java
List<String> files = Arrays.asList("doc1.pdf", "doc2.docx", "doc3.xlsx");

// Process in parallel
files.parallelStream()
    .forEach(file -> {
        if (validateFileFormat(file)) {
            processDocument(file);
        }
    });
```

**注意：** 不要過度平行化。若 I/O 為瓶頸，過多執行緒不會提升效能，請自行測試找出最佳執行緒數。

### JVM 調校建議

針對文件密集型應用程式：
- 增加堆積大小：`-Xmx2g`（依需求調整）
- 監控 GC：使用 `-XX:+PrintGCDetails` 觀察問題
- 考慮使用 G1GC 以取得較短的暫停時間：`-XX:+UseG1GC`

## 實務應用與整合

以下示範真實情境，說明檔案格式偵測的關鍵角色。

### 1. 文件管理系統

**情境：** 使用者上傳文件，需要索引、處理與儲存。

**實作範例：**
```java
public class DocumentUploadHandler {
    public void handleUpload(MultipartFile file) {
        // Validate format first
        if (!isFormatSupported(file.getOriginalFilename())) {
            throw new InvalidFormatException(
                "Please upload: " + getSupportedFormatsString()
            );
        }
        
        // Process valid document
        processAndStore(file);
    }
    
    private boolean isFormatSupported(String filename) {
        String ext = getExtension(filename);
        return FormatCache.getSupportedFormats().stream()
            .anyMatch(ft -> ft.getExtension().equalsIgnoreCase(ext));
    }
}
```

### 2. 雲端儲存整合

**情境：** 從 AWS S3 或 Google Drive 同步文件，僅處理支援格式。

**效益：** 避免下載與處理不支援的檔案，節省頻寬與運算時間。

```java
public void syncFromS3(String bucketName) {
    S3Client s3 = S3Client.create();
    ListObjectsV2Request listReq = ListObjectsV2Request.builder()
        .bucket(bucketName)
        .build();
    
    ListObjectsV2Response listing = s3.listObjectsV2(listReq);
    
    for (S3Object object : listing.contents()) {
        if (isFormatSupported(object.key())) {
            // Download and process only supported formats
            downloadAndProcess(bucketName, object.key());
        } else {
            logger.info("Skipping unsupported format: " + object.key());
        }
    }
}
```

### 3. 企業工作流程自動化

**情境：** 根據文件類型將其路由至不同處理管線。

**範例：** PDF 走簽章流程，試算表走資料抽取，影像走 OCR。

```java
public void routeDocument(String filePath) {
    try (Signature signature = new Signature(filePath)) {
        FileType type = signature.getDocumentInfo().getFileType();
        
        switch (type.getExtension()) {
            case ".pdf":
            case ".docx":
                sendToSignatureWorkflow(filePath);
                break;
            case ".xlsx":
            case ".csv":
                sendToDataExtractionWorkflow(filePath);
                break;
            case ".jpg":
            case ".png":
                sendToOCRWorkflow(filePath);
                break;
            default:
                logger.warn("No workflow defined for: " + type.getExtension());
        }
    }
}
```

### 4. 建立檔案類型選取器

**情境：** 前端 UI 需要動態顯示支援的檔案類型。

**前端整合範例：**
```java
@RestController
public class FormatController {
    @GetMapping("/api/supported-formats")
    public ResponseEntity<List<String>> getSupportedFormats() {
        List<String> extensions = FileType.getSupportedFileTypes().stream()
            .map(FileType::getExtension)
            .sorted()
            .collect(Collectors.toList());
        
        return ResponseEntity.ok(extensions);
    }
}
```

前端可使用上述資料配置檔案上傳元件：
```javascript
// Frontend code (for context, not part of Java implementation)
fetch('/api/supported-formats')
    .then(res => res.json())
    .then(formats => {
        fileInput.accept = formats.join(',');
    });
```

## 如何檢查檔案副檔名 java？

載入檔名、擷取其副檔名，並與 `Signature.getSupportedFileTypes()` 回傳的快取清單比對。此兩步驟確保你使用的是最新的目錄，而非硬編碼的陣列，同時因為 GroupDocs.Signature 會在後續驗證檔案標頭，避免偽造副檔名的問題。

## 什麼是 GroupDocs.Signature？

GroupDocs.Signature 是一套 Java 函式庫，讓開發者能在超過 50 種文件格式上新增、驗證與管理數位簽章。它提供統一的 API，支援 PDF、Office、影像等多種型別，並能處理加密檔案、受密碼保護的文件與多頁簽章等複雜情境。

## 為何使用函式庫偵測而非 Java 內建方法？

函式庫偵測會檢查實際的檔案標頭與內部結構，確保內容真的符合聲稱的格式。Java 內建的 `Files.probeContentType` 或單純的字串副檔名檢查容易被偽造，例如將惡意的 `exe` 改名為 `pdf`。GroupDocs.Signature 透過深度內容分析，在任何後續處理前先排除這類風險。

## 何時應該快取支援的檔案格式？

在應用程式啟動時或首次需要時快取格式清單，之後在 JVM 整個生命週期內重複使用不可變的集合。對於高吞吐量的 Web 服務而言，若每個請求都觸發反射密集的函式庫初始化，會額外增加毫秒級的延遲，快取可有效降低此開銷。

## 如何在 Java 中處理不支援的檔案格式？

在早期偵測到不支援的格式時，記錄此嘗試以供稽核，並回傳明確的錯誤訊息告知使用者允許的副檔名。此做法提升使用者體驗，同時減少後端不必要的處理負擔。

## 常見問答

**Q: 如何在 Maven 中更新 GroupDocs.Signature 函式庫版本？**  
A: 在 `pom.xml` 的 `<version>` 標籤改為目標版本，然後執行 `mvn clean install`。更新前請務必閱讀 [release notes](https://releases.groupdocs.com/signature/java/) 以了解可能的破壞性變更。

**Q: 即使副檔名錯誤，GroupDocs.Signature 仍能偵測檔案格式嗎？**  
A: 能。函式庫執行內容為基礎的驗證，即使檔案被改名為 `.pdf`，若實際不是有效的 PDF，仍會在處理時被拒絕。`getSupportedFileTypes()` 僅列出函式庫可處理的格式，真正的類型仍需嘗試開啟檔案驗證。

**Q: 免費試用與臨時授權有何差異？**  
A: 免費試用可立即使用，但會有浮水印與部分功能限制。臨時授權提供完整功能，且在 30 天內無浮水印，適合在類似正式環境中徹底測試。

**Q: 應如何在應用程式中處理不支援的檔案格式？**  
A: 回傳類似「不支援的格式。支援的副檔名有：.pdf、.docx、.xlsx、.png、.jpg」的簡潔錯誤訊息。將事件寫入日誌以供安全監控，並可在 UI 中提供提示列出允許的類型。

**Q: GroupDocs.Signature 能處理加密或受密碼保護的檔案嗎？**  
A: 能，但在建立 `Signature` 實例時必須提供密碼。格式偵測本身不需要密碼，然而後續的簽章或其他操作則需要正確的密碼。

**Q: 是否有 GroupDocs.Signature 的社群或支援論壇？**  
A: 有！請前往 [GroupDocs Forum](https://forum.groupdocs.com/c/signature/) 參與社群討論、查看程式碼範例，或直接向 GroupDocs 團隊提問。

## 資源

**文件說明：**
- [GroupDocs.Signature for Java Documentation](https://docs.groupdocs.com/signature/java/) – 完整指南與教學
- [API Reference](https://reference.groupdocs.com/signature/java/) – 全部類別與方法說明

**下載與授權：**
- [Download Library](https://releases.groupdocs.com/signature/java/) – 最新發行版與版本歷史
- [Purchase Licenses](https://purchase.groupdocs.com/buy) – 定價與授權方案
- [Free Trial](https://releases.groupdocs.com/signature/java/) – 立即開始測試

**支援與社群：**
- [GroupDocs Forum](https://forum.groupdocs.com/c/signature/) – 社群討論與技術支援

---

**最後更新日期：** 2026-05-11  
**測試環境：** GroupDocs.Signature 23.12 for Java  
**作者：** GroupDocs

```xml
<version>24.1</version>  <!-- Update to newer version -->
```

```java
try {
    validateAndProcess(file);
} catch (UnsupportedFormatException e) {
    return ResponseEntity
        .badRequest()
        .body("Unsupported format. Please upload: " + getSupportedFormatsString());
}
```

```java
LoadOptions loadOptions = new LoadOptions();
loadOptions.setPassword("your-password");
Signature signature = new Signature("protected.pdf", loadOptions);
```

## 相關教學

- [Add QR Code to PDF Java - Complete Guide with GroupDocs.Signature](/signature/java/qr-code-signatures/qr-code-signatures-java-groupdocs/)
- [Java Text Signature Search - A Complete Guide to Document Verification with GroupDocs.Signature](/signature/java/search-verification/java-text-signature-search-groupdocs-signature/)
- [Digital Signature in Java - Complete Guide to Certificate Loading and Document Signing](/signature/java/digital-signatures/digital-signature-loading-signing-groupdocs-java/)