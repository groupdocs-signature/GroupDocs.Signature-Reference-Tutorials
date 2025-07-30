---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 為 DICOM 映像簽署二維碼。本指南涵蓋醫學影像中二維碼簽名的設定、實作和驗證。"
"title": "如何使用 GroupDocs.Signature for .NET 為 DICOM 影像簽署（二維碼）－綜合指南"
"url": "/zh-hant/net/qr-code-signatures/groupdocs-signature-net-dicom-images-qr-codes/"
"weight": 1
---

# 如何使用 GroupDocs.Signature for .NET 對帶有二維碼的 DICOM 影像進行簽署：綜合指南

您是否正在尋找一種安全的方法來驗證您的 DICOM 檔案？本詳細指南將向您展示如何使用 GroupDocs.Signature for .NET 將二維碼簽章整合到 DICOM 影像中。本教學涵蓋從設定到實施的整個流程，非常適合醫療專業人員、開發人員以及任何使用數位醫療文件的人員。

## 您將學到什麼：
- 使用 GroupDocs.Signature for .NET 設定您的開發環境。
- 使用二維碼簽署 DICOM 影像的逐步說明。
- 驗證和搜尋 DICOM 檔案中的二維碼簽章的方法。
- 用於產生簽名文件預覽以供審查的技術。
- 優化效能和有效管理資源的最佳實務。

讓我們從先決條件開始吧！

## 先決條件

若要使用 GroupDocs.Signature for .NET，請確保您的環境已準備就緒。您需要：

### 所需的庫和版本
- **適用於 .NET 的 GroupDocs.Signature**：確保與您的 .NET 框架相容。

### 環境設定要求
- Windows 或 Linux 上的開發環境。
- 安裝了 Visual Studio 或其他與 .NET 相容的 IDE。

### 知識前提
- 對 C# 程式設計有基本的了解。
- 熟悉 .NET 應用程式中的檔案 I/O。

## 為 .NET 設定 GroupDocs.Signature

使用您喜歡的方法安裝 GroupDocs.Signature 庫：

**使用 .NET CLI：**
```bash
dotnet add package GroupDocs.Signature
```

**套件管理器：**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 套件管理器 UI：**
- 搜尋“GroupDocs.Signature”並安裝最新版本。

### 許可證獲取

先免費試用，探索各項功能。如需長期使用，請考慮從 [群組文檔](https://purchase。groupdocs.com/buy).

安裝完成後，初始化函式庫：

```csharp
using GroupDocs.Signature;
// 使用您的 DICOM 檔案路徑初始化簽名物件。
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample.dicom");
```

## 實施指南

### 使用二維碼簽署 DICOM 影像

#### 概述
新增二維碼簽名，確保醫療文件的真實性和可追溯性。

**步驟1：初始化簽名對象**

```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY\\sample.dicom";
using (Signature signature = new Signature(filePath))
{
    // 繼續簽名操作...
}
```

**步驟 2：建立二維碼簽名選項**

配置文字、大小和對齊等屬性。

```csharp
QrCodeSignOptions options = new QrCodeSignOptions("Patient #36363393. R: No-Issues")
{
    AllPages = true,
    Width = 100,
    Height = 100,
    VerticalAlignment = VerticalAlignment.Bottom,
    HorizontalAlignment = HorizontalAlignment.Right,
    Margin = new Padding() { Right = 5, Left = 5 }
};
```

**步驟 3：新增 XMP 元數據**

使用附加元資料來增強文件。

```csharp
DicomSaveOptions dicomSaveOptions = new DicomSaveOptions()
{
    XmpEntries = new List<DicomXmpEntry>() { new DicomXmpEntry(DicomXmpType.PatientName, "Patient #4") }
};
```

**步驟4：簽署文件**

執行簽名並儲存。

```csharp
SignResult signResult = signature.Sign("YOUR_OUTPUT_DIRECTORY\\SignedDicom", options, dicomSaveOptions);
```

### 取得文件資訊

從簽署的 DICOM 檔案中檢索元資料以確保資料完整性。

**概述：**
存取文件資訊和 XMP 元資料簽章進行驗證。

**步驟 1：檢索文件資訊**

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    IDocumentInfo signedDocumentInfo = signature.GetDocumentInfo();
}
```

**步驟 2：迭代並列印 XMP 數據**

顯示元數據詳細資訊。

```csharp
foreach (var item in signedDocumentInfo.MetadataSignatures)
{
    Console.WriteLine(item.ToString());
}
```

### 驗證 DICOM 簽名

驗證 DICOM 影像中的二維碼簽名的真實性。

**概述：**
確保簽名正確且真實。

**步驟 1：建立二維碼驗證選項**

設定與二維碼中的特定文字相符的選項。

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true,
    Text = "Patient #36363393",
    MatchType = TextMatchType.Contains
};
```

**第 2 步：驗證簽名**

檢查簽名是否符合標準。

```csharp
VerificationResult result = signature.Verify(options);

if (result.IsValid)
{
    Console.WriteLine($"DICOM {filePath} has {result.Succeeded.Count} successfully verified signatures!");
}
```

### 在 DICOM 中搜尋簽名

在簽署的 DICOM 影像中找到二維碼簽名。

**概述：**
有效地查找所有二維碼簽名以管理文件真實性。

**步驟 1：搜尋二維碼簽名**

```csharp
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

**步驟 2：迭代並列印簽名詳細信息**

檢查每個找到的簽名的詳細資訊。

```csharp
foreach (var QrCodeSignature in signatures)
{
    Console.WriteLine($"QRCode signature found at page {QrCodeSignature.PageNumber} with type {QrCodeSignature.EncodeType.TypeName} and text {QrCodeSignature.Text}");
}
```

### 產生簽名 DICOM 的預覽

建立視覺預覽以供驗證。

**概述：**
產生影像預覽來驗證內容，無需專門的軟體。

**步驟 1：定義流方法**

設定預覽產生期間文件流程管理的方法。

```csharp
Stream CreatePageStream(PreviewPageData pageData)
{
    string imageFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignDicomImageAdvanced", $"preview-{pageData.PageNumber}.jpg");
    var folder = Path.GetDirectoryName(imageFilePath);
    if (!Directory.Exists(folder))
    {
        Directory.CreateDirectory(folder);
    }
    return new FileStream(imageFilePath, FileMode.Create);
}

void ReleasePageStream(PreviewPageData pageData, Stream pageStream)
{
    pageStream.Dispose();
}
```

**第 2 步：產生預覽**

執行預覽生成過程。

```csharp
using (Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY\\sample_signed.dicom"))
{
    PreviewOptions previewOption = new PreviewOptions(CreatePageStream, ReleasePageStream)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
    };

    signature.GeneratePreview(previewOption);
}
```

## 實際應用

1. **醫療記錄管理**：使用二維碼簽名驗證病患記錄是否符合。
2. **醫療保健系統中的審計跟踪**：追蹤文件變更並使用二維碼驗證真實性。
3. **安全資料共享**：透過嵌入數位簽名確保醫學影像的安全共享。
4. **合規性驗證**：定期驗證 DICOM 文件的完整性以滿足法律要求。
5. **與 EHR 系統集成**：將簽署的 DICOM 檔案無縫整合到電子健康記錄 (EHR) 系統中，以簡化操作。