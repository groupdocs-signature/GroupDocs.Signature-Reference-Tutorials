---
"date": "2025-05-08"
"description": "了解如何使用 GroupDocs.Signature for Java 安全地對影像進行簽名，包括二維碼簽名和進階影像保存選項。非常適合商務人士和開發者。"
"title": "使用 GroupDocs.Signature for Java 掌握影像簽章與最佳化"
"url": "/zh-hant/java/image-signatures/groupdocs-signature-java-image-optimization/"
"weight": 1
---

# 使用 GroupDocs.Signature for Java 掌握影像簽章與最佳化

在當今的數位時代，安全地簽署文件至關重要。無論您是負責驗證合約的商業人士，還是保護圖像的個人，強大的簽名功能都至關重要。 **GroupDocs.Signature for Java** 提供強大的功能，可無縫建立二維碼簽名並最佳化影像保存選項。本教學將指導您如何利用這些功能進行有效的文件管理。

### 您將學到什麼：
- 在影像上產生二維碼簽名。
- 配置進階 BMP、GIF、JPEG、PNG 和 TIFF 儲存選項。
- 在您的專案中為 Java 實作 GroupDocs.Signature。
- 這些功能的實際應用。

讓我們確保您已正確設定一切！

## 先決條件

在深入了解實作細節之前，請確保您已：

### 所需的庫和依賴項
要使用 GroupDocs.Signature for Java，請將其庫整合到您的專案中。以下是如何根據您的建置系統將其新增的方法：

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

或者，您可以 [直接下載最新版本](https://releases.groupdocs.com/signature/java/) 如果您的項目設定需要它。

### 環境設定要求
- Java 開發工具包 (JDK) 已安裝並正確配置。
- 用於程式碼開發的 IDE，例如 IntelliJ IDEA 或 Eclipse。

### 知識前提
建議具備 Java 程式設計基礎知識。熟悉 Maven/Gradle 建置工具將有所幫助，但並非必需，因為我們將引導您完成設定過程。

## 為 Java 設定 GroupDocs.Signature

若要開始使用 GroupDocs.Signature，請依照下列步驟操作：

1. **安裝依賴項**：將適當的依賴項添加到您的 `pom.xml` 或者 `build.gradle` 文件如上所示。
2. **許可證獲取**：
   - 獲得 [免費試用](https://releases.groupdocs.com/signature/java/) 探索圖書館的全部功能。
   - 如需延長使用時間，請考慮購買許可證或透過其申請臨時許可證 [購買頁面](https://purchase。groupdocs.com/buy).

### 基本初始化和設定
設定環境後，透過建立以下實例來初始化 GroupDocs.Signature `Signature` 類。操作方法如下：

```java
import com.groupdocs.signature.Signature;

public class SignatureSetup {
    public static void main(String[] args) throws Exception {
        // 使用文檔目錄的檔案路徑進行初始化
        String filePath = "YOUR_DOCUMENT_DIRECTORY/sampleImage.jpg";
        Signature signature = new Signature(filePath);
        
        System.out.println("GroupDocs.Signature initialized successfully!");
    }
}
```

## 實施指南

現在您已經完成了必要的設置，讓我們深入研究如何使用 GroupDocs.Signature for Java 實現特定功能。

### 在影像上建立二維碼簽名

#### 概述
本節將指導您在影像文件上產生二維碼簽名。這對於以非侵入式的方式將元資料或資訊直接嵌入影像尤其有用。

##### 步驟1：初始化簽名對象
首先，創建一個 `Signature` 指向目標文件的物件。
```java
String filePath = "YOUR_DOCUMENT_DIRECTORY/sampleImage.jpg";
Signature signature = new Signature(filePath);
```

##### 步驟 2：設定二維碼簽名選項
配置使用二維碼簽署的選項。您需要指定內容和位置等詳細資訊。

```java
import com.groupdocs.signature.domain.qrcodes.QrCodeTypes;
import com.groupdocs.signature.options.sign.QrCodeSignOptions;

QrCodeSignOptions signOptions = new QrCodeSignOptions("JohnSmith");
signOptions.setEncodeType(QrCodeTypes.QR);
signOptions.setLeft(100);  // 距左邊距的位置
signOptions.setTop(100);   // 距上邊距的位置
```

##### 步驟3：簽署文件
最後，將二維碼簽名套用到您的文件。

```java
signature.sign("output/imageWithQR.jpg", signOptions);
System.out.println("QR Code Signature Applied Successfully!");
```

### 配置進階影像儲存選項

#### BMP儲存選項配置
此配置可讓您自訂圖像以 BMP 格式儲存的方式。請根據需要調整壓縮率、解析度和其他參數。

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.BmpSaveOptions;
import com.groupdocs.signature.domain.enums.BitmapCompression;

BmpSaveOptions bmpSaveOptions = new BmpSaveOptions();
bmpSaveOptions.setAddMissingExtenstion(true);
bmpSaveOptions.setCompression(BitmapCompression.Rgb);
bmpSaveOptions.setHorizontalResolution(7);
bmpSaveOptions.setVerticalResolution(7);
bmpSaveOptions.setBitsPerPixel(16);
bmpSaveOptions.setOverwriteExistingFiles(true);
```

#### GIF 儲存選項配置
將影像儲存為 GIF 時，您可以控制背景色彩和調色板排序等方面。

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.GifSaveOptions;

GifSaveOptions gifSaveOptions = new GifSaveOptions();
gifSaveOptions.setBackgroundColorIndex((byte) 2);
gifSaveOptions.setColorResolution((byte) 7);
gifSaveOptions.setDoPaletteCorrection(true);
gifSaveOptions.setTrailer(true);
gifSaveOptions.setInterlaced(false);
gifSaveOptions.setPaletteSorted(true);
gifSaveOptions.setPixelAspectRatio((byte) 24);
gifSaveOptions.setAddMissingExtenstion(true);
```

#### JPEG 儲存選項配置
使用品質、顏色類型和壓縮模式設定優化您的 JPEG 影像儲存。

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.JpegSaveOptions;
import com.groupdocs.signature.domain.enums.JpegCompressionColorMode;
import com.groupdocs.signature.domain.enums.JpegCompressionMode;
import com.groupdocs.signature.domain.enums.JpegRoundingMode;

JpegSaveOptions jpegSaveOptions = new JpegSaveOptions();
jpegSaveOptions.setAddMissingExtenstion(true);
jpegSaveOptions.setBitsPerChannel((byte) 8);
jpegSaveOptions.setColorType(JpegCompressionColorMode.Rgb);
jpegSaveOptions.setComment("signed jpeg file");
jpegSaveOptions.setCompressionType(JpegCompressionMode.Lossless);
jpegSaveOptions.setQuality(100);
jpegSaveOptions.setSampleRoundingMode(JpegRoundingMode.Extrapolate);
```

#### PNG 儲存選項配置
使用 PNG，您可以定義位元深度和壓縮等級以滿足您的需求。

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.PngSaveOptions;
import com.groupdocs.signature.domain.enums.PngColorType;
import com.groupdocs.signature.domain.enums.PngFilterType;

PngSaveOptions pngSaveOptions = new PngSaveOptions();
pngSaveOptions.setBitDepth((byte) 8);
pngSaveOptions.setColorType(PngColorType.Grayscale);
pngSaveOptions.setCompressionLevel(9);
pngSaveOptions.setFilterType(PngFilterType.Adaptive);
pngSaveOptions.setProgressive(true);
pngSaveOptions.setAddMissingExtenstion(true);
```

#### TIFF 儲存選項配置
對於 TIFF 影像，您可以指定格式和其他相關設定。

```java
import com.groupdocs.signature.options.saveoptions.imagessaveoptions.TiffSaveOptions;
import com.groupdocs.signature.domain.enums.TiffFormat;

TiffSaveOptions tiffSaveOptions = new TiffSaveOptions();
tiffSaveOptions.setExpectedTiffFormat(TiffFormat.TiffNoCompressionBw);
tiffSaveOptions.setAddMissingExtenstion(true);
```

## 實際應用

### 真實用例
1. **合約簽訂**：在合約影像中嵌入二維碼，以便快速驗證。
2. **行銷資料**：使用二維碼將品牌訊息直接添加到宣傳資料上。
3. **影像存檔**：優化影像保存設定以在存檔期間保持品質並減少檔案大小。