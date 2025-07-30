---
"description": "透過我們全面的逐步指南和程式碼範例，了解如何使用 GroupDocs.Signature for .NET 有效地搜尋文件中的文字簽章。"
"linktitle": "搜尋文字簽名"
"second_title": "GroupDocs.簽署 .NET API"
"title": "在文件中搜尋文字簽名"
"url": "/zh-hant/net/signature-searching/search-for-text-signatures/"
"weight": 16
---

## 介紹

文字簽名是指示文件作者身份、批准或驗證的常用方法。在數位文件管理中，以程式設計方式搜尋和提取文字簽名的能力對於文件驗證、工作流程自動化和合規性驗證至關重要。 GroupDocs.Signature for .NET 提供了一個全面的解決方案，用於在 .NET 應用程式中實作文字簽章搜尋功能，支援各種文件格式和進階搜尋功能。

本教學將引導您使用 GroupDocs.Signature for .NET 在文件中搜尋文字簽名的過程，提供詳細的解釋、逐步說明和實用的程式碼範例。

## 先決條件

在深入文字簽名搜尋之前，請確保您符合以下先決條件：

1. GroupDocs.Signature for .NET 函式庫：從 [發布頁面](https://releases。groupdocs.com/signature/net/).

2. 開發環境：設定適當的開發環境，例如 Visual Studio 或任何支援 .NET 的相容 IDE。

3. 樣本文檔：準備包含文字簽名的測試文檔，以供驗證和測試。

4. 基本 C# 知識：熟悉 C# 程式語言和 .NET 框架概念。

## 導入命名空間

首先匯入存取 GroupDocs.Signature 功能所需的命名空間：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

現在，讓我們將搜尋文字簽名的過程分解為清晰、易於管理的步驟：

## 步驟 1：載入文檔

首先，定義文檔路徑並初始化 `Signature` 目的：

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);

using (Signature signature = new Signature(filePath))
{
    // 文字簽名搜尋代碼將在此處添加
}
```

## 第 2 步：配置搜尋選項

建立和配置 `TextSearchOptions` 指定如何搜尋文字簽名：

```csharp
// 配置文字搜尋選項
TextSearchOptions options = new TextSearchOptions
{
    // 在所有頁面上搜尋
    AllPages = true,
    
    // 可選：指定要匹配的文本
    // 文字 =“已批准”，
    
    // 可選：指定匹配類型
    // 匹配類型 = 文字匹配類型.包含
};
```

## 步驟3：執行文字簽名搜索

使用配置的選項執行搜尋操作：

```csharp
// 搜尋文字簽名
List<TextSignature> signatures = signature.Search<TextSignature>(options);
```

## 步驟4：處理並顯示結果

遍歷找到的文字簽名並顯示其詳細資訊：

```csharp
// 顯示搜尋結果
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");

foreach (TextSignature textSignature in signatures)
{
    Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
    Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
    Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
    Console.WriteLine();
}
```

## 完整範例

這是一個完整的工作範例，示範如何在文件中搜尋文字簽名：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace TextSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文件路徑 - 使用您的文件路徑更新
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // 初始化簽名實例
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // 配置文字搜尋選項
                    TextSearchOptions options = new TextSearchOptions
                    {
                        // 在所有頁面上搜尋
                        AllPages = true
                    };
                    
                    // 搜尋文字簽名
                    List<TextSignature> signatures = signature.Search<TextSignature>(options);
                    
                    // 顯示搜尋結果
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} text signature(s):");
                    
                    foreach (TextSignature textSignature in signatures)
                    {
                        Console.WriteLine($"Text signature found at page {textSignature.PageNumber} with text '{textSignature.Text}'");
                        Console.WriteLine($"Location: X={textSignature.Left}, Y={textSignature.Top}, Width={textSignature.Width}, Height={textSignature.Height}");
                        Console.WriteLine($"Signature type: {textSignature.SignatureImplementation}");
                        Console.WriteLine();
                    }
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"Error occurred: {ex.Message}");
                }
            }
            
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

## 高級文字簽名搜尋技術

### 使用特定文字條件搜尋

為了更有針對性的搜索，您可以自訂 `TextSearchOptions` 按特定文字內容過濾：

```csharp
// 使用特定文字條件建立搜尋選項
TextSearchOptions options = new TextSearchOptions
{
    // 在所有頁面上搜尋
    AllPages = true,
    
    // 搜尋特定文本
    Text = "Approved",
    
    // 指定符合類型（包含、精確、以...開頭、以...結尾）
    MatchType = TextMatchType.Contains,
    
    // 區分大小寫的搜尋
    MatchCase = true
};
```

### 在特定文件區域中搜尋

您可以將搜尋限制在文件的特定區域：

```csharp
// 為特定文檔區域建立搜尋選項
TextSearchOptions options = new TextSearchOptions
{
    // 僅在特定頁面上搜尋
    AllPages = false,
    PageNumber = 1,
    
    // 或指定多個頁面
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // 定義要搜尋的特定區域
    Rectangle = new Rectangle(100, 100, 400, 200)
};
```

### 進階文字過濾

針對更複雜的搜尋要求實作自訂過濾邏輯：

```csharp
// 使用自訂處理建立搜尋選項
TextSearchOptions options = new TextSearchOptions
{
    AllPages = true,
    
    // 使用委託定義自訂處理
    ProcessCompleted = (TextSignature signature) =>
    {
        // 自訂驗證邏輯
        bool isValid = signature.Text.Length > 5 && 
                      (signature.Text.Contains("Approved") || signature.Text.Contains("Verified"));
        
        return isValid;
    }
};
```

### 搜尋不同的文字樣式

使用字體和樣式屬性來過濾文字簽名：

```csharp
// 建立針對特定文字外觀的搜尋選項
TextSearchOptions options = new TextSearchOptions
{
    // 按字體名稱過濾
    FontName = "Arial",
    
    // 依字體大小範圍過濾
    MinFontSize = 10,
    MaxFontSize = 14,
    
    // 按字體顏色過濾
    ForeColor = System.Drawing.Color.Blue
};
```

### 提取簽署元數據

提取並處理與文字簽名相關的元資料：

```csharp
foreach (TextSignature signature in signatures)
{
    // 存取簽署元數據
    if (signature.Metadata != null && signature.Metadata.Count > 0)
    {
        Console.WriteLine("Signature Metadata:");
        
        foreach (var item in signature.Metadata)
        {
            Console.WriteLine($"  {item.Key}: {item.Value}");
        }
    }
    
    // 檢查簽名的建立和修改日期
    if (signature.CreatedOn.HasValue)
    {
        Console.WriteLine($"Created on: {signature.CreatedOn.Value}");
    }
    
    if (signature.ModifiedOn.HasValue)
    {
        Console.WriteLine($"Modified on: {signature.ModifiedOn.Value}");
    }
}
```

## 結論

在本指南中，我們探討如何使用 GroupDocs.Signature for .NET 在文件中搜尋文字簽章。從基本的搜尋操作到進階技巧，您現在掌握了在 .NET 應用程式中實現強大文字簽名功能的知識。

GroupDocs.Signature 提供了一個強大且靈活的文字簽章處理框架，可讓您建立複雜的文件驗證系統、自動化工作流程解決方案和合規性驗證工具。

## 常見問題解答

### 我可以在受密碼保護的文件中搜尋文字簽名嗎？

是的，GroupDocs.Signature 支援在受密碼保護的文件中搜尋文字簽章。您可以在初始化時提供密碼 `Signature` 目的：

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // 搜尋文字簽名
}
```

### 文字簽章搜尋支援哪些文件格式？

GroupDocs.Signature 支援多種文件格式，包括 PDF、Microsoft Office 文件（Word、Excel、PowerPoint）、OpenOffice 格式、圖像等。

### 我可以搜尋具有特定格式（例如粗體或斜體）的文字簽名嗎？

是的，您可以使用 `FontBold` 和 `FontItalic` 屬性 `TextSearchOptions`：

```csharp
TextSearchOptions options = new TextSearchOptions
{
    FontBold = true,
    FontItalic = true
};
```

### 如何提高大型文件的搜尋效能？

對於大型文檔，您可以透過以下方式優化搜尋效能：

1. 將搜尋限制在特定頁面而不是搜尋整個文檔
2. 使用更具體的搜尋條件來減少匹配數
3. 使用 `Rectangle` 如果你知道簽名通常位於哪裡
4. 在應用程式中實作分頁以批次處理搜尋結果

### 我能否偵測文字簽名是否以電子方式添加或是否為原始文件內容的一部分？

GroupDocs.Signature 可以區分文件中不同類型的文字元素。 `SignatureImplementation` 的財產 `TextSignature` 指示文字是正式簽名還是常規文件內容。然而，最終的判斷可能取決於文本最初是如何添加到文件中的。

## 參見

* [API 參考](https://reference.groupdocs.com/signature/net/)
* [GitHub 上的程式碼範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [產品文件](https://docs.groupdocs.com/signature/net/)
* [產品頁面](https://products.groupdocs.com/signature/net/)
* [下載最新版本](https://releases.groupdocs.com/signature/net/)
* [部落格文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [免費支援論壇](https://forum.groupdocs.com/c/signature/13)
* [臨時執照](https://purchase.groupdocs.com/temporary-license/)