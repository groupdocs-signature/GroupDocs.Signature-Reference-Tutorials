---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 的二維碼加密和數位簽章來保護 PDF 文件。有效增強文件安全性。"
"title": "使用 GroupDocs.Signature 在 Java 中實作帶有二維碼加密的安全 PDF 簽名"
"url": "/zh-hant/java/qr-code-signatures/secure-pdf-signing-qr-code-groupdocs-java/"
"weight": 1
---

# 如何使用 GroupDocs.Signature 在 Java 中實現具有二維碼加密的安全 PDF 簽名

在當今的數位時代，保護文件中的敏感資訊至關重要。網路威脅的興起使得資料加密成為文件管理的重要組成部分。本教學將指導您使用 GroupDocs.Signature for Java 實現安全的 PDF 簽名，並使用二維碼加密。學完本文後，您將能夠將強大的安全功能整合到您的應用程式中。

## 您將學到什麼：
- 理解 Java 中的對稱資料加密
- 建立自訂簽名類
- 使用自訂資料和對齊方式配置二維碼簽名
- 整合 GroupDocs.Signature 實現安全的 PDF 簽名

準備好了嗎？讓我們開始吧！

## 先決條件
在開始之前，請確保您具備以下條件：
- **Java 開發工具包 (JDK)：** 版本 8 或更高版本。
- **Maven 或 Gradle：** 用於依賴管理。請根據您的項目設定進行選擇。
- **Java程式設計知識：** 對 Java 物件導向程式設計有基本的了解。

## 為 Java 設定 GroupDocs.Signature
要開始使用 GroupDocs.Signature，您需要將其新增為專案的依賴項。該庫提供了用於管理數位簽章和文件加密的強大工具。

### Maven 設定
將以下相依性新增至您的 `pom.xml` 文件：
```xml
<dependency>
    <groupId>com.groupdocs</groupId>
    <artifactId>groupdocs-signature</artifactId>
    <version>23.12</version>
</dependency>
```

### Gradle 設定
對於 Gradle 用戶，將其包含在您的 `build.gradle` 文件：
```gradle
implementation 'com.groupdocs:groupdocs-signature:23.12'
```

### 直接下載
或者，從下載最新版本 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 許可證獲取
您可以先免費試用 GroupDocs.Signature 來評估其功能。如需長期使用，請考慮購買許可證或透過其網站申請臨時許可證。

## 實施指南
本指南分為幾個主要部分，涵蓋資料加密、自訂簽章建立和二維碼簽章配置。

### 對稱演算法資料加密
加密資料可確保其在傳輸和預存程序中的安全性。以下是使用 GroupDocs.Signature 設定對稱加密的方法：

#### 設定對稱加密
1. **導入必要的套件：**
   ```java
   import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricAlgorithmType;
   import com.groupdocs.signature.domain.extensions.encryption.SymmetricEncryption;
   ```
2. **初始化加密物件：**
   使用安全金鑰和鹽進行加密。替換 `"YOUR_SECURE_KEY"` 使用您自己的鑰匙。
   ```java
   String key = "YOUR_SECURE_KEY";
   String salt = "YOUR_SECURE_SALT";

   IDataEncryption encryption = new SymmetricEncryption(
       SymmetricAlgorithmType.Rijndael, 
       key, 
       salt
   );
   ```
   - **對稱演算法類型.Rijndael：** 這指定了要使用的對稱演算法的類型。
   - **密鑰和鹽：** 確保這些對於您的應用程式來說是唯一的和安全的。

### 自訂資料簽名類
建立自訂類別可以讓你有效地管理簽名屬性。具體方法如下：

#### 定義 `DocumentSignatureData` 班級
```java
class DocumentSignatureData {
    private String ID;
    private String Author;
    private Date Signed = new Date();
    private BigDecimal DataFactor = new BigDecimal(0.01);

    public String getID() { return ID; }
    public void setID(String value) { ID = value; }

    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }

    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }

    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```
- **ID、作者、簽名：** 這些欄位儲存簽署的元資料。
- **數據因素：** 保存與應用程式邏輯相關的數值。

### QR碼簽名選項
二維碼提供了一種緊湊的資訊嵌入方式。您可以使用自訂資料和加密方式進行配置：

#### 設定二維碼簽名
1. **初始化 `Signature` 目的：**
   ```java
   import com.groupdocs.signature.Signature;
   
   Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY");
   ```
2. **配置二維碼選項：**
   ```java
   import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
   import com.groupdocs.signature.options.sign.QrCodeSignOptions;
   import java.util.UUID;

   DocumentSignatureData documentSignature = new DocumentSignatureData();
   documentSignature.setID(UUID.randomUUID().toString());
   documentSignature.setAuthor(System.getenv("USERNAME"));
   documentSignature.setDataFactor(new BigDecimal("11.22"));

   QrCodeSignOptions options = new QrCodeSignOptions();
   options.setData(documentSignature);
   options.setEncodeType(QrCodeTypes.QR);
   options.setDataEncryption(encryption); // 使用加密對象
   options.setHeight(100);
   options.setWidth(100);
   options.setVerticalAlignment(com.groupdocs.signature.domain.enums.VerticalAlignment.Bottom);
   options.setHorizontalAlignment(com.groupdocs.signature.domain.enums.HorizontalAlignment.Right);

   import com.groupdocs.signature.domain.Padding;
   Padding padding = new Padding();
   padding.setRight(10);
   padding.setBottom(10);
   options.setMargin(padding);
   ```
   - **編碼類型：** 指定二維碼格式。
   - **對齊和邊距：** 自訂二維碼在文件上的顯示方式。

### 範例用法
若要使用您配置的選項簽署文件：
```java
signature.sign("YOUR_OUTPUT_DIRECTORY/QRCodeEncryptedObject.pdf\