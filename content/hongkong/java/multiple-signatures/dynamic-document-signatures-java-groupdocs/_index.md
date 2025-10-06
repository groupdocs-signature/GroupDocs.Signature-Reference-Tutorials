---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 建立動態文字和條碼圖片簽名，提高電子簽名效率。"
"title": "Java 中的動態文件簽名－掌握 GroupDocs.Signature 的電子簽名"
"url": "/zh-hant/java/multiple-signatures/dynamic-document-signatures-java-groupdocs/"
"weight": 1
type: docs
---
# 使用 GroupDocs 在 Java 中建立動態文件簽名

在當今快節奏的數位世界中，高效地以電子方式簽署文件的需求比以往任何時候都更加重要。無論您是希望簡化合約審批流程的商務人士，還是管理個人文件的個人，電子簽名都能提供快速便捷的服務。本教學將指導您使用 GroupDocs.Signature for Java 建立動態文字和條碼圖像簽章。透過利用伸展模式，您的簽名可以無縫適應整個頁面，從而確保一致性和可讀性。

**您將學到什麼：**
- 如何將 GroupDocs.Signature for Java 整合到您的專案中。
- 建立具有全頁寬度拉伸的文字簽名的步驟。
- 實現跨越頁面高度的條碼圖像簽名的技術。
- 電子簽名在各種商業場景中的實際應用。

在開始編碼之前，讓我們深入了解先決條件。

## 先決條件
在踏上這段旅程之前，請確保您已準備好以下物品：

1. **所需的庫和版本：**
   - 您需要 Java 版本 23.12 或更高版本的 GroupDocs.Signature。

2. **環境設定要求：**
   - 您的系統上安裝了可運行的 Java 開發工具包 (JDK)。
   - 整合開發環境 (IDE)，例如 IntelliJ IDEA、Eclipse 或 NetBeans。

3. **知識前提：**
   - 對 Java 程式設計和 IDE 使用有基本的了解。
   - 熟悉 Maven 或 Gradle 的依賴管理將會很有幫助。

有了這些先決條件，讓我們為您的 Java 專案設定 GroupDocs.Signature。

## 為 Java 設定 GroupDocs.Signature
要開始使用 GroupDocs.Signature for Java，您需要將其新增為依賴項。以下是使用不同建置工具執行此操作的方法：

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
如果您願意，請直接從 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 許可證獲取
在繼續之前，請考慮獲取許可證：
- **免費試用：** 從免費試用開始探索功能。
- **臨時執照：** 如果您需要更多不受限制的時間，請提出請求。
- **購買：** 購買許可證以供長期使用。

透過建立以下實例來初始化 GroupDocs.Signature `Signature` 類。這將設定您的環境，為實施數位簽章做好準備。

## 實施指南
現在我們的設定已經完成，讓我們探索如何使用 GroupDocs.Signature 實作每個簽章功能。

### 拉伸模式的文字簽名
此功能可讓您新增橫跨整個頁面寬度的文字簽名，確保可見度和一致性。

#### 概述
文字簽名提供了一種簡單的數位簽名文件方法。透過將拉伸模式設定為 `PageWidth`，它可以動態適應不同的文件大小。

#### 實施步驟
**1.導入所需的類別**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.StretchMode;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.TextSignOptions;
```

**2. 初始化簽名實例**
創建一個 `Signature` 對象，指定文檔的路徑。

```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sample.docx";
Signature signature = new Signature(filePath);
```

**3. 配置文字簽章選項**
使用所需的配置（例如對齊方式和邊距）設定文字符號選項。

```java
TextSignOptions textOptions = new TextSignOptions("This is a test message");
textOptions.setAllPages(true);  // 應用於所有頁面
textOptions.setVerticalAlignment(VerticalAlignment.Top);
textOptions.setMargin(new Padding(50));
textOptions.setStretch(StretchMode.PageWidth);
```

**4. 簽署並儲存文件**
最後，使用配置的選項對文件進行簽名並儲存。

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/TextSignatureWithStretch_signed.docx";
signature.sign(outputFilePath, textOptions);
```

### 拉伸模式的條碼簽名
此功能添加了跨越整個頁面高度的條碼簽名，以提高可視性。

#### 概述
條碼簽名對於驗證真偽和追蹤文件至關重要。將拉伸模式設定為 `PageHeight`，它們在不同的文件尺寸上都保持清晰度。

#### 實施步驟
**1.導入所需的類別**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.Padding;
import com.groupdocs.signature.domain.enums.StretchMode;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.options.sign.BarcodeSignOptions;
import com.groupdocs.signature.domain.barcodes.BarcodeTypes;
```

**2. 初始化簽名實例**

```java
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

**3.配置條碼簽名選項**
調整條碼設置，包括類型和對齊。

```java
BarcodeSignOptions barcodeOptions = new BarcodeSignOptions("123456");
barcodeOptions.setAllPages(true);
barcodeOptions.setEncodeType(BarcodeTypes.Code128);
barcodeOptions.setVerticalAlignment(VerticalAlignment.Bottom);
barcodeOptions.setMargin(new Padding(50));
barcodeOptions.setStretch(StretchMode.PageWidth);
```

**4. 簽署並儲存文件**

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/BarcodeSignatureWithStretch_signed.docx";
signature.sign(outputFilePath, barcodeOptions);
```

### 具有拉伸模式的影像簽名
此功能引入了垂直拉伸以覆蓋頁面高度的圖像簽名。

#### 概述
影像簽名增添了個性化的觸感。透過將拉伸模式設定為 `PageHeight`，它們可以有效地適應不同的文件大小。

#### 實施步驟
**1.導入所需的類別**

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.domain.enums.StretchMode;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.options.sign.ImageSignOptions;
```

**2. 初始化簽名實例**

```java
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/sample.docx");
```

**3. 配置影像簽名選項**
定義影像設置，包括對齊和拉伸模式。

```java
ImageSignOptions imageOptions = new ImageSignOptions();
imageOptions.setAllPages(true);
imageOptions.setStretch(StretchMode.PageHeight);
imageOptions.setHorizontalAlignment(HorizontalAlignment.Right);
imageOptions.setImageFilePath("YOUR_DOCUMENT_DIRECTORY/image.png");
```

**4. 簽署並儲存文件**

```java
String outputFilePath = "YOUR_OUTPUT_DIRECTORY/ImageSignatureWithStretch_signed.docx";
signature.sign(outputFilePath, imageOptions);
```

## 實際應用
電子簽名徹底改變了各行各業的文件管理。以下是一些實際應用：

1. **合約管理：** 簡化法律和商業環境中的合約審批。
2. **教育機構：** 方便成績單、證書等學生文件的簽署。
3. **衛生保健：** 使用簽署的同意書管理病患記錄。
4. **房地產：** 透過數位簽署協議來加快財產交易。

整合的可能性非常大，允許 CRM 或 ERP 等系統無縫地整合數位簽名，以增強工作流程自動化。

## 性能考慮
使用 GroupDocs.Signature 時，請考慮以下優化效能的提示：
- **記憶體管理：** 有效管理文件處理過程中的記憶體使用情況，以確保順利運作。