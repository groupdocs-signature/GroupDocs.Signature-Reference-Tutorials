---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 提取詳細的文件信息，包括簽名、元資料等。本指南涵蓋設定、實施和最佳實務。"
"title": "掌握 GroupDocs.Signature for .NET&#58; 高效提取和顯示文件信息"
"url": "/zh-hant/net/preview-info/groupdocs-signature-net-document-info-extraction/"
"weight": 1
---

# 掌握 .NET 的 GroupDocs.Signature：高效提取和顯示文件信息

## 介紹

您是否希望有效率地從應用程式中的文件中提取全面的詳細資訊？無論是管理合約、協議還是多頁 PDF，強大的解決方案都至關重要。 **適用於 .NET 的 GroupDocs.Signature** 提供強大的功能，旨在透過檢索和顯示表單欄位、簽章、元資料等元素來簡化文件分析。本教學將指導您如何利用這些功能來增強應用程式的功能。

**您將學到什麼：**
- 如何使用 GroupDocs.Signature for .NET 擷取詳細文件信息
- 顯示各種簽名類型和表單欄位詳細信息
- 提取元資料和頁面特定屬性

在深入實施之前，讓我們先回顧一下先決條件。

## 先決條件

在利用 GroupDocs.Signature for .NET 之前，請確保您的環境已正確設定。本教學假設您熟悉 C# 並具備文件處理概念的基礎知識。

### 所需的庫和依賴項
- **適用於 .NET 的 GroupDocs.Signature**：我們將使用的主要庫。
- **.NET Framework 或 .NET Core**：取決於您的項目設定。

### 環境設定
確保您已準備好 Visual Studio 或其他支援 .NET 專案的合適 IDE 的開發環境。

### 知識前提
- 對 C# 程式設計有基本的了解。
- 熟悉文件類型（PDF、Word、Excel）及其屬性。

## 為 .NET 設定 GroupDocs.Signature

要使用 GroupDocs.Signature for .NET，您需要安裝該程式庫。以下是幾種方法：

### 安裝說明

**使用 .NET CLI：**
```bash
dotnet add package GroupDocs.Signature
```

**使用套件管理器控制台：**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 套件管理器 UI：**
在 NuGet 套件管理員中搜尋“GroupDocs.Signature”並安裝最新版本。

### 許可證獲取
若要充分利用 GroupDocs.Signature，請考慮取得許可證：
- **免費試用**：從免費試用開始探索功能。
- **臨時執照**：取得臨時許可證以進行延長測試。
- **購買**：購買用於生產用途的完整許可證。

安裝並取得許可後，透過設定 GroupDocs.Signature 環境來初始化您的項目，如下所示：

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;

public class GetDocumentInfoFeature
{
    public static void Run()
    {
        // 定義要分析的文件的文件路徑
        string filePath = "YOUR_DOCUMENT_DIRECTORY\Sample_Signed_Multi_Document.pdf";  // 替換為您的實際文件路徑
        
        SignatureSettings signatureSettings = new SignatureSettings
        {
            IncludeStandardMetadataSignatures = true
        };

        using (Signature signature = new Signature(filePath, signatureSettings))
        {
            IDocumentInfo documentInfo = signature.GetDocumentInfo();
            // 進一步的操作將在這裡進行...
        }
    }
}
```

## 實施指南

設定完成後，讓我們來探索如何實作 GroupDocs.Signature for .NET 的各種功能。

### 檢索並顯示基本文件屬性

**概述**：提取檔案格式、大小和頁數等基本屬性。

#### 逐步實施：
1. **初始化簽名對象**：創建 `Signature` 與您的文件路徑相關的類別。
2. **GetDocumentInfo 方法**：使用 `GetDocumentInfo()` 方法來檢索有關文件的詳細資訊。
3. **顯示文件屬性**：使用以下方式輸出格式、副檔名和大小等基本屬性 `Console.WriteLine` 用於調試或記錄目的。

```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
```

### 顯示有關每個文件頁面的信息

**概述**：透過檢索和顯示有關文件中每一頁的資訊來深入了解。

#### 逐步實施：
1. **遍歷頁面**：循環遍歷 `documentInfo.Pages` 訪問單個頁面的詳細信息，例如寬度和高度。

```csharp
foreach (PageInfo pageInfo in documentInfo.Pages)
{
    Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```

### 顯示表單欄位簽章訊息

**概述**：提取並顯示與文件內的表單欄位相關的資訊。

#### 逐步實施：
1. **訪問表單字段**： 使用 `documentInfo.FormFields` 檢索文件中存在的所有表單欄位簽章。
2. **顯示每個表單欄位的詳細信息**：遍歷每個表單欄位並輸出其類型、名稱和值。

```csharp
Console.WriteLine($"Document Form Fields information: count = {documentInfo.FormFields.Count}");
foreach (FormFieldSignature formField in documentInfo.FormFields)
{
    Console.WriteLine($" - type #{formField.Type}: Name: {formField.Name} Value: {formField.Value}");
}
```

### 顯示各種簽名訊息

**概述**：檢索和顯示文字、圖像、數字、條碼、二維碼、表單欄位和元資料簽名的資訊。

#### 實施步驟：
- **文字簽名**： 使用權 `documentInfo.TextSignatures` 取得每個文字簽名的詳細信息，包括其 ID、位置、大小和建立日期。

```csharp
Console.WriteLine($"Document Text signatures: {documentInfo.TextSignatures.Count}");
foreach (TextSignature textSignature in documentInfo.TextSignatures)
{
    Console.WriteLine($" - #{textSignature.SignatureId}: Text: {textSignature.Text} Location: {textSignature.Left}x{textSignature.Top}. Size: {textSignature.Width}x{textSignature.Height}. CreatedOn/ModifiedOn: {textSignature.CreatedOn.ToShortDateString()} / {textSignature.ModifiedOn.ToShortDateString()}");
}
```

- **影像簽名**：與文字簽名類似，使用 `documentInfo.ImageSignatures` 有關圖像簽名的大小和格式等詳細資訊。

```csharp
Console.WriteLine($"Document Image signatures: {documentInfo.ImageSignatures.Count}");
foreach (ImageSignature imageSignature in documentInfo.ImageSignatures)
{
    Console.WriteLine($" - #{imageSignature.SignatureId}: Size: {imageSignature.Size} bytes, Format: {imageSignature.Format}. CreatedOn/ModifiedOn: {imageSignature.CreatedOn.ToShortDateString()} / {imageSignature.ModifiedOn.ToShortDateString()}");
}
```

- **數位簽名**：對於數位簽名，利用 `documentInfo.DigitalSignatures` 提取簽名 ID 和時間戳記。

```csharp
Console.WriteLine($"Document Digital signatures: {documentInfo.DigitalSignatures.Count}");
foreach (DigitalSignature digitalSignature in documentInfo.DigitalSignatures)
{
    Console.WriteLine($" - #{digitalSignature.SignatureId}. CreatedOn/ModifiedOn: {digitalSignature.CreatedOn.ToShortDateString()} / {digitalSignature.ModifiedOn.ToShortDateString()}");
}
```

- **條碼和二維碼簽名**： 使用 `documentInfo.BarcodeSignatures` 和 `documentInfo.QrCodeSignatures` 分別收集條碼和二維碼的詳細資料。

```csharp
Console.WriteLine($"Document Barcode signatures: {documentInfo.BarcodeSignatures.Count}");
foreach (BarcodeSignature barcodeSignature in documentInfo.BarcodeSignatures)
{
    Console.WriteLine($" - #{barcodeSignature.SignatureId}: Type: {barcodeSignature.EncodeType?.TypeName}. Text: {barcodeSignature.Text}");
}

Console.WriteLine($"Document QR Code signatures: {documentInfo.QrCodeSignatures.Count}");
foreach (QrCodeSignature qrCodeSignature in documentInfo.QrCodeSignatures)
{
    Console.WriteLine($" - #{qrCodeSignature.SignatureId}: Type: {qrCodeSignature.EncodeType?.TypeName}. Text: {qrCodeSignature.Text}");
}
```

### 結論

透過本教學課程，您學習如何利用 GroupDocs.Signature for .NET 有效率地擷取和顯示全面的文件資訊。這項技能將增強您的應用程式精準、輕鬆管理文件的能力。

**後續步驟：**
- 探索 GroupDocs.Signature 的其他功能。
- 在您的應用程式中實施簽名驗證。
- 將此功能整合到更大的工作流程中，以實現自動化文件處理。