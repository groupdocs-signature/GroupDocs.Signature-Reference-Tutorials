---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature 實作 Java 二維碼簽章。增強文件安全性、配置簽名選項並在 Java 應用程式中套用自訂加密。"
"title": "Java QR 碼簽署指南 &#58; 使用 GroupDocs.Signature 保護您的文檔"
"url": "/zh-hant/java/qr-code-signatures/java-qr-code-signing-groupdocs-signature/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature for Java 實作 Java QR 碼簽名

## 介紹

透過在 Java 應用程式中嵌入二維碼，增強數位文件的安全性。利用 GroupDocs.Signature for Java，您可以有效確保文件的真實性和可追溯性。本指南將指導您建立自訂資料簽章、配置二維碼簽章選項，並使用強大的加密技術保護您的文件。

**您將學到什麼：**
- 如何使用 GroupDocs.Signature 建立自訂資料簽章類
- 在 Java 應用程式中配置二維碼簽名選項
- 使用二維碼簽署文件並套用自訂加密

讓我們深入了解先決條件並開始將此功能整合到您的專案中！

## 先決條件

在開始之前，請確保您已經在開發環境中設定了必要的程式庫和相依性。

### 所需的庫和版本

若要為 Java 實作 GroupDocs.Signature，請包含下列相依性：

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
implementation 'com.groupdocs:groupdocs-signation:23.12'
```

您也可以直接從 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 環境設定要求

- 確保您已安裝可運行的 Java 開發工具包 (JDK)。
- 設定您的整合開發環境 (IDE)，例如 IntelliJ IDEA 或 Eclipse。

### 知識前提

- 對 Java 程式設計和物件導向概念有基本的了解。
- 熟悉使用 Maven 或 Gradle 處理依賴項。

## 為 Java 設定 GroupDocs.Signature

首先，請按照上面的安裝說明在您的專案中設定 GroupDocs.Signature，並將其包含在您的建置配置中。

### 許可證取得步驟

GroupDocs 提供不同的授權選項：
- **免費試用**：無限制測試所有功能。
- **臨時執照**：取得用於評估目的的許可證。
- **購買**：獲得商業使用的完整許可。

下載後，像這樣初始化 GroupDocs.Signature：

```java
import com.groupdocs.signature.Signature;

class InitializeGroupDocs {
    public static void main(String[] args) {
        Signature signature = new Signature("path/to/your/document");
        // 現在您可以開始使用簽名物件來處理文件。
    }
}
```

## 實施指南

讓我們將實施過程分解為易於管理的部分，並專注於關鍵特性。

### 自訂資料簽名類

#### 概述
建立一個自訂類別來儲存簽名數據，例如 ID、作者、簽名日期和其他因素。這可確保您的簽名中封裝了所有必要的元資料。

#### 逐步實施

**定義 DocumentSignatureData 類別**

```java
import com.groupdocs.signature.domain.extensions.serialization.FormatAttribute;
import java.util.Date;
import java.math.BigDecimal;

class DocumentSignatureData {
    @FormatAttribute(propertyName = "SignID")
    public String ID; // 簽名的唯一識別符
    
    public String getID() { return ID; }
    public void setID(String value) { ID = value; }
    
    @FormatAttribute(propertyName = "SAuth")
    public final String Author; // 文件的作者
    
    public final String getAuthor() { return Author; }
    public final void setAuthor(String value) { Author = value; }
    
    @FormatAttribute(propertyName = "SDate", propertyFormat = "yyyy-MM-dd")
    public final Date Signed = new Date(); // 簽署日期和時間
    
    public final Date getSigned() { return Signed; }
    public final void setSigned(Date value) { Signed = value; }
    
    @FormatAttribute(propertyName = "SDFact", propertyFormat = "N2")
    public final BigDecimal DataFactor = new BigDecimal(0.01); // 簽署的附加資料因素
    
    public final BigDecimal getDataFactor() { return DataFactor; }
    public final void setDataFactor(BigDecimal value) { DataFactor = value; }
}
```

**解釋：**
- **格式屬性**：註釋屬性以自訂序列化。
- **特性**：擷取必要的詳細信息，例如唯一 ID、作者姓名、簽名日期和資料因素。

### QR 碼簽名選項配置

#### 概述
配置二維碼簽章選項來定義二維碼在文件上的顯示方式，包括大小、對齊方式和填滿。

#### 逐步實施

**定義 QrCodeSignOptionsConfig 類**

```java
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

class QrCodeSignOptionsConfig {
    public static QrCodeSignOptions setupQrCodeSignOptions(DocumentSignatureData documentSignature) {
        QrCodeSignOptions options = new QrCodeSignOptions();
        
        // 將自訂資料物件序列化為二維碼
        options.setData(documentSignature);
        
        // 指定二維碼類型
        options.setEncodeType(QrCodeTypes.QR);
        
        // 配置對齊的填充
        Padding padding = new Padding();
        padding.setRight(10); // 右填充（以像素為單位）
        padding.setBottom(10); // 底部填充（以像素為單位）
        options.setMargin(padding);
        
        // 定義二維碼的大小和位置
        options.setHeight(100);
        options.setWidth(100);
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        return options;
    }
}
```

**解釋：**
- **QrCodeSignOptions**：管理二維碼的顯示方式，包括其大小和位置。
- **填充**：調整文檔內的對齊方式。

### 使用二維碼和自訂加密進行文件簽名

#### 概述
結合二維碼和自訂加密技術，安全地簽署文件。這確保了資料的完整性和保密性。

#### 逐步實施

**使用二維碼簽署文件**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.extensions.encryption.IDataEncryption;
import com.groupdocs.signature.exception.GroupDocsSignatureException;

import java.util.UUID;

class SignDocumentWithQRCode {
    public static void signDocument(String filePath, String outputFilePath) throws Exception {
        try {
            Signature signature = new Signature(filePath);

            // 自訂XOR加密策略
            IDataEncryption encryption = new CustomXOREncryption();

            // 配置自訂文件簽章資料對象
            DocumentSignatureData documentSignature = new DocumentSignatureData();
            documentSignature.setID(UUID.randomUUID().toString());
            documentSignature.setAuthor(System.getenv("USERNAME"));
            documentSignature.setSigned(new Date());
            documentSignature.setDataFactor(new BigDecimal("11.22"));

            // 設定二維碼選項
            QrCodeSignOptions options = QrCodeSignOptionsConfig.setupQrCodeSignOptions(documentSignature);

            // 將二維碼內的資料加密
            options.setDataEncryption(encryption);

            // 簽署並儲存文件
            signature.sign(outputFilePath, options);
        } catch (Exception e) {
            throw new GroupDocsSignatureException(e.getMessage());
        }
    }
}
```

**解釋：**
- **自訂異或加密**：實施自訂加密策略來保護二維碼資料。
- **唯一識別符**：為每個簽名產生一個唯一的識別碼。