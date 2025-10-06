---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature 在 Java 中產生安全動態的二維碼簽章。輕鬆簡化文件簽名流程。"
"title": "使用 GroupDocs.Signature for Java 產生二維碼簽章－綜合指南"
"url": "/zh-hant/java/qr-code-signatures/generate-qr-code-signatures-groupdocs-java/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature for Java 產生二維碼簽名

## 介紹

在當今的數位時代，文件安全至關重要。無論您處理的是合約、發票還是協議，確保簽名的準確性和安全性都可能頗具挑戰性。 **GroupDocs.Signature for Java** 提供強大的解決方案來簡化在您的文件中添加數位簽章的過程。

本教學將指導您使用 GroupDocs.Signature for Java 產生二維碼簽名，從而增強在文件中嵌入附加資料的安全性和靈活性。透過學習，您將學習：

- 為 Java 設定和配置 GroupDocs.Signature。
- 產生具有精確對齊設定二維碼簽章的技術。
- 配置簽名預覽選項以全面查看已簽署的文件。
- 產生簽名流以確保無縫文件處理。

讓我們深入探討如何在 Java 應用程式中實現這些功能。首先，讓我們介紹一些先決條件，以便您順利入門。

## 先決條件

在使用 GroupDocs.Signature for Java 之前，請確保符合以下要求：

- **庫和依賴項**：安裝必要的庫。使用 Maven 或 Gradle 來管理相依性。
  
  **Maven**
  ```xml
  <dependency>
      <groupId>com.groupdocs</groupId>
      <artifactId>groupdocs-signature</artifactId>
      <version>23.12</version>
  </dependency>
  ```

  **Gradle**
  ```gradle
  implementation 'com.groupdocs:groupdocs-signature:23.12'
  ```

- **環境設定**：確保您擁有具有 JDK 和 IntelliJ IDEA 或 Eclipse 等 IDE 的 Java 開發環境。

- **知識前提**：熟悉 Java 程式設計概念以及了解數位簽章至關重要。

接下來，我們將指導您在專案環境中為 Java 設定 GroupDocs.Signature。

## 為 Java 設定 GroupDocs.Signature

若要開始使用 GroupDocs.Signature for Java，請依照下列步驟操作：

1. **新增依賴項**：使用 Maven 或 Gradle 包含依賴項，如上所示。
2. **許可證獲取**：
   - 從下載免費試用版開始 [GroupDocs 發布](https://releases。groupdocs.com/signature/java/).
   - 如需延長使用時間，請考慮購買許可證或透過其申請臨時許可證 [購買頁面](https://purchase。groupdocs.com/buy).
3. **基本初始化**：
   在您的 Java 應用程式中初始化該程式庫以開始使用其功能。

   ```java
   import com.groupdocs.signature.Signature;
   
   // 初始化簽名對象
   Signature signature = new Signature("sample.pdf");
   ```

配置好 GroupDocs.Signature for Java 後，就可以產生二維碼簽章了。讓我們深入了解具體細節。

## 實施指南

### 產生二維碼簽名

建立二維碼簽章涉及幾個關鍵步驟。每個步驟都有助於自訂資料在文件中的嵌入和顯示方式。

#### 概述
二維碼簽章用途廣泛；它允許您將複雜的資訊（例如地址、URL 或二進位資料）直接嵌入到文件中。讓我們看看如何使用 GroupDocs.Signature for Java 產生具有特定對齊設定的二維碼簽章。

#### 逐步實施

##### 1. 配置二維碼選項
首先設定 `QrCodeSignOptions` 對象。您可以在此處指定二維碼的類型及其應包含的資料。

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.extensions.serialization.Address;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

QrCodeSignOptions signOptions = new QrCodeSignOptions();
signOptions.setEncodeType(QrCodeTypes.QR);

// 使用地址對象設定數據
Address address = new Address();
address.setStreet("221B Baker Street");
address.setCity("London");
address.setState("NW");
address.setZIP("NW16XE");
address.setCountry("England");

signOptions.setData(address);
```
**解釋**：這裡我們設定二維碼類型為標準 `QR` 並填入地址資訊。此資料封裝可確保文件中的重要資訊隨時可用。

##### 2. 對齊二維碼
調整對齊設定以控制二維碼在文件頁面上出現的位置。

```java
signOptions.setHorizontalAlignment(HorizontalAlignment.Left);
signOptions.setVerticalAlignment(VerticalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(100);
```
**解釋**：對齊選項（`HorizontalAlignment` 和 `VerticalAlignment`可讓您精確定位二維碼。此步驟可確保二維碼美觀且位置合理，從而達到最佳掃描效果。

##### 3.設定邊距
定義二維碼周圍的邊距，以確保它不會接觸到文件的邊緣，這對於掃描的可靠性非常重要。

```java
signOptions.setMargin(new Padding(10));
```
**解釋**：此處使用 `Padding`，確保二維碼和文件邊緣之間有空間，以提高可掃描性。

### 配置簽名預覽選項

設定預覽選項可讓您在最終確定簽名之前直觀地看到最終效果。操作方法如下：

#### 概述
預覽設定對於驗證文件中簽名的外觀至關重要。

#### 逐步實施

##### 1. 建立並配置 PreviewOptions
利用 `PreviewSignatureOptions` 定義如何預覽簽名。

```java
import com.groupdocs.signature.options.PreviewSignatureOptions;
import com.groupdocs.signature.options.preview.PreviewFormats;
import java.util.UUID;

PreviewSignatureOptions previewOption = new PreviewSignatureOptions(signOptions);
previewOption.setSignatureId(UUID.randomUUID().toString());
previewOption.setPreviewFormat(PreviewFormats.JPEG);
```
**解釋**： 這 `PreviewSignatureOptions` 物件配置為產生二維碼的 JPEG 預覽。每個簽名的唯一識別碼（`UUID`) 確保您可以有效地追蹤和管理多個簽名。

### 產生簽名流

產生流可確保您的簽章文件已正確儲存或傳輸。

#### 概述
建立文件流可以無縫處理已簽署的文檔，確保其正確儲存在指定的目錄中。

#### 逐步實施

##### 1. 定義輸出目錄並產生流
確保生成流之前輸出目錄存在，以避免文件寫入過程中出現錯誤。

```java
import java.io.FileOutputStream;
import java.io.OutputStream;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public OutputStream generateSignatureStream(PreviewSignatureOptions previewOptions) {
    try {
        Path path = Paths.get("YOUR_OUTPUT_DIRECTORY");
        if (!Files.exists(path)) {
            Files.createDirectories(path);
        }
        
        // 建立輸出流來保存簽署的文檔
        return new FileOutputStream(path.resolve("signedDocument.pdf"));
    } catch (Exception e) {
        e.printStackTrace();
        return null;
    }
}
```
**解釋**：此方法檢查指定目錄是否存在，並在必要時創建，然後返回用於保存文件的文件輸出流。處理目錄可確保已簽署的文件以有序的方式儲存。

## 結論

透過本指南，您學習如何使用 GroupDocs.Signature for Java 產生二維碼簽名，從而增強了在文件中嵌入附加資料的安全性和靈活性。遵循這些步驟，您可以自信地在 Java 應用程式中實現數位簽章功能。

為了進一步探索，請考慮嘗試不同類型的簽章或探索 GroupDocs.Signature for Java 提供的其他功能。