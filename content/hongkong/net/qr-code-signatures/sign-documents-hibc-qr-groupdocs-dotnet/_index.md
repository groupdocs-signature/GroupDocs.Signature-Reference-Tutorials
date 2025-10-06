---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 為 PDF 文件簽署 HIBC 二維碼。本指南涵蓋 LIC 和 PAS 二維碼，包括二維碼、Aztec 碼和 DataMatrix 碼。"
"title": "如何使用 GroupDocs.Signature for .NET 簽署帶有 HIBC 二維碼的文件－綜合指南"
"url": "/zh-hant/net/qr-code-signatures/sign-documents-hibc-qr-groupdocs-dotnet/"
"weight": 1
type: docs
---
# 如何使用 GroupDocs.Signature for .NET 簽署帶有 HIBC QR 碼的文檔

## 介紹

在當今快節奏的商業環境中，確保文件的真實性和完整性至關重要。無論您處理的是藥品、保健產品還是物流，擁有安全的文件簽名和追蹤方法可以節省時間並避免錯誤。輸入 **適用於 .NET 的 GroupDocs.Signature**，一個強大的庫，旨在透過將 HIBC QR 碼無縫整合到您的文件中來簡化文件管理流程。

在本教程中，我們將探討如何利用 GroupDocs.Signature for .NET 為具有各種 HIBC QR 碼（LIC（許可證）和 PAS（產品認證系統））的 PDF 文件簽名，包括 QR 碼、Aztec 碼和 DataMatrix。最終，您將對如何在 .NET 應用程式中實現這些解決方案有深入的理解。

**您將學到什麼：**
- 如何為 .NET 設定 GroupDocs.Signature
- 實施 HIBC LIC QR 碼、Aztec 碼和 DataMatrix
- 新增 HIBC PAS QR 碼、Aztec 碼和 DataMatrix
- 實際用例和整合可能性

在開始實現這些功能之前，讓我們先深入了解先決條件。

## 先決條件

在開始編碼之前，請確保您已準備好以下內容：

- **.NET 環境**：請確保您的系統上安裝了 .NET（最好是 .NET Core 或 .NET 5/6+）。
- **適用於 .NET 的 GroupDocs.Signature**：這個庫將成為我們的主要工具。您可以透過 NuGet 安裝它。
- **基本程式設計知識**：建議熟悉 C# 並在 .NET 中處理文件。

### 所需庫

要將 GroupDocs.Signature 用於 .NET，您需要使用以下方法之一新增套件：

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**套件管理器**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 套件管理器 UI**
搜尋“GroupDocs.Signature”並安裝最新版本。

### 許可證獲取

您可以獲得免費試用許可證進行測試。如需長期使用，請考慮購買訂閱或申請臨時許可證：

- **免費試用**： 使用權 [這裡](https://releases.groupdocs.com/signature/net/)
- **臨時執照**：請求於 [此連結](https://purchase.groupdocs.com/temporary-license/)

### 環境設定

設定環境，確保您的專案目標為適當的 .NET 版本並且可以存取 GroupDocs.Signature。在應用程式中按如下所示初始化它：

```csharp
using GroupDocs.Signature;
```

## 為 .NET 設定 GroupDocs.Signature

要開始使用 GroupDocs.Signature for .NET，您需要安裝程式庫並在專案中配置基本設定。

### 安裝

按照上述方法之一將 GroupDocs.Signature 添加到您的專案中。安裝後，請在程式碼檔案中引用它，以確保您的專案已配置為使用它。

### 許可證初始化

獲取許可證後，按如下方式初始化它：

```csharp
SignatureConfig signConfig = new SignatureConfig();
signConfig.LicensePath = "path/to/your/license.lic";
Signature signature = new Signature("Sample.pdf", signConfig);
```

此設定將允許您無限制地存取 GroupDocs.Signature 的所有功能。

## 實施指南

現在，讓我們深入研究如何使用 GroupDocs.Signature for .NET 的 HIBC QR 碼來實現每個功能。

### 使用 HIBC LIC 二維碼簽署文件

#### 概述

使用 HIBC LIC 二維碼對文件進行簽名，可確保許可場景中的合規性和可追溯性。本節將指導您如何在 PDF 文件中建立和嵌入二維碼。

#### 實施步驟

##### 步驟 1：配置來源和輸出路徑

定義來源文件的位置以及簽章輸出的儲存位置：

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICQR.pdf");
```

##### 步驟 2：建立二維碼簽名選項

使用特定文字和設定配置您的二維碼：

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_QR_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICQR)
    {
        Left = 1,
        Top = 1,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // 使用這些選項簽署文件。
    signature.Sign(destinFilePath, hibcLic_QR_Options);
}
```

**解釋**： 
- `QrCodeSignOptions` 設定二維碼的外觀和內容。在這裡，我們指定 HIBC LIC 二維碼類型並將其放置在文件上。
- `ReturnContent` 設定為 true 可讓您檢索簽署文件的渲染影像。

#### 故障排除提示

- 確保文檔路徑指定正確。
- 驗證 GroupDocs.Signature 是否已取得適當許可以實現全部功能。

### 使用 HIBC LIC Aztec 代碼簽署文件

#### 概述

Aztec 碼提供了另一種編碼形式，適用於高密度資訊儲存。本節重點介紹如何使用 GroupDocs.Signature 將 Aztec 碼嵌入到您的文件中。

#### 實施步驟

##### 步驟 1：配置路徑

與上一個功能類似，定義檔路徑：

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICAztec");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICAztec.pdf");
```

##### 步驟 2：設定 Aztec 程式碼選項

使用 GroupDocs.Signature 設定您的 Aztec 代碼：

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_AZ_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICAztec)
    {
        Left = 1,
        Top = 200,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_AZ_Options);
}
```

**解釋**： 
- 這 `QrCodeSignOptions` 這裡再次使用，但採用的是 Aztec 代碼類型。
- 定位（`Top`， `Left`) 和內容檢索設定與二維碼類似。

#### 故障排除提示

- 確認文件路徑準確。
- 確保 GroupDocs.Signature 的版本支援 Aztec 程式碼類型。

### 使用 HIBC LIC DataMatrix 簽署文件

#### 概述

DataMatrix 程式碼提供了另一種強大的資料儲存方法。本節示範如何將 DataMatrix 整合到您的 PDF 文件中。

#### 實施步驟

##### 步驟 1：設定檔案路徑

和以前一樣，確定文件的位置：

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCLICDataMatrix");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCLICDataMatrix.pdf");
```

##### 步驟 2：建立 DataMatrix 標誌選項

配置並套用 DataMatrix 程式碼：

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcLic_DM_Options = new QrCodeSignOptions("A123PROD30917/75#422011907#GP293", QrCodeTypes.HIBCLICDataMatrix)
    {
        Left = 1,
        Top = 400,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    signature.Sign(destinFilePath, hibcLic_DM_Options);
}
```

**解釋**： 
- `QrCodeSignOptions` 用於設定DataMatrix程式碼的外觀和內容。
- 定位（`Top`， `Left`) 和檢索設定遵循與先前的程式碼相同的模式。

#### 故障排除提示

- 確保所有檔案路徑均正確指定。
- 驗證 GroupDocs.Signature 在您的版本中是否支援 DataMatrix 程式碼類型。

### 使用 HIBC PAS 二維碼簽署文件

#### 概述

使用 HIBC PAS 二維碼簽署文件可增強產品追蹤和可追溯性。本節將指導您如何使用 GroupDocs.Signature 將 PAS 二維碼嵌入 PDF 檔案。

#### 實施步驟

##### 步驟 1：配置來源和輸出路徑

定義來源文件的位置以及簽章輸出的儲存位置：

```csharp
string sourceFilePath = Path.Combine("YOUR_DOCUMENT_DIRECTORY", "Sample.pdf");
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignWithHIBCPASQR");
string destinFilePath = Path.Combine(outputPath, "SignedDocumentWithHIBCPASQR.pdf");
```

##### 步驟 2：建立二維碼簽名選項

使用特定文字和設定配置您的 PAS QR 碼：

```csharp
using (Signature signature = new Signature(sourceFilePath))
{
    var hibcPas_QR_Options = new QrCodeSignOptions("PAS123456789012", QrCodeTypes.HIBCPASQR)
    {
        Left = 1,
        Top = 500,
        ReturnContent = true,
        ReturnContentType = FileType.PNG
    };

    // 使用這些選項簽署文件。
    signature.Sign(destinFilePath, hibcPas_QR_Options);
}
```

**解釋**： 
- `QrCodeSignOptions` 配置為 HIBC PAS QR 碼類型並定位在文件上。
- `ReturnContent` 設定為 true 則會擷取簽名文件的渲染影像。

#### 故障排除提示

- 確保所有路徑均正確指定。
- 驗證 GroupDocs.Signature 在您的版本中是否支援 PAS QR Code 類型。

### 結論

請依照本指南，您可以使用 GroupDocs.Signature for .NET 將 HIBC LIC 和 PAS 二維碼有效地整合到 PDF 文件中。此流程可增強各行各業的文件安全性、可追溯性和合規性。如需進一步的自訂和進階功能，請參閱 [GroupDocs 文檔](https://docs。groupdocs.com/signature/net/).