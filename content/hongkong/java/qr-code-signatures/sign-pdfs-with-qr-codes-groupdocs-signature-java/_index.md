---
"date": "2025-05-08"
"description": "學習如何使用 GroupDocs.Signature for Java 安全地使用二維碼對 PDF 文件進行簽署。本教程涵蓋設定、實作和實際應用。"
"title": "如何使用 GroupDocs.Signature for Java 為 PDF 簽署二維碼"
"url": "/zh-hant/java/qr-code-signatures/sign-pdfs-with-qr-codes-groupdocs-signature-java/"
"weight": 1
type: docs
---
# 如何使用 GroupDocs.Signature for Java 為 PDF 文件簽署二維碼

在當今的數位時代，安全地簽署文件比以往任何時候都更加重要。無論您是商務人士還是想要驗證文件的個人，合適的工具都能發揮重要作用。本教學將指導您如何使用 **GroupDocs.Signature for Java** 使用包含 Mailmark2D 物件等複雜資料的二維碼對 PDF 文件進行簽署。我們將涵蓋從環境設定到高級功能實現的所有內容。

## 您將學到什麼
- 如何為 Java 設定 GroupDocs.Signature
- 建立和配置用於簽名 PDF 的二維碼
- 利用 Mailmark2D 物件進行複雜的資料編碼
- 此功能在實際場景中的實際應用

準備好開始了嗎？我們先來了解先決條件。

## 先決條件
在開始之前，請確保您已：
- **Java 開發工具包 (JDK)**：版本 8 或更高版本。
- **整合開發環境 (IDE)** 例如 IntelliJ IDEA 或 Eclipse。
- 對 Java 程式設計和 Maven/Gradle 建置工具有基本的了解。

### 所需的庫和依賴項
要使用 GroupDocs.Signature for Java，您需要將該程式庫新增至您的專案。具體方法如下：

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

**直接下載：**  
對於不使用建置管理員的用戶，請從下載最新版本 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 許可證獲取
GroupDocs 提供多種授權選項：
- **免費試用**：從試用開始探索功能。
- **臨時執照**：取得臨時許可證以進行延長測試。
- **購買**：購買用於生產用途的完整許可證。

## 為 Java 設定 GroupDocs.Signature
準備好環境並包含庫後，初始化 GroupDocs.Signature。此設定對於存取其所有功能至關重要：

```java
import com.groupdocs.signature.Signature;

class SetupGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
        // 現在您可以使用“簽名”來簽署文件。
    }
}
```

## 實施指南
### 使用二維碼簽署文件
#### 概述
此功能可讓您在 PDF 文件中新增二維碼作為數位簽章。二維碼將包含 Mailmark2D 物件中編碼的複雜資料。

**步驟1：導入所需的包**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;
```

**步驟2：設定檔案路徑並初始化簽名對象**
設定來源文檔和輸出檔案的路徑。初始化 `Signature` 帶有 PDF 路徑的物件：

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY";
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignWithQRCodeMailmark2DObject.pdf";

final Signature signature = new Signature(filePath);
```

**步驟 3：建立二維碼簽名選項**
使用類型、位置和資料等特定設定配置二維碼：

```java
QrCodeSignOptions options = new QrCodeSignOptions();
options.setEncodeType(QrCodeTypes.QR); // 設定二維碼類型
options.setLeft(100); // 放置的 X 座標
options.setTop(100);  // 放置的 Y 座標
```

**步驟4：簽署文件**
執行簽名流程並儲存簽名後的文件：

```java
try {
    signature.sign(outputFilePath, options);
} finally {
    if (signature != null) signature.dispose();
}
```

### 建立 Mailmark2D 資料對象
#### 概述
Mailmark2D 物件用於在二維碼中編碼複雜資料。本節介紹如何設定此物件。

**步驟1：導入所需的包**

```java
import com.groupdocs.signature.domain.extensions.mailmark2d.Mailmark2D;
import com.groupdocs.signature.domain.extensions.mailmark2d.Mailmark2DType;
import com.groupdocs.signature.domain.extensions.serialization.DataMatrixEncodeMode;
```

**步驟2：初始化並配置Mailmark2D對象**
設定 Mailmark2D 物件的各種屬性來定義複雜資料：

```java
Mailmark2D mailmark2D = new Mailmark2D();
mailmark2D.setUPUCountryID("JGB "); // 郵政服務國家/地區 ID
mailmark2D.setInformationTypeID("0"); // 資訊類型標識符
mailmark2D.setClass("1"); // 郵件處理類
mailmark2D.setSupplyChainID(123); // 供應鏈標識
mailmark2D.setItemID(1234); // 唯一商品 ID
mailmark2D.setDestinationPostCodeAndDPS("QWE1"); // 目的地郵遞區號
mailmark2D.setRTSFlag("0"); // 退回寄件者標誌
mailmark2D.setReturnToSenderPostCode("QWE2"); // 退貨郵遞區號
mailmark2D.setDataMatrixType(Mailmark2DType.Type_7); // 資料矩陣類型
mailmark2D.setCustomerContentEncodeMode(DataMatrixEncodeMode.C40); // 編碼模式
mailmark2D.setCustomerContent("CUSTOM"); // 自訂內容
```

## 實際應用
1. **法律文件認證**：確保法律文件已簽署並通過二維碼驗證。
2. **發票處理**：將二維碼附加到發票上，以便於追蹤和驗證。
3. **運輸標籤**：使用運輸標籤上的二維碼來編碼詳細的追蹤資訊。
4. **活動門票**：透過在門票上的二維碼中嵌入活動詳情來增強安全性。
5. **供應鏈管理**：使用二維碼 Mailmark2D 資料簡化物流。

## 性能考慮
- 透過有效管理記憶體使用量來優化效能，尤其是在處理大型 PDF 檔案時。
- 如果整合到 Web 應用程序，請使用非同步處理以避免阻塞操作。
- 定期更新 GroupDocs.Signature 以利用改進和錯誤修復。

## 結論
透過本指南，您學習如何使用 GroupDocs.Signature for Java 為具有二維碼的 PDF 文件簽署。這項強大的功能可以整合到各種工作流程中，以增強文件安全性並簡化流程。為了進一步探索 GroupDocs.Signature 的功能，您可以嘗試不同的配置或將其與其他系統整合。

## 常見問題部分
1. **我可以免費使用 GroupDocs.Signature 嗎？**  
   是的，您可以先免費試用一下，測試其功能。
2. **可以使用該庫簽署哪些類型的文件？**  
   除了 PDF，您還可以簽署圖像、Word 文件、Excel 電子表格等。
3. **如何解決簽名錯誤？**  
   檢查錯誤日誌中的特定訊息並確保所有相依性都已正確配置。
4. **我可以自訂二維碼的外觀嗎？**  
   是的，您可以使用下列方式調整大小、位置和其他屬性 `QrCodeSignOptions`。
5. **可以一次簽署多份文件嗎？**  
   雖然 GroupDocs.Signature 一次處理一個文檔，但您可以編寫批次腳本以提高效率。

## 資源
- **文件**： [GroupDocs.Signature Java 文檔](https://docs.groupdocs.com/signature/java/)
- **API 參考**： [GroupDocs 簽章 API 參考](https://reference.groupdocs.com/signature/java/)
- **下載**： [GroupDocs.Signature 發布](https://releases.groupdocs.com/signature/java/)
- **購買**： [購買 GroupDocs 許可證](https://purchase.groupdocs.com/buy)
- **免費試用**： [開始免費試用](https://releases.groupdocs.com/signature/java/)
- **臨時執照**： [申請臨時執照](https://purchase.groupdocs.com/temporary-license/)
- **支援**： [GroupDocs 論壇](https://forum.groupdocs.com/c/signature/)

利用這些資源，您可以加深對 GroupDocs.Signature 的理解，並在您的應用程式中擴展其功能。祝您編碼愉快！