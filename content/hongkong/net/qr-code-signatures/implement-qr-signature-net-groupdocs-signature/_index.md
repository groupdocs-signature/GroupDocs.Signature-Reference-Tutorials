---
"date": "2025-05-07"
"description": "了解如何使用 GroupDocs.Signature 在 .NET 中實作和搜尋二維碼簽章。簡化文件驗證和管理。"
"title": "使用 GroupDocs.Signature 在 .NET 中實作二維碼簽章－綜合指南"
"url": "/zh-hant/net/qr-code-signatures/implement-qr-signature-net-groupdocs-signature/"
"weight": 1
type: docs
---
# 如何使用 GroupDocs.Signature 在 .NET 中實作和搜尋二維碼簽名

## 介紹

想要高效率管理文件中的二維碼簽章？隨著數位簽章的重要性日益提升，確保業務營運中精準的搜尋功能至關重要。本指南將指導您使用 GroupDocs.Signature for .NET 實作二維碼簽章搜尋功能。

**您將學到什麼：**
- 設定和配置 GroupDocs.Signature 庫
- 在文件中搜尋特定二維碼簽名的步驟
- 有效保存和處理已發現簽名的技術

讓我們深入研究如何增強您的文件管理系統！

## 先決條件

開始之前請確保您已具備以下條件：

### 所需的庫和相依性：
- **適用於 .NET 的 GroupDocs.Signature**：一個強大的數位簽名庫。請使用以下方法之一進行安裝。

### 環境設定要求：
- 安裝了.NET Framework或.NET Core的開發環境。
- 對 C# 程式語言有基本的了解。

### 知識前提：
- 熟悉使用 C# 處理文件和目錄
- 了解數位簽章和二維碼結構將會很有幫助。

## 為 .NET 設定 GroupDocs.Signature

安裝 GroupDocs.Signature 庫非常簡單。請使用以下方法之一：

**.NET CLI**
```bash
dotnet add package GroupDocs.Signature
```

**套件管理器**
```powershell
Install-Package GroupDocs.Signature
```

**NuGet 套件管理器 UI：**
- 在 Visual Studio 中開啟您的專案。
- 前往「工具」>「NuGet 套件管理器」>「管理解決方案的 NuGet 套件」。
- 搜尋“GroupDocs.Signature”並安裝最新版本。

### 許可證獲取

要試用 GroupDocs.Signature，您可以先免費試用或申請臨時許可證：

- **免費試用**：下載自 [GroupDocs 發布](https://releases。groupdocs.com/signature/net/).
- **臨時執照**：申請臨時駕照 [GroupDocs 購買](https://purchase。groupdocs.com/temporary-license/).

### 基本初始化

設定庫後，在專案中初始化它：

```csharp
using GroupDocs.Signature;

// 使用文檔路徑初始化簽名對象
Signature signature = new Signature("YOUR_DOCUMENT_DIRECTORY/SAMPLE_SIGNED_MULTI");
```

## 實施指南

讓我們將該功能分解為邏輯步驟。

### 配置二維碼簽名的搜尋選項

首先，配置用於在文件中搜尋二維碼的選項。這些選項允許指定頁面和二維碼圖案：

**初始化QrCodeSearchOptions**

```csharp
using GroupDocs.Signature.Options;

// 配置搜尋選項
QrCodeSearchOptions options = new QrCodeSearchOptions()
{
    AllPages = false, // 僅搜尋特定頁面
    PageNumber = 1,   // 從第 1 頁開始
    PagesSetup = new PagesSetup() { FirstPage = true, LastPage = true }, // 定義要搜尋的頁面
    EncodeType = QrCodeTypes.QR, // 指定二維碼類型
    MatchType = TextMatchType.Contains, // 搜尋包含模式的文本
    Text = "John", // 二維碼中的文字圖案
    ReturnContent = true, // 啟用返回二維碼圖像
    ReturnContentType = FileType.PNG // 返回圖像的格式
};
```

### 執行搜尋

根據配置的選項執行搜尋：

```csharp
// 執行搜尋並檢索簽名
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(options);

Console.WriteLine("Source document contains the following signatures:");
foreach (QrCodeSignature qrSignature in signatures)
{
    Console.WriteLine($"\t #{qrSignature.SignatureId} at {qrSignature.PageNumber}-page, " +
                     $"{qrSignature.EncodeType.TypeName} type, Text = '{qrSignature.Text}', created " +
                     $"{qrSignature.CreatedOn.ToShortDateString()}, modified {qrSignature.ModifiedOn.ToShortDateString()}");
}
```

### 儲存二維碼圖像

找到特徵後，將其圖像儲存到指定目錄：

```csharp
string outputPath = Path.Combine("YOUR_OUTPUT_DIRECTORY", "SearchForQRCodeAdvanced");

if (!Directory.Exists(outputPath))
{
    Directory.CreateDirectory(outputPath);
}

int i = 0;
foreach (QrCodeSignature qrCodeSignature in signatures)
{
    string outputFilePath = Path.Combine(outputPath, $"image{i}{qrCodeSignature.Format.Extension}");

    // 儲存二維碼圖像
    using (FileStream fs = new FileStream(outputFilePath, FileMode.Create))
    {
        fs.Write(qrCodeSignature.Content, 0, qrCodeSignature.Content.Length);
    }
    i++;
}
```

## 實際應用

此功能可應用於各種場景：
1. **文件驗證**：快速驗證合約或協議上的簽名。
2. **庫存管理**：高效率追蹤二維碼庫存物品。
3. **活動票務系統**：使用二維碼驗證活動門票以進行入場控制。
4. **行銷活動**：分析行銷資料中的二維碼參與度和回應率。

## 性能考慮

為確保最佳性能：
- **限制搜尋範圍**： 使用 `AllPages = false` 透過搜尋特定頁面來減少處理時間。
- **優化記憶體使用**：使用以下方式妥善處理物品 `using` 語句來有效地管理記憶體。
- **批次處理**：批量處理文檔，以平衡負載並避免資源耗盡。

## 結論

您已經了解如何使用 GroupDocs.Signature for .NET 實作二維碼簽章搜尋功能，透過提供精確且有效率的搜尋來增強文件管理流程。 

**後續步驟：**
- 探索 GroupDocs.Signature 庫的更多功能。
- 將此功能整合到您現有的系統中。

準備好將這些技能付諸實踐了嗎？今天就開始在你的專案中運用它們吧！

## 常見問題部分

1. **什麼是適用於 .NET 的 GroupDocs.Signature？**
   - 一個全面的 API，允許開發人員使用 .NET 應用程式處理文件中的數位簽章。

2. **我可以搜尋文件所有頁面上的二維碼嗎？**
   - 是的，透過設定 `AllPages = true` 在你的 `QrCodeSearchOptions`。

3. **GroupDocs.Signature 支援哪些檔案類型的二維碼搜尋？**
   - 它支援各種文件格式，包括 PDF 和 Word 文件。

4. **如何處理包含許多簽署的大型文件？**
   - 透過限制頁面來優化大量搜尋或處理文件。

5. **此功能可以整合到現有系統中嗎？**
   - 當然！ GroupDocs.Signature 與其他 .NET 應用程式和服務無縫整合。

## 資源
- [GroupDocs 簽署文檔](https://docs.groupdocs.com/signature/net/)
- [API 參考](https://reference.groupdocs.com/signature/net/)
- [下載最新版本](https://releases.groupdocs.com/signature/net/)
- [購買許可證](https://purchase.groupdocs.com/buy)
- [免費試用版下載](https://releases.groupdocs.com/signature/net/)
- [臨時執照申請](https://purchase.groupdocs.com/temporary-license/)
- [GroupDocs 支援論壇](https://forum.groupdocs.com/c/signature/)