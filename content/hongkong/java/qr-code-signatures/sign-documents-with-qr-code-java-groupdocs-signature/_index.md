---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature 在 Java 中透過二維碼對文件進行電子簽署。增強文件管理系統的安全性和效率。"
"title": "使用 Java 和 GroupDocs.Signature 透過二維碼簽署文件－綜合指南"
"url": "/zh-hant/java/qr-code-signatures/sign-documents-with-qr-code-java-groupdocs-signature/"
"weight": 1
type: docs
---
# 使用 Java 和 GroupDocs.Signature 透過二維碼簽署文檔

您是否希望為您的文件管理系統增添額外的安全性和效率？在當今的數位時代，電子簽名文件是一項必備功能，而二維碼簽名兼具便利性和可靠性。在本指南中，我們將探索如何使用 GroupDocs.Signature for Java 為影像文件新增二維碼簽章。完成本教學後，您將能夠無縫地實現這些功能。

## 您將學到什麼
- 在您的專案中為 Java 設定 GroupDocs.Signature
- 建立和配置二維碼簽名選項
- 為不同的輸出格式配置影像儲存選項
- 使用二維碼簽署文件的實際應用

讓我們開始這段令人興奮的旅程吧！

### 先決條件
在深入實施之前，請確保您已涵蓋以下內容：

- **庫和依賴項：** 您需要 GroupDocs.Signature 庫。請確保使用 23.12 版本以確保相容性。
- **環境設定：** 本指南假設您對 Maven 或 Gradle 等 Java 開發環境有基本的了解。
- **知識前提：** 熟悉 Java 程式設計、Java 檔案處理以及 XML/Gradle 建置檔案的基本知識是有益的。

### 為 Java 設定 GroupDocs.Signature
若要開始使用 GroupDocs.Signature for Java，請透過 Maven 或 Gradle 將相依性新增至您的專案：

**Maven：**
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

**Gradle：**
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

或者，直接從 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

要開始試用或購買：
- **免費試用和許可證獲取：** 訪問 [GroupDocs 免費試用](https://releases.groupdocs.com/signature/java/) 下載該庫。
- **臨時執照：** 如果您需要更多時間進行評估，請申請臨時許可證 [GroupDocs 臨時許可證](https://purchase。groupdocs.com/temporary-license/).
- **購買：** 如需完整功能和支持，請透過以下方式購買許可證 [GroupDocs 購買](https://purchase。groupdocs.com/buy).

#### 基本初始化
在專案中設定庫後，按如下方式初始化它：
```java
import com.groupdocs.signature.Signature;

public class InitializeSignature {
    public void setup() {
        Signature signature = new Signature("SampleImage.jpg");
        // 您的初始化程式碼在這裡...
    }
}
```

### 實施指南
現在您已完成所有設置，讓我們實現二維碼簽名功能。

#### 使用二維碼簽名簽署文件
本節將引導您使用 GroupDocs.Signature for Java 為影像文件新增二維碼簽章。

**步驟：**
1. **建立簽名實例：** 初始化 `Signature` 與您的文件路徑相關的類別。
   ```java
   String filePath = "YOUR_DOCUMENT_DIRECTORY/SampleImage.jpg";
   Signature signature = new Signature(filePath);
   ```

2. **配置二維碼簽名選項：** 設定二維碼選項，指定文字和位置。
   ```java
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;

   QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
   signOptions.setEncodeType(QrCodeTypes.QR);
   signOptions.setLeft(100);  // 從左側開始定位
   signOptions.setTop(100);   // 從頂部開始定位
   ```

3. **設定影像儲存選項：** 定義已簽署文件的儲存方式和位置。
   ```java
   import com.groupdocs.signature.options.saveoptions.imagessaveoptions.ImageSaveOptions;
   import com.groupdocs.signature.domain.enums.ImageSaveFileFormat;

   String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SaveSignedOutputType/SampleJPG.svg";
   ImageSaveOptions saveOptions = new ImageSaveOptions();
   saveOptions.setFileFormat(ImageSaveFileFormat.Svg);
   saveOptions.setOverwriteExistingFiles(true);
   ```

4. **簽署並儲存文件：** 使用配置的選項套用二維碼簽章。
   ```java
   try {
       signature.sign(outputFilePath, signOptions, saveOptions);
   } catch (Exception e) {
       throw new GroupDocsSignatureException(e.getMessage());
   }
   ```

#### 配置二維碼簽名選項
為了更好地控製文件的二維碼簽名：

**步驟：**
1. **建立和自訂二維碼選項：**
    ```java
    public QrCodeSignOptions createQRCodeOptions() {
        QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
        signOptions.setEncodeType(QrCodeTypes.QR);
        signOptions.setLeft(100);  // 根據需要自訂位置
        signOptions.setTop(100);
        
        return signOptions;
    }
    ```
   - `QrCodeSignOptions(String text)`：使用指定的文字初始化二維碼選項。
   - `setEncodeType(QrCodeTypes type)`：定義二維碼類型。
   - `setLeft(int left)` 和 `setTop(int top)`：將二維碼定位到文件上。

#### 配置輸出格式的影像儲存選項
控制已簽署文件的儲存位置以及儲存格式：

**步驟：**
1. **建立並設定影像儲存選項：**
    ```java
    public ImageSaveOptions createImageSaveOptions() {
        ImageSaveOptions saveOptions = new ImageSaveOptions();
        saveOptions.setFileFormat(ImageSaveFileFormat.Svg);  // 可以更改為其他格式，如 PNG、JPG。
        saveOptions.setOverwriteExistingFiles(true);
        
        return saveOptions;
    }
    ```
   - `setFileFormat(ImageSaveFileFormat format)`：確定輸出檔案的格式。
   - `setOverwriteExistingFiles(boolean overwrite)`：決定是否覆蓋現有文件。

### 實際應用
QR 碼簽名用途廣泛，可用於各種實際場景：
1. **合約簽訂：** 使用連結到數位驗證系統的二維碼安全地簽署合約。
2. **文件認證：** 使用二維碼作為驗證文件的防篡改方法。
3. **庫存管理：** 將二維碼附加到庫存物品上，以便輕鬆追蹤和簽署貨物。

### 性能考慮
在 Java 應用程式中實作 GroupDocs.Signature 時：
- **優化資源使用：** 透過在處理後關閉串流來確保高效的記憶體管理。
- **效能提示：** 如果有必要，請使用多線程處理大量文件。
- **最佳實踐：** 定期更新至 GroupDocs.Signature 的最新版本，以獲得更好的效能和新功能。

### 結論
在本教程中，您學習如何使用 GroupDocs.Signature 將二維碼簽章整合到您的 Java 應用程式中。此功能不僅可以增強文件安全性，還能簡化數位化工作流程。掌握本教學的知識後，您就可以在專案中運用這些強大的工具了。探索 GroupDocs.Signature 的其他功能，以獲得更強大的解決方案。

### 關鍵字推薦
- “使用 Java 實作二維碼簽名”
- “GroupDocs簽名實現”
- “電子文件簽名”