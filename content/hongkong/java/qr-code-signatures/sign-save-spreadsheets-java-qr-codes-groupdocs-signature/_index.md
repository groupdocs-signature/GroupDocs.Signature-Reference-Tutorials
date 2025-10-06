---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 為 Excel 電子表格簽署二維碼，並將其儲存為多種格式。高效保護您的文件安全。"
"title": "使用 GroupDocs.Signature 在 Java 中對帶有二維碼的 Excel 電子表格進行簽名和保存"
"url": "/zh-hant/java/qr-code-signatures/sign-save-spreadsheets-java-qr-codes-groupdocs-signature/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature 在 Java 中對帶有二維碼的 Excel 電子表格進行簽名和保存

## 介紹

在當今的數位時代，確保文件的真實性比以往任何時候都更加重要。無論您處理的是合約、協議還是財務電子表格，安全簽名文件都能節省時間並防止詐欺。 **GroupDocs.Signature for Java** 是一個功能強大的庫，可以簡化各種文件格式的電子簽名。本教學將引導您使用 GroupDocs.Signature 對具有二維碼的 Excel 電子表格進行簽名，並將其儲存為不同的格式。

### 您將學到什麼：
- 如何使用二維碼簽名簽署電子表格。
- 以多種輸出格式儲存簽署的文件，如 PDF、XLSX 等。
- 處理文件簽章時優化 Java 應用程式的效能。

完成本教學後，您將對如何在 Java 應用程式中整合和使用 GroupDocs.Signature 執行簽署任務有深入的理解。在開始實現這些功能之前，讓我們先深入了解必要的工具設定！

## 先決條件

在繼續本指南之前，請確保您已具備以下條件：
- **Java 開發工具包 (JDK)** 安裝在您的機器上。
- 具備 Java 程式設計基礎並熟悉 Maven 或 Gradle 建置系統。
- 像 IntelliJ IDEA、Eclipse 或 NetBeans 這樣的 IDE。

此外，您需要在專案中為 Java 設定 GroupDocs.Signature。設定過程非常簡單，可以使用 Maven 或 Gradle 依賴項來實現，如下所示：

## 為 Java 設定 GroupDocs.Signature

首先，將 GroupDocs.Signature 相依性新增至專案的建置檔案。

### Maven
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

或者，您可以直接從 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

#### 許可證獲取
要充分利用 GroupDocs.Signature 的功能：
- **免費試用**：從免費試用開始探索基本功能。
- **臨時執照**：在評估期間取得臨時許可證以獲得完全存取權限。
- **購買**：為了長期使用，請考慮購買商業許可證。

### 基本初始化和設定
初始化 `Signature` 透過傳遞文檔文件路徑來分類，如下所示：
```java
import com.groupdocs.signature.Signature;

// 使用文檔路徑進行初始化
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SampleSpreadsheet.xlsx");
```

## 實施指南
在本節中，我們將介紹使用 GroupDocs.Signature 簽署電子表格並儲存的步驟。

### 使用二維碼簽署電子表格
#### 概述
此功能可讓您在 Excel 電子表格中新增二維碼簽章。它對於添加易於掃描的安全電子標識符特別有用。
##### 步驟 1：定義檔案路徑
首先定義輸入和輸出檔案的路徑：
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleSpreadsheet.xlsx";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/signedDocument.pdf";
```
##### 步驟2：初始化簽名對象
創建一個 `Signature` 物件與您的文件的文件路徑。
```java
Signature signature = new Signature(filePath);
```
##### 步驟 3：建立二維碼簽名選項
配置二維碼簽名選項。指定二維碼的文字、類型和位置等屬性：
```java
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100); // X座標
signOptions.setTop(100);  // Y座標
```
##### 步驟 4：配置儲存選項
指定已簽署文件的儲存方式，包括其格式：
```java
import com.groupdocs.signature.options.saveoptions.SpreadsheetSaveOptions;
import com.groupdocs.signature.domain.enums.SpreadsheetSaveFileFormat;

SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions();
saveOptions.setFileFormat(SpreadsheetSaveFileFormat.Pdf);
saveOptions.setOverwriteExistingFiles(true);
```
##### 步驟 5：簽署並儲存文檔
最後，使用 `sign` 應用二維碼簽名並儲存文件的方法：
```java
try {
    signature.sign(outputFilePath, signOptions, saveOptions);
} catch (Exception e) {
    e.printStackTrace();
}
```
### 將文件儲存為不同的輸出文件格式
#### 概述
GroupDocs.Signature 讓您可以將簽署的文件儲存為各種格式，例如 PDF、XLSX 和 DOCX。
##### 步驟 1：定義輸出路徑
指定所需的輸出檔案路徑和格式：
```java
String outputPath = "YOUR_OUTPUT_DIRECTORY/signedDocument.pdf"; // 根據需要更改格式
```
##### 第 2 步：設定儲存選項
配置 `SpreadsheetSaveOptions` 定義文檔的儲存方式：
```java
SpreadsheetSaveOptions saveOptions = new SpreadsheetSaveOptions();
saveOptions.setFileFormat(SpreadsheetSaveFileFormat.Pdf); // 可以改變為不同的格式
saveOptions.setOverwriteExistingFiles(true);
```
##### 步驟3：實施簽章操作
在簽名操作中使用這些選項。確保 `signature` 物件已正確初始化：
```java
// 使用範例（假設簽名物件存在）
signature.sign(outputPath, signOptions, saveOptions);
```
## 實際應用
以下是此功能可以發揮作用的一些實際場景：
- **法律文件**：使用二維碼安全簽署合同，以便於驗證。
- **財務報告**：在包含敏感財務資料的電子表格中新增簽名。
- **庫存管理**：在庫存表上使用二維碼，以簡化追蹤和身份驗證。

## 性能考慮
處理文件簽名時，請考慮以下提示：
- 透過分析簽章操作期間的資源使用量來最佳化 Java 記憶體管理。
- GroupDocs.Signature 針對效能進行了最佳化，但請確保您在合適的環境中運行它以有效地處理大型文件。

## 結論
現在，您應該已經能夠熟練使用 GroupDocs.Signature 來簽署並保存帶有二維碼的 Excel 電子表格。這款強大的工具可以顯著增強您數位文件的安全性和真實性。接下來，您可以探索其他功能，例如文字簽名或圖章簽名，以進一步保護您的文件。

**號召性用語**：立即嘗試在您的專案中實施這些解決方案！

## 常見問題部分
1. **GroupDocs.Signature 支援哪些格式？**
   - 它支援 PDF、XLSX、DOCX 等。
2. **如何解決簽名問題？**
   - 檢查異常訊息以尋找線索；確保所有檔案路徑正確。
3. **是否可以在一份文件中籤署多頁？**
   - 是的，在您的簽名選項中指定頁碼。
4. **GroupDocs.Signature 可以在 Web 應用程式中使用嗎？**
   - 絕對的，它非常適合伺服器端 Java 應用程式。
5. **如果需要，我如何獲得支持？**
   - 使用 [GroupDocs 支援論壇](https://forum.groupdocs.com/c/signature) 尋求幫助。

## 資源
- **文件**：可以在以下位置找到綜合指南和 API 參考 [GroupDocs 文檔](https://docs。groupdocs.com/signature/java/).
- **API 參考**：詳細資訊請參閱 [API 參考頁面](https://reference。groupdocs.com/signature/java/).
- **下載**：造訪最新版本 [GroupDocs 發布](https://releases。groupdocs.com/signature/java/).
- **購買和許可**：詳細了解許可選項，請訪問 [GroupDocs 購買](https://purchase.groupdocs.com/buy) 並透過以下方式獲得免費試用 [GroupDocs 免費試用](http://www.groupdocs.com/pricing)