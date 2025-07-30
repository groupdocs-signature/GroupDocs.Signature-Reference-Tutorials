---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature 在 Java 中實作自訂影像簽章。本指南涵蓋定位、對齊、外觀調整和邊框自訂。"
"title": "如何使用 GroupDocs.Signature 在 Java 中自訂映像簽名"
"url": "/zh-hant/java/image-signatures/customize-image-signatures-java-groupdocs-signature/"
"weight": 1
---

# 如何使用 GroupDocs.Signature for Java 實作自訂映像簽名

## 介紹

在當今的數位世界中，電子文檔簽章對於許多業務流程至關重要。確保您的簽名準確出現在文件上的所需位置，同時又保持專業的外觀，可能頗具挑戰性。 **GroupDocs.Signature for Java** 提供強大的自訂選項，將電子簽名無縫整合到應用程式中。

本教學將引導您設定適用於 Java 的 GroupDocs.Signature，並探索關鍵功能，例如定位、對齊以及使用各種配置（例如大小、對齊方式、外觀調整和邊框自訂）設定影像簽名的樣式。讀完本文後，您將了解如何：
- 設定簽名位置和大小
- 簽名與頁邊距對齊
- 調整影像外觀設定
- 自訂影像邊框

讓我們開始吧！

## 先決條件

在開始之前，請確保您已準備好以下先決條件：
1. **Java 開發工具包 (JDK)**：確保您的系統上安裝了 JDK 8 或更高版本。
2. **整合開發環境 (IDE)**：使用 IntelliJ IDEA 或 Eclipse 等 IDE 進行 Java 開發。
3. **GroupDocs.Signature 庫**：在您的專案中新增 GroupDocs.Signature 作為相依性。

### 所需的庫和依賴項

若要包含 GroupDocs.Signature，您可以使用 Maven 或 Gradle：

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

或者，直接從 [GroupDocs.Signature Java 版本](https://releases。groupdocs.com/signature/java/).

### 環境設定

確保您的 IDE 配置為包含外部函式庫，並設定一個包含輸入文件、簽名影像和輸出簽章文件目錄的項目。

### 知識前提

- 對 Java 程式設計有基本的了解。
- 熟悉處理 Java 應用程式中的檔案路徑。

## 為 Java 設定 GroupDocs.Signature

若要開始使用 GroupDocs.Signature，請依照下列設定步驟操作：
1. **新增依賴項**：使用提供的 Maven 或 Gradle 配置來包含該庫。
2. **許可證獲取**：首先從下載免費試用版 [群組文檔](https://releases.groupdocs.com/signature/java/) 並考慮在需要時購買許可證。

### 基本初始化

以下是在 Java 應用程式中初始化 GroupDocs.Signature 的方法：

```java
import com.groupdocs.signature.Signature;

public class Main {
    public static void main(String[] args) throws Exception {
        String filePath = "path/to/your/document.docx";
        Signature signature = new Signature(filePath);
        
        // 此處提供其他設定和使用方法
    }
}
```

## 實施指南

讓我們逐步了解自訂圖像簽名的各種功能的實現。

### 設定簽名位置和大小

**概述**：此功能可讓您指定簽名在文件上顯示的位置及其尺寸，確保跨文件的一致性。

#### 逐步實施

1. **初始化簽名對象**：創建 `Signature` 類與您的文件路徑。
2. **配置 ImageSignOptions**：設定影像簽名的選項，包括大小和位置。

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.ImageSignOptions;

public class SignWithImagePosition {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/document.docx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/signature.png";
        String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignaturePosition.docx";

        Signature signature = new Signature(filePath);
        ImageSignOptions options = new ImageSignOptions(imagePath);

        // 設定文件上簽署的位置
        options.setLeft(100);  // 座標（以像素為單位）
        options.setTop(100);   // Y 座標（以像素為單位）

        // 設定簽名矩形的大小
        options.setWidth(100);  // 寬度（以像素為單位）
        options.setHeight(30);  // 高度（以像素為單位）
        
        // 簽署並儲存文件
        signature.sign(outputFilePath, options);
    }
}
```

### 設定簽名對齊方式和邊距

**概述**：調整對齊方式可確保文件不同部分的位置保持一致。邊距有助於避免剪下或與其他內容重疊。

#### 逐步實施

1. **定義垂直和水平對齊**：使用枚舉值進行所需的對齊。
2. **使用填滿配置邊距**：指定邊距以達到精確定位。

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.ImageSignOptions;
import com.groupdocs.signature.domain.enums.HorizontalAlignment;
import com.groupdocs.signature.domain.enums.VerticalAlignment;
import com.groupdocs.signature.domain.Padding;

public class SignWithImageAlignment {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/document.docx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/signature.png";
        String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignatureAlignment.docx";

        Signature signature = new Signature(filePath);
        ImageSignOptions options = new ImageSignOptions(imagePath);

        // 設定簽名的垂直對齊方式
        options.setVerticalAlignment(VerticalAlignment.Bottom);
        
        // 設定簽名的水平對齊方式
        options.setHorizontalAlignment(HorizontalAlignment.Right);
        
        // 配置邊距填充以定位簽名
        Padding padding = new Padding();
        padding.setBottom(20);  // 下邊距（以像素為單位）
        padding.setRight(20);   // 右邊距（以像素為單位）
        options.setMargin(padding);

        // 簽署並儲存文件
        signature.sign(outputFilePath, options);
    }
}
```

### 透過灰階和亮度調整設定影像外觀

**概述**：自訂影像外觀可以增強視覺吸引力。選項包括套用灰度或調整亮度。

#### 逐步實施

1. **配置影像外觀設定**： 使用 `ImageAppearance` 調整影像在文件上的顯示效果。

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.ImageSignOptions;
import com.groupdocs.signature.domain.appearances.ImageAppearance;

public class SignWithImageAppearance {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/document.docx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/signature.png";
        String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignatureAppearance.docx";

        Signature signature = new Signature(filePath);
        ImageSignOptions options = new ImageSignOptions(imagePath);

        // 建立和配置圖像外觀設置
        ImageAppearance imageAppearance = new ImageAppearance();
        
        // 對影像應用灰階效果
        imageAppearance.setGrayscale(true);
        
        // 調整影像的亮度等級
        imageAppearance.setBrightness(0.9f);  // 亮度等級（範圍：0.0 - 1.0）
        
        options.setAppearance(imageAppearance);

        // 簽署並儲存文件
        signature.sign(outputFilePath, options);
    }
}
```

### 設定圖像邊框的樣式和透明度

**概述**：自訂邊框可以增強簽章的專業性。

#### 逐步實施

1. **配置邊框選項**： 使用 `Border` 設定來定義樣式和透明度。

```java
import com.groupdocs.signature.Signature;
import com.groupdocs.signature.options.sign.ImageSignOptions;
import com.groupdocs.signature.domain.Border;

public class SignWithImageBorder {
    public static void run() throws Exception {
        String filePath = "YOUR_DOCUMENT_DIRECTORY/document.docx";
        String imagePath = "YOUR_DOCUMENT_DIRECTORY/signature.png";
        String outputFilePath = "YOUR_OUTPUT_DIRECTORY/SignatureBorder.docx";

        Signature signature = new Signature(filePath);
        ImageSignOptions options = new ImageSignOptions(imagePath);

        // 建立並配置影像的邊框設置
        Border border = new Border();
        border.setColor(java.awt.Color.BLACK);  // 設定邊框顏色
        border.setWidth(2);                    // 設定邊框寬度（以像素為單位）
        border.setDashStyle(com.groupdocs.signature.domain.enums.DashStyle.DashDot);
        
        options.setBorder(border);

        // 簽署並儲存文件
        signature.sign(outputFilePath, options);
    }
}
```