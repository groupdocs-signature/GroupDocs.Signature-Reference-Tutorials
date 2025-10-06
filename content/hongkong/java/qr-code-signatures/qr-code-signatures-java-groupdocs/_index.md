---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature 在 Java 中實作和驗證二維碼簽名，從而增強文件安全性。請按照本逐步指南，了解如何安全簽名。"
"title": "保護您的文件 &#58; 使用 GroupDocs.Signature 在 Java 中實作二維碼簽名"
"url": "/zh-hant/java/qr-code-signatures/qr-code-signatures-java-groupdocs/"
"weight": 1
type: docs
---
# 保護您的文件：使用 GroupDocs.Signature 在 Java 中實作二維碼簽名

在當今的數位環境中，確保合約、發票或敏感個人資訊等文件的安全至關重要。增強文件安全性並簡化驗證流程的創新方法是使用二維碼簽名。本教學將指導您使用 GroupDocs.Signature 在 Java 中為文件實作和驗證二維碼簽章。

## 您將學到什麼
- 如何使用二維碼簽署文件
- 使用二維碼驗證已簽署的文件
- 在文件中搜尋現有的二維碼簽名
- 更新並刪除文件中的二維碼簽名

讓我們設定您的環境並開始吧！

### 先決條件
在開始之前，請確保您符合以下先決條件：

#### 所需的庫和依賴項
您需要 GroupDocs.Signature for Java。您可以透過 Maven 或 Gradle 將其添加，或直接下載。

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

**直接下載**
從下載最新版本 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

#### 環境設定要求
- 確保您已安裝 Java 開發工具包 (JDK) 8 或更高版本。
- 使用 IntelliJ IDEA、Eclipse 或 NetBeans 等 IDE。

#### 知識前提
對 Java 程式設計和文件處理有基本的了解是有益的。

## 為 Java 設定 GroupDocs.Signature
若要在您的專案中使用 GroupDocs.Signature，請依照下列步驟操作：
1. **安裝**：根據您的設定在 Maven、Gradle 或直接下載之間進行選擇。
2. **許可證獲取**：
   - 從免費試用開始 [GroupDocs 網站](https://releases。groupdocs.com/signature/java/).
   - 考慮從以下機構取得臨時許可證，以進行擴展測試和開發： [這裡](https://purchase。groupdocs.com/temporary-license/).
3. **基本初始化**： 
    初始化 GroupDocs.Signature 的方法如下：

    ```java
    Signature signature = new Signature("YOUR_DOCUMENT_PATH");
    ```

這為您實施二維碼簽名做好了準備。

## 實施指南

### 使用二維碼簽名簽署文件
#### 概述
使用二維碼簽署文件需要嵌入一個代表您數位簽名的唯一代碼。此流程可確保文件安全，並方便日後驗證其真實性。

##### 步驟 1：設定您的簽名選項
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

Signature signature = new Signature("YOUR_DOCUMENT_PATH");
QrCodeSignOptions signOptions = new QrCodeSignOptions("John Smith", com.groupdocs.signature.domain.qrcodes.QrCodeTypes.QR);

signOptions.setVerticalAlignment(VerticalAlignment.Top);
signOptions.setHorizontalAlignment(HorizontalAlignment.Center);
signOptions.setWidth(100);
signOptions.setHeight(40);
```
**解釋**： `QrCodeSignOptions` 配置為建立具有特定文字和對齊方式的二維碼。根據需要調整寬度和高度。

##### 步驟 2：自訂簽名外觀
```java
import java.awt.Color;

signOptions.setForeColor(Color.RED); // 設定二維碼顏色
com.groupdocs.signature.domain.SignatureFont signatureFont = new com.groupdocs.signature.domain.SignatureFont();
signatureFont.setSize(12);
signatureFont.setFamilyName("Comic Sans MS");
signOptions.setFont(signatureFont);
```
**解釋**：自訂字體和顏色可增強視覺識別。

##### 步驟3：簽署文件
```java
import java.util.ArrayList;
import java.util.List;

List<String> signatureIds = new ArrayList<>();
List<com.groupdocs.signature.domain.BaseSignature> signedSignatures = signature.sign("YOUR_OUTPUT_PATH", signOptions).getSucceeded();

for (com.groupdocs.signature.domain.BaseSignature temp : signedSignatures) {
    signatureIds.add(temp.getSignatureId());
}
```
**解釋**：此步驟對文件進行簽名並儲存簽名 ID 以供日後參考。

### 使用二維碼簽名驗證文檔
#### 概述
驗證可確保文件已合法簽署。以下是如何驗證文件中二維碼簽名的方法。

##### 步驟 1：設定驗證選項
```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.verify.QrCodeVerifyOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeVerifyOptions verifyOptions = new QrCodeVerifyOptions();

verifyOptions.setEncodeType(QrCodeTypes.QR);
verifyOptions.setText("John Smith"); // 簡訊驗證
verifyOptions.setAllPages(false); 
verifyOptions.setPageNumber(1);
```
**解釋**：驗證選項指定要尋找的二維碼類型和文本，確保簽名符合您的期望。

##### 第 2 步：執行驗證
```java
boolean isValid = signature2.verify(verifyOptions).isValid();
System.out.println("Is Signature Valid? " + isValid);
```
**解釋**：這將檢查文件是否包含符合您條件的有效二維碼。

### 搜尋文檔中的二維碼簽名
#### 概述
有時需要在文件中尋找現有簽章。以下是使用 GroupDocs.Signature 搜尋簽名的方法。

##### 步驟 1：配置搜尋選項
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import com.groupdocs.signature.options.search.QrCodeSearchOptions;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
QrCodeSearchOptions searchOptions = new QrCodeSearchOptions();
searchOptions.setAllPages(true);
```
**解釋**：這將設定工具來掃描所有頁面上的二維碼簽名。

##### 第 2 步：執行搜尋
```java
List<QrCodeSignature> signatures = signature2.search(QrCodeSignature.class, searchOptions);

for (QrCodeSignature qrSignature : signatures) {
    System.out.println("Found Signature ID: " + qrSignature.getSignatureId());
}
```
**解釋**：這將檢索文件中找到的所有二維碼簽名。

### 更新文檔二維碼簽名
#### 概述
更新簽章涉及更改其屬性，例如位置或大小。操作方法如下：

##### 步驟 1：準備更新簽名
```java
import com.groupdocs.signature.domain.signatures.QrCodeSignature;
import java.io.ByteArrayOutputStream;

Signature signature2 = new Signature("YOUR_OUTPUT_PATH");
List<QrCodeSignature> signaturesToUpdate = new ArrayList<>();

// 假設「簽名」是透過搜尋獲得的 QrCodeSignature 物件列表
for (QrCodeSignature qrSignature : signatures) {
    qrSignature.setLeft(qrSignature.getLeft() + 100);
    qrSignature.setTop(qrSignature.getTop() + 100);
    qrSignature.setWidth(200);
    qrSignature.setHeight(50);
    signaturesToUpdate.add(qrSignature);
}
```
**解釋**：調整每個簽名的位置和大小。

##### 第 2 步：更新文檔
```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();
signature2.update(outputStream, signaturesToUpdate);
```
**解釋**：文件已使用修改後的二維碼簽章進行更新。

### 刪除文檔二維碼按ID簽名
#### 概述
如果簽名不再需要或錯誤添加，則可能需要刪除該簽名。您可以使用其唯一 ID 將其刪除，具體方法如下。

##### 步驟 1：識別要刪除的簽名
```java
import com.groupdocs.signature.domain.SignatureCollection;
import java.util.Arrays;

SignatureCollection signaturesToDelete = signature2.search(QrCodeSignature.class);
Arrays.stream(signaturesToDelete).forEach(signature -> {
    if (signature.getSignatureId().equals("YOUR_SIGNATURE_ID")) {
        signature.delete();
    }
});
```
**解釋**：透過其唯一 ID 尋找並刪除二維碼簽名。

## 結論
本指南已引導您使用 GroupDocs.Signature 在 Java 中使用二維碼簽章來保護文件安全。遵循這些步驟，您可以確保文件安全簽名，並輕鬆驗證其真實性。