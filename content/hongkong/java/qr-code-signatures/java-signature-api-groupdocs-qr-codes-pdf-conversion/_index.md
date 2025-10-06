---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 將二維碼新增至文件並將 PDF 轉換為 DOC 格式。安全地簡化您的文件工作流程。"
"title": "使用 GroupDocs.Signature API 在 Java 中實作二維碼簽章和 PDF 轉換"
"url": "/zh-hant/java/qr-code-signatures/java-signature-api-groupdocs-qr-codes-pdf-conversion/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature API 在 Java 中實作二維碼簽章和 PDF 轉換

## 介紹

在當今的數位世界中，安全且高效的文件簽名對於各種規模的企業至關重要。本教學將引導您使用 GroupDocs.Signature for Java 將二維碼新增至文件中，並將其從 PDF 無縫轉換為 DOC 格式。無論您是想簡化文件工作流程還是增強資料安全性，此解決方案都能提供強大的工具集。

**您將學到什麼：**
- 使用檔案路徑初始化簽名物件。
- 使用 GroupDocs.Signature for Java 建立和設定二維碼簽章選項。
- 配置 PDF 儲存選項以輸出不同的文件類型。
- 使用配置的選項有效率地簽署文件。
- 實際應用和性能考慮。

在深入實施之前，讓我們先回顧先決條件，以確保您已準備好開始。

## 先決條件

要成功實現本教程中討論的功能，您需要：

- **所需的庫和版本：**
  - GroupDocs.Signature 適用於 Java 版本 23.12 或更高版本。
  
- **環境設定要求：**
  - 您的機器上安裝了 JDK（Java 開發工具包）。
  - IDE，例如 IntelliJ IDEA 或 Eclipse。
- **知識前提：**
  - 對 Java 程式設計概念有基本的了解。
  - 熟悉 Maven 或 Gradle 的依賴管理。

## 為 Java 設定 GroupDocs.Signature

首先，將 GroupDocs.Signature 庫整合到您的專案中。具體操作如下：

### Maven 集成
在您的 `pom.xml`：
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 集成
對於使用 Gradle 的用戶，請將其包含在您的 `build.gradle` 文件：
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下載
或者，直接從 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

**許可證取得步驟：**
- **免費試用：** 首先下載免費試用版來探索其功能。
- **臨時執照：** 如果您在開發期間需要延長存取權限，請取得臨時許可證。
- **購買：** 如需長期使用，請考慮從 [群組文檔](https://purchase。groupdocs.com/buy).

### 基本初始化
若要在您的專案中初始化 Java 的 GroupDocs.Signature，請依照下列步驟操作：
```java
import com.groupdocs.signature.Signature;

String filePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF";
Signature signature = new Signature(filePath);
```
此基本設定可讓您開始使用 GroupDocs.Signature 庫處理文件。

## 實施指南

讓我們將實作分解為幾個關鍵功能，以便您能夠添加二維碼並有效地轉換 PDF。

### 功能1：初始化簽名對象

**概述：** 
若要使用任何文件簽名功能，請初始化 `Signature` 對象至關重要。此物件代表 GroupDocs.Signature for Java 中的文件。

#### 逐步實施：
1. **導入簽名類別：**
   ```java
   import com.groupdocs.signature.Signature;
   ```
2. **定義文檔路徑：**
   指定目標 PDF 文件的文件路徑。
   ```java
   String filePath = "YOUR_DOCUMENT_DIRECTORY/SAMPLE_PDF";
   ```
3. **建立簽名對象：**
   使用檔案路徑初始化：
   ```java
   Signature signature = new Signature(filePath);
   ```
此配置為對文件的進一步操作奠定了基礎。

### 功能 2：建立和設定二維碼簽名選項

**概述：** 
使用 GroupDocs.Signature 可以輕鬆將二維碼新增至 PDF。此功能可讓您定義二維碼包含的資料及其在文件中的位置。

#### 逐步實施：
1. **導入所需的類別：**
   ```java
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import com.groupdocs.signature.domain.enums.QrCodeTypes;
   ```
2. **初始化二維碼簽名選項：**
   設定您想要的內容的二維碼。
   ```java
   QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
   signOptions.setEncodeType(QrCodeTypes.QR);
   ```
3. **配置位置：**
   定義二維碼在文件上出現的位置：
   ```java
   signOptions.setLeft(100); // X 座標
   signOptions.setTop(100);  // 座標
   ```
此設定可確保您選擇的資料以二維碼的形式顯示在 PDF 的指定位置。

### 功能 3：為不同的輸出類型設定 PDF 儲存選項

**概述：** 
透過配置儲存選項，可以將已簽署的文件轉換為其他格式，例如 DOC。此功能允許靈活地選擇輸出格式。

#### 逐步實施：
1. **導入保存選項類別：**
   ```java
   import com.groupdocs.signature.options.saveoptions.PdfSaveOptions;
   import com.groupdocs.signature.domain.enums.PdfSaveFileFormat;
   ```
2. **初始化 PDF 保存選項：**
   配置輸出格式和文件處理。
   ```java
   PdfSaveOptions saveOptions = new PdfSaveOptions();
   saveOptions.setFileFormat(PdfSaveFileFormat.Doc);
   saveOptions.setOverwriteExistingFiles(true);
   ```
此配置可確保您的簽名文件以 DOC 格式儲存，並在必要時覆寫現有文件。

### 功能 4：使用設定選項簽署文檔

**概述：** 
最後一步是使用配置的二維碼和儲存選項對 PDF 進行簽署。此過程會整合所有先前的設置，產生已簽署的輸出檔案。

#### 逐步實施：
1. **定義輸出檔路徑：**
   指定已簽署文件的儲存位置。
   ```java
   String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SaveSignedOutputType/Sample.doc";
   ```
2. **執行簽名操作：**
   使用 try-catch 區塊來處理異常：
   ```java
   try {
       signature.sign(outputFilePath, signOptions, saveOptions);
   } catch (Exception e) {
       throw new RuntimeException(e.getMessage());
   }
   ```
此程式碼對文件進行簽名並以指定的格式儲存，從而完成工作流程。

## 實際應用

以下是實施此解決方案的一些實際用例：
1. **合約管理：** 透過嵌入連結到數位簽名的獨特二維碼來簡化合約簽署。
2. **發票處理：** 將簽署的 PDF 發票轉換為可編輯的 DOC 格式，以便於處理和存檔。
3. **文件歸檔：** 使用二維碼整合快速檢索以數位方式儲存的文檔元資料。

與其他系統（例如 ERP 或 CRM 平台）的整合可以透過自動化文件工作流程進一步提高效率。

## 性能考慮

使用 GroupDocs.Signature for Java 時，請考慮以下提示以最佳化效能：
- **高效率資源利用：** 透過確保優化 JVM 設定來最大限度地減少記憶體使用。
- **批次：** 如果簽署多個文件，批次可以提高吞吐量。
- **錯誤處理：** 實施全面的錯誤處理以防止工作流程中斷。

遵循這些最佳實務將有助於在使用 GroupDocs.Signature for Java 時保持最佳效能。

## 結論

透過本教程，您學習如何利用 GroupDocs.Signature for Java 有效地新增二維碼並轉換 PDF。現在，您已掌握了增強文件簽署流程的知識，從而確保應用程式的安全性和多功能性。

為了進一步探索 GroupDocs.Signature for Java 的功能，請考慮嘗試其他功能，例如數位簽章或批次選項。

**後續步驟：**
- 嘗試實作 GroupDocs.Signature 提供的其他簽章類型。