---
"description": "透過本全面的逐步指南和程式碼範例，了解如何使用 GroupDocs.Signature for .NET 在文件中有效搜尋二維碼。"
"linktitle": "搜尋二維碼"
"second_title": "GroupDocs.簽署 .NET API"
"title": "在文件中搜尋二維碼簽名"
"url": "/zh-hant/net/signature-searching/search-for-qr-codes/"
"weight": 15
---

## 介紹

在當今的數位文件生態系統中，二維碼簽章已成為嵌入資訊、身份驗證和增強文件安全性的寶貴工具。 GroupDocs.Signature for .NET 為開發人員提供了強大的 API，用於從各種文件格式中搜尋和提取二維碼，從而在 .NET 應用程式中實現高級文件分析和驗證功能。

本綜合教學將引導您完成使用 GroupDocs.Signature for .NET 實作二維碼搜尋功能的流程，提供清晰的解釋、逐步說明和可整合到您自己的應用程式中的實用程式碼範例。

## 先決條件

在深入進行二維碼簽名搜尋之前，請確保您符合以下先決條件：

1. GroupDocs.Signature for .NET SDK：從 [下載頁面](https://releases。groupdocs.com/signature/net/).

2. 開發環境：設定 .NET 開發環境，例如 Visual Studio，並安裝 .NET Framework 或 .NET Core。

3. 基礎知識：熟悉 C# 程式設計和 .NET 開發概念。

4. 樣本文檔：準備包含二維碼的測試文檔，用於驗證和測試。

## 導入命名空間

首先匯入必要的命名空間來存取 GroupDocs.Signature 功能：

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;
```

現在，讓我們將搜尋二維碼的過程分解為清晰、易於遵循的步驟：

## 步驟 1：定義文檔路徑

首先，指定包含要搜尋的二維碼的文件的路徑：

```csharp
string filePath = "sample_multiple_signatures.docx";
```

## 步驟2：初始化簽名對象

建立一個實例 `Signature` 透過傳遞文檔路徑來類：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 二維碼搜尋代碼將會加入此處
}
```

## 步驟3：搜尋二維碼簽名

使用 `Search` 方法使用適當的簽章類型來尋找文件中的二維碼：

```csharp
// 在文件中搜尋二維碼簽名
List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
```

## 步驟4：處理並顯示結果

遍歷找到的二維碼簽名並存取其屬性：

```csharp
// 顯示有關找到的二維碼的信息
Console.WriteLine($"\nSource document contains {signatures.Count} QR code signature(s):");

foreach (var qrCodeSignature in signatures)
{
    Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
    Console.WriteLine($"Content: {qrCodeSignature.Text}");
    Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
    Console.WriteLine();
}
```

## 完整範例

以下是一個全面的工作範例，演示了在文件中搜尋二維碼的完整過程：

```csharp
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
using System;
using System.Collections.Generic;

namespace QrCodeSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文件路徑 - 使用您的文件路徑更新
            string filePath = "sample_multiple_signatures.docx";
            
            // 初始化簽名實例
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // 在文件中搜尋二維碼簽名
                    List<QrCodeSignature> signatures = signature.Search<QrCodeSignature>(SignatureType.QrCode);
                    
                    // 顯示搜尋結果
                    Console.WriteLine($"\nSource document ['{filePath}'] contains {signatures.Count} QR code signature(s):");
                    
                    foreach (var qrCodeSignature in signatures)
                    {
                        Console.WriteLine($"QR Code found at page {qrCodeSignature.PageNumber} with type {qrCodeSignature.EncodeType.TypeName}");
                        Console.WriteLine($"Content: {qrCodeSignature.Text}");
                        Console.WriteLine($"Location: X={qrCodeSignature.Left}, Y={qrCodeSignature.Top}, Width={qrCodeSignature.Width}, Height={qrCodeSignature.Height}");
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

## 高級二維碼搜尋技術

### 使用特定條件搜尋

如需更有針對性的搜索，您可以使用 `QrCodeSearchOptions` 自訂您的搜尋條件：

```csharp
// 建立具有特定條件的二維碼搜尋選項
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    // 僅在特定頁面上搜尋
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // 按二維碼內容過濾
    Text = "Invoice",
    MatchType = TextMatchType.Contains,
    
    // 按特定二維碼類型過濾
    EncodeType = QrCodeTypes.QR,
    
    // 定義要搜尋的特定區域
    Rectangle = new Rectangle(100, 100, 400, 400)
};

// 使用特定選項進行搜尋
List<QrCodeSignature> filteredSignatures = signature.Search<QrCodeSignature>(options);
```

### 處理二維碼數據

您可以根據應用需求對二維碼資料進行自訂處理：

```csharp
foreach (var qrCode in signatures)
{
    // 根據內容擷取並處理二維碼數據
    string qrContent = qrCode.Text;
    
    if (qrContent.StartsWith("URL:"))
    {
        // 處理 URL 數據
        string url = qrContent.Substring(4);
        Console.WriteLine($"Found URL in QR code: {url}");
    }
    else if (qrContent.StartsWith("CONTACT:"))
    {
        // 處理聯絡資訊
        string contact = qrContent.Substring(8);
        Console.WriteLine($"Found contact information in QR code: {contact}");
    }
    else if (qrContent.StartsWith("INVOICE:"))
    {
        // 處理發票訊息
        string invoiceData = qrContent.Substring(8);
        Console.WriteLine($"Found invoice information in QR code: {invoiceData}");
        
        // 解析並驗證發票數據
        if (ValidateInvoiceData(invoiceData))
        {
            Console.WriteLine("Invoice data is valid!");
        }
        else
        {
            Console.WriteLine("Warning: Invalid invoice data detected!");
        }
    }
}

// 驗證方法範例
static bool ValidateInvoiceData(string data)
{
    // 實作驗證邏輯
    return !string.IsNullOrEmpty(data) && data.Contains("ID") && data.Contains("Amount");
}
```

### 實施安全驗證

二維碼通常用於身份驗證。以下是如何實現基本的安全驗證：

```csharp
// 檢查文件是否包含有效的身份驗證二維碼
bool hasValidAuthQrCode = false;

foreach (var qrCode in signatures)
{
    if (qrCode.Text.StartsWith("AUTH:"))
    {
        string authCode = qrCode.Text.Substring(5);
        
        // 驗證身份驗證程式碼（例如，針對資料庫或預定義清單）
        if (VerifyAuthCode(authCode))
        {
            hasValidAuthQrCode = true;
            Console.WriteLine("Document contains valid authentication QR code!");
            break;
        }
    }
}

if (!hasValidAuthQrCode)
{
    Console.WriteLine("Warning: Document does not contain a valid authentication QR code!");
}

// 驗證方法範例
static bool VerifyAuthCode(string code)
{
    // 實作驗證邏輯
    // 這可以是資料庫查找、API 呼叫或與預定義值的比較
    return code == "A7B82C3D" || code == "X9Y8Z7W6";
}
```

### 擷取二維碼影像

您可以從文件中提取二維碼圖像以供進一步處理或顯示：

```csharp
// 將二維碼影像儲存到磁碟
foreach (var qrCode in signatures)
{
    if (qrCode.Content != null)
    {
        // 根據頁碼和位置建立唯一的檔案名
        string outputPath = $"QrCode_P{qrCode.PageNumber}_X{qrCode.Left}_Y{qrCode.Top}.png";
        
        // 儲存影像數據
        File.WriteAllBytes(outputPath, qrCode.Content);
        Console.WriteLine($"Saved QR code image to {outputPath}");
    }
}
```

## 結論

在本指南中，我們探討如何使用 GroupDocs.Signature for .NET 在文件中搜尋二維碼簽章。從基礎搜尋到進階技巧，您現在掌握了在 .NET 應用程式中實現強大二維碼處理的知識。 GroupDocs.Signature API 提供了一個強大且靈活的框架，可用於處理各種文件格式的各種簽章類型（包括二維碼）。

透過利用這些功能，您可以在 .NET 應用程式中增強文件驗證流程、實施身份驗證系統並提取嵌入在二維碼中的有價值的資訊。

## 常見問題解答

### GroupDocs.Signature 支援哪些二維碼格式？

GroupDocs.Signature 支援多種二維碼格式，包括標準二維碼、Micro QR Code 以及其他常見的二維碼標準。具體格式可透過 `EncodeType` 的財產 `QrCodeSignature` 目的。

### 我可以在受密碼保護的文件中搜尋二維碼嗎？

是的，GroupDocs.Signature 支援在受密碼保護的文件中搜尋二維碼，只需在初始化時提供密碼即可。 `Signature` 目的：

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // 搜尋二維碼
}
```

### 如何根據內容過濾二維碼？

您可以使用以下方式根據內容過濾二維碼 `Text` 和 `MatchType` 的屬性 `QrCodeSearchOptions`：

```csharp
QrCodeSearchOptions options = new QrCodeSearchOptions
{
    Text = "Invoice",
    MatchType = TextMatchType.Contains // 其他選項：Exact、StartsWith、EndsWith
};
```

### GroupDocs.Signature 能偵測損壞或部分可見的二維碼嗎？

GroupDocs.Signature 能夠偵測部分可見的二維碼，但嚴重損壞的二維碼可能無法辨識。檢測精度取決於文件中二維碼的品質和可見性。

### 二維碼搜尋支援哪些文檔格式？

GroupDocs.Signature 支援在各種文件格式中進行二維碼搜索，包括 PDF、Microsoft Office 文件（Word、Excel、PowerPoint）、圖像（JPEG、PNG、TIFF）等。

## 參見

* [API 參考](https://reference.groupdocs.com/signature/net/)
* [GitHub 上的程式碼範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [產品文件](https://docs.groupdocs.com/signature/net/)
* [產品頁面](https://products.groupdocs.com/signature/net/)
* [下載最新版本](https://releases.groupdocs.com/signature/net/)
* [部落格文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [免費支援論壇](https://forum.groupdocs.com/c/signature/13)
* [臨時執照](https://purchase.groupdocs.com/temporary-license/)