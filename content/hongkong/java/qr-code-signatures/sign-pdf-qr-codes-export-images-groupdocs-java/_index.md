---
"date": "2025-05-08"
"description": "了解如何透過使用二維碼簽署 PDF 並使用 GroupDocs.Signature for Java 將其匯出為映像來增強文件安全性。"
"title": "使用 QR 碼簽名對 PDF 進行簽名並使用 GroupDocs for Java 匯出為影像"
"url": "/zh-hant/java/qr-code-signatures/sign-pdf-qr-codes-export-images-groupdocs-java/"
"weight": 1
---

# 使用 GroupDocs.Signature for Java 簽署 PDF 並將其匯出為帶有二維碼的圖像的綜合指南

## 介紹

在數位時代，確保文件真實性對於金融、法律和醫療保健等行業至關重要。將電子簽名整合到文件中可以節省時間並提高安全性。本教學將指導您使用 GroupDocs.Signature for Java 將二維碼簽名新增至 PDF 並將其匯出為具有自訂邊框的影像。

**您將學到什麼：**
- 如何使用 GroupDocs.Signature 對帶有二維碼簽名的文件進行簽署。
- 如何使用自訂配置將簽署的文件匯出為影像。
- 使用 Java 數位簽章時優化效能的最佳實務。

讓我們先回顧一下實現這些功能之前的先決條件！

## 先決條件

開始之前，請確保你的開發環境已正確設定。本節概述了你需要了解和安裝的內容：

### 所需庫
您需要 GroupDocs.Signature for Java 函式庫。您可以使用 Maven 或 Gradle 將其新增至您的專案。請確保您使用的是該庫的 23.12 版本。

#### Maven 依賴
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

#### Gradle 實現
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下載
對於那些不喜歡使用建置工具的人，請從下載最新版本 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 環境設定要求
確保您的開發環境配備：
- JDK 8 或更高版本。
- IDE，例如 IntelliJ IDEA 或 Eclipse。

### 知識前提
熟悉 Java 程式設計並具備 Java 檔案處理的基本知識將有所幫助，但並非強制要求。我們將引導您完成每個步驟，確保清晰易懂。

## 為 Java 設定 GroupDocs.Signature

使用 GroupDocs.Signature 設定您的專案非常簡單：

1. **新增依賴項：**
   如果使用 Maven 或 Gradle，請在「先決條件」部分中新增如上所示的依賴項。

2. **許可證取得步驟：**
   - **免費試用：** 首先從下載免費試用版 [群組文檔](https://releases。groupdocs.com/signature/java/).
   - **臨時執照：** 對於不受評估限制的擴展測試，請申請臨時許可證 [臨時執照](https://purchase。groupdocs.com/temporary-license/).
   - **購買：** 要在生產中使用，請考慮從 [購買 GroupDocs](https://purchase。groupdocs.com/buy).

3. **基本初始化和設定：**

以下是初始化的範例：
```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public static void main(String[] args) throws Exception {
        // 使用文件路徑實例化簽章對象
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
        
        // 使用此“簽名”對象執行各種操作
    }
}
```

## 實施指南

### 文件上的二維碼簽名

#### 概述：
添加二維碼簽名可以增強安全性並驗證真實性。本節介紹如何使用 GroupDocs.Signature 對 PDF 進行二維碼簽章。

##### 導入必要的類別
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
```

##### 設定簽名對象
初始化你的 `Signature` 帶有 PDF 文件路徑的物件：
```java
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
```

##### 配置二維碼選項
建立並配置 `QrCodeSignOptions` 實例。包括設定二維碼的內容、在頁面上的位置以及指定其為二維碼類型。
```java
QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith"); // 設定二維碼內容

signOptions.setEncodeType(QrCodeTypes.QR); // 指定二維碼類型
signOptions.setLeft(100); // 簽名位置的 X 座標
signOptions.setTop(100); // 簽名位置的 Y 座標
```

##### 簽署並儲存文檔
使用 `sign` 應用二維碼簽名並儲存的方法：
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/signedWithQRCode.png", signOptions);
```

#### 故障排除提示：
- 確保您的文件路徑正確。
- 驗證所有相依性是否均已正確新增。

### 使用自訂邊框和頁面設定將文件匯出為圖像

#### 概述：
此功能示範如何將簽署的 PDF 匯出為影像，並附帶自訂邊框和頁面配置。它非常適合以視覺化格式呈現文件。

##### 導入必要的類別
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Border;
import com.groupdocs.signature.domain.enums.DashStyle;
import com.groupdocs.signature.domain.ImageSaveFileFormat;
import com.groupdocs.signature.options.saveoptions.ExportImageSaveOptions;
import java.awt.Color;
```

##### 設定簽名對象
和以前一樣，初始化你的 `Signature` 具有文檔路徑的物件：
```java
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.pdf");
```

##### 配置匯出選項
建立一個實例 `ExportImageSaveOptions`。在這裡，您可以定義圖像格式、邊框屬性和頁面設定。
```java
ExportImageSaveOptions exportImageSaveOptions = new ExportImageSaveOptions(ImageSaveFileFormat.Png);

Border border = new Border();
border.setColor(Color.BLUE); // 將邊框顏色設定為藍色
border.setWeight(5); // 設定邊框寬度
border.setDashStyle(DashStyle.Solid); // 設定邊框的虛線樣式
border.setTransparency(0.5); // 設定邊框透明度

exportImageSaveOptions.setBorder(border);
exportImageSaveOptions.setPagesSetup(new PagesSetup());
exportImageSaveOptions.getPagesSetup().setFirstPage(true); // 僅匯出第一頁
exportImageSaveOptions.setPageColumns(2); // 設定佈局的列數
```

##### 簽名並儲存為圖像
套用匯出選項將文件儲存為圖片：
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/signedAndSavedAsImage.png", null, exportImageSaveOptions);
```

#### 故障排除提示：
- 檢查輸出檔案的格式相容性。
- 確保所有自訂都適合頁面尺寸。

## 實際應用

1. **法律文件：** 使用二維碼簽名增強法律合同，以便於驗證和以數位格式儲存。
2. **教育部門：** 對學術證書進行數位簽名並將其匯出為圖像以供分發。
3. **商業合約：** 透過允許電子簽名和生成可共享的圖像版本來簡化合約流程。

## 性能考慮

處理大型文件或高解析度影像時，請考慮以下事項：
- 透過在 Java 中有效管理資源來優化記憶體使用情況。
- 使用適當的資料結構來處理文件處理任務。
- 定期分析您的應用程式以識別瓶頸。

## 結論

透過本指南，您學習如何使用 GroupDocs.Signature for Java 有效地使用二維碼對 PDF 進行簽名，並將其匯出為圖片。這些工具可以顯著提昇文件的安全性和美觀度。

下一步包括試驗 GroupDocs.Signature 提供的附加功能或將其整合到更大的系統中，例如文件管理平台。

## 常見問題部分

1. **什麼是 GroupDocs.Signature？**
   - 一個全面的庫，用於在 Java 中為各種文件格式添加電子簽名，增強文件的安全性和真實性。