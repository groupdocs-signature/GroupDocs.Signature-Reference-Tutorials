---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature for .NET 有效率地簽署、驗證、搜尋、更新和刪除文件中的文字簽章。立即簡化您的數位簽章流程。"
"title": "使用 GroupDocs.Signature for .NET 進行主文檔簽署和驗證"
"url": "/zh-hant/net/digital-signatures/master-document-signing-groupdocs-signature-net/"
"weight": 1
type: docs
---
# 使用 GroupDocs.Signature for .NET 進行主文檔簽署和驗證

## 如何使用 GroupDocs.Signature for .NET 掌握文件簽章與驗證

在當今的數位時代，高效的文件簽名解決方案對於管理合約、協議或任何法律文件至關重要。自動化此流程可以節省時間並減少錯誤。 **適用於 .NET 的 GroupDocs.Signature** 提供強大的解決方案，簡化應用程式中的文字簽章管理。本指南將帶您了解 GroupDocs.Signature for .NET 的功能，包括簽署、驗證、搜尋、更新和刪除文字簽署。

## 您將學到什麼

- 如何使用可自訂的文字簽名簽署文檔
- 有效驗證簽名文件的技術
- 在文件中搜尋現有文字簽名的方法
- 根據需要更新和刪除文字簽名的步驟
- 優化效能和記憶體管理的最佳實踐

讓我們先來了解先決條件。

## 先決條件

在開始之前，請確保您的開發環境已設定必要的工具：

### 所需的庫和依賴項

- **適用於 .NET 的 GroupDocs.Signature**：該庫使您能夠在應用程式中添加簽名功能。
- **.NET Framework 4.6.1 或更高版本** （或 .NET Core 2.x+）

### 環境設定要求

您將需要一個 C# 開發環境（例如 Visual Studio）和網際網路連線來下載必要的軟體套件。

### 知識前提

建議您熟悉基本的 C# 程式設計概念。如果您是 GroupDocs.Signature for .NET 的新手，不用擔心—本指南將引導您完成每個步驟。

## 為 .NET 設定 GroupDocs.Signature

首先，您需要在專案中安裝 GroupDocs.Signature 庫。具體操作如下：

### 透過 .NET CLI 安裝
```bash
dotnet add package GroupDocs.Signature
```

### 套件管理器控制台
```powershell
Install-Package GroupDocs.Signature
```

### NuGet 套件管理器 UI
1. 在 Visual Studio 中開啟您的專案。
2. 導航至 **工具** > **NuGet 套件管理器** > **管理解決方案的 NuGet 套件**。
3. 搜尋“GroupDocs.Signature”並安裝最新版本。

#### 許可證取得步驟
- **免費試用**：從下載開始免費試用 [GroupDocs 免費試用](https://releases。groupdocs.com/signature/net/).
- **臨時執照**：取得臨時許可證以評估完整功能 [臨時執照](https://purchase。groupdocs.com/temporary-license/).
- **購買**：如需繼續使用，請從 [GroupDocs 購買頁面](https://purchase。groupdocs.com/buy).

#### 基本初始化和設定

安裝後，在您的專案中初始化 GroupDocs.Signature，如下所示：

```csharp
using GroupDocs.Signature;

// 使用文件路徑初始化簽章實例。
Signature signature = new Signature("path/to/your/document.pdf");
```

現在您已完成設置，讓我們探索如何利用 GroupDocs.Signature 實現各種功能。

## 實施指南

### 使用文字簽名簽署文檔

此功能可讓您為文件新增文字簽名。讓我們來詳細了解：

#### 概述
您可以使用字體大小、顏色、對齊方式等各種選項自訂文字簽名的外觀和位置。

#### 逐步實施

**步驟 1**：定義檔案路徑和輸出位置。
```csharp
string filePath = "YOUR_DOCUMENT_DIRECTORY"; // 原始文檔的路徑
string outputFilePath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SignedDocument.docx");
```

**第 2 步**：使用建立文字簽名 `TextSignOptions`。
```csharp
using (Signature signature = new Signature(filePath))
{
    TextSignOptions signOptions = new TextSignOptions("John Smith")
    {
        VerticalAlignment = GroupDocs.Signature.Options.VerticalAlignment.Top,
        HorizontalAlignment = GroupDocs.Signature.Options.HorizontalAlignment.Center,
        Width = 100,
        Height = 40,
        Margin = new Padding(20),
        ForeColor = Color.Red,
        Font = new SignatureFont { Size = 12, FamilyName = "Comic Sans MS" }
    };
```

**步驟3**：簽署文件並輸出結果。
```csharp
    SignResult signResult = signature.Sign(outputFilePath, signOptions);
    foreach (BaseSignature temp in signResult.Succeeded)
    {
        Console.WriteLine($"Signed Text Signature: Id:{temp.SignatureId}, Location: {temp.Left}x{temp.Top}. Size: {temp.Width}x{temp.Height}");
    }
}
```

#### 關鍵配置選項
- **垂直對齊和水平對齊**：控制簽名在頁面上出現的位置。
- **字體**：自訂文字簽名的字體大小和樣式。

### 驗證文件中的文字簽名

驗證可確保文件已如預期簽署。具體實現方式如下：

#### 概述
驗證文件中現有的文字簽名以確認其真實性和完整性。

#### 逐步實施

**步驟 1**：指定簽名文檔的文件路徑。
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // 簽署文檔的路徑
```

**第 2 步**：使用以下方式建立驗證選項 `TextVerifyOptions`。
```csharp
using (Signature signature = new Signature(filePath))
{
    TextVerifyOptions verifyOptions = new TextVerifyOptions()
    {
        AllPages = false,
        PageNumber = 1,
        Text = "John Smith",
        MatchType = GroupDocs.Signature.Options.TextMatchType.Exact
    };
```

**步驟3**：驗證文件。
```csharp
    VerificationResult verifyResult = signature.Verify(verifyOptions);
    if (verifyResult.IsValid)
    {
        Console.WriteLine("Document was verified successfully!");
    }
    else
    {
        Console.WriteLine("Document failed verification process.");
    }
}
```

#### 故障排除提示
- 確保 `Text` 屬性與文件中的內容完全相符。
- 檢查 `PageNumber` 對應於包含簽名的正確頁面。

### 搜尋文件中的文字簽名

使用此功能可以有效地在文件中定位文字簽名。

#### 概述
搜尋文件的全部或選定頁面以尋找特定的文字簽名。

#### 逐步實施

**步驟 1**：定義檔案路徑。
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // 簽署文檔的路徑
```

**第 2 步**： 使用 `TextSearchOptions` 進行搜尋。
```csharp
using (Signature signature = new Signature(filePath))
{
    TextSearchOptions searchOptions = new TextSearchOptions()
    {
        AllPages = true,
        MatchType = GroupDocs.Signature.Options.TextMatchType.Exact,
        Text = "John Smith"
    };
```

**步驟3**：執行搜尋。
```csharp
    List<TextSignature> signatures = signature.Search<TextSignature>(searchOptions);
    foreach (TextSignature textSignature in signatures)
    {
        if (textSignature != null)
        {
            Console.WriteLine($"Found Text signature at page {textSignature.PageNumber} with type [{textSignature.SignatureImplementation}] and text '{textSignature.Text}'. Location: {textSignature.Left}-{textSignature.Top}. Size is {textSignature.Width}x{textSignature.Height}.");
        }
    }
}
```

### 更新文件文字簽名

在需要時修改文件中現有的文字簽名。

#### 概述
調整現有文字簽名的屬性，例如大小和位置。

#### 逐步實施

**步驟 1**：指定檔案路徑和簽章ID。
```csharp
string filePath = "YOUR_OUTPUT_DIRECTORY"; // 簽署文檔的路徑
List<string> signatureIds = new List<string>(); // 假設此清單中填入了有效的簽名 ID
```

**第 2 步**： 創造 `TextSignature` 需要更新的對象。
```csharp
using (Signature signature = new Signature(filePath))
{
    foreach (var item in signatureIds)
    {
        TextSignature temp = new TextSignature(item)
        {
            Width = 150,
            Height = 50,
            HorizontalAlignment = GroupDocs.Signature.Options.HorizontalAlignment.Right
        };
```

**步驟3**：更新文檔。
```csharp
        SignResult signResult = signature.UpdateSignatures(temp);
        if (signResult.Succeeded.Count > 0)
        {
            Console.WriteLine($"Updated Text Signature: Id:{temp.SignatureId}");
        }
    }
}
```

#### 關鍵配置選項
- **寬度和高度**：調整簽名的大小。
- **水平對齊**：控制更新後的簽名在頁面上出現的位置。

## 結論

透過本指南，您學習如何使用 GroupDocs.Signature for .NET 來簽署、驗證、搜尋、更新和刪除文件中的文字簽章。這些功能對於在應用程式中自動化數位簽章流程至關重要。如需更多詳細資訊和進階選項，請參閱 [官方文檔](https://docs。groupdocs.com/signature/net/).