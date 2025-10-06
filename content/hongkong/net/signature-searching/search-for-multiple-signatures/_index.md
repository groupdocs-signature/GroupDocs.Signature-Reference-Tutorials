---
"description": "了解如何使用 GroupDocs.Signature for .NET 在文件中搜尋多種簽章類型。本指南包含增強文件安全性的程式碼範例，內容全面。"
"linktitle": "搜尋多個簽名"
"second_title": "GroupDocs.簽署 .NET API"
"title": "在文件中搜尋多種簽名類型"
"url": "/zh-hant/net/signature-searching/search-for-multiple-signatures/"
"weight": 14
type: docs
---
## 介紹

在現代文件管理系統中，在單一文件中搜尋和驗證多種簽章類型的能力日益重要。組織通常使用各種簽章類型（例如數位簽章、文字簽章、條碼、二維碼等）來增強文件安全性並簡化驗證流程。 GroupDocs.Signature for .NET 提供了一個強大的框架，使開發人員能夠在各種文件格式中實現全面的簽章搜尋功能。

本教學將引導您使用 GroupDocs.Signature for .NET 在文件中搜尋多種簽章類型的流程，並提供詳細的解釋和實用的程式碼範例。

## 先決條件

在深入實現多重簽名搜尋功能之前，請確保您符合以下先決條件：

1. 開發環境：Visual Studio 或系統上安裝的任何首選的 .NET 開發環境。
  
2. GroupDocs.Signature for .NET：從下列位置下載並安裝 GroupDocs.Signature for .NET 函式庫 [這裡](https://releases。groupdocs.com/signature/net/).

3. 基本 C# 知識：熟悉 C# 程式語言和 .NET 框架概念。

4. 樣本文件：準備包含各種類型簽署的測試文件，以供測試目的。

## 導入命名空間

首先匯入存取 GroupDocs.Signature 功能所需的命名空間：

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

現在，讓我們將搜尋多種簽名類型的流程分解為清晰、易於管理的步驟：

## 步驟 1：載入文檔

首先，載入包含要搜尋的簽名的文件：

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // 多重簽名搜尋代碼將在此處添加
}
```

## 步驟 2：定義不同簽名類型的搜尋選項

為您想要搜尋的每種簽名類型建立搜尋選項：

```csharp
// 定義文字簽名的搜尋選項
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,  // 在所有頁面上搜尋
    Text = "Signature",  // 可選：要尋找的文本
    MatchType = TextMatchType.Contains  // 匹配條件
};

// 定義數位簽章的搜尋選項
DigitalSearchOptions digitalOptions = new DigitalSearchOptions
{
    AllPages = true
};

// 定義條碼簽名的搜尋選項
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
{
    AllPages = true,
    Text = "123456",  // 可選：要匹配的條碼文本
    MatchType = TextMatchType.Exact  // 匹配條件
};

// 定義二維碼簽名的搜尋選項
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
{
    AllPages = true,
    Text = "John",  // 可選：要匹配的二維碼文本
    MatchType = TextMatchType.Contains  // 匹配條件
};

// 定義元資料簽章的搜尋選項
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```

## 步驟 3：向集合新增選項

將所有搜尋選項新增至集合：

```csharp
// 建立一個清單來保存所有搜尋選項
List<SearchOptions> searchOptions = new List<SearchOptions>
{
    textOptions,
    digitalOptions,
    barcodeOptions,
    qrCodeOptions,
    metadataOptions
};
```

## 步驟 4：執行搜尋並處理結果

使用組合搜尋選項執行搜尋並處理結果：

```csharp
// 使用定義的選項搜尋所有簽名類型
SearchResult result = signature.Search(searchOptions);

// 檢查是否找到簽名
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
    
    // 遍歷找到的簽名
    foreach (var foundSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}, ID: {foundSignature.SignatureId}");
        
        // 處理特定簽名類型
        if (foundSignature is TextSignature textSignature)
        {
            Console.WriteLine($"Text: '{textSignature.Text}'");
        }
        else if (foundSignature is BarcodeSignature barcodeSignature)
        {
            Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
        }
        else if (foundSignature is QrCodeSignature qrCodeSignature)
        {
            Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
        }
        else if (foundSignature is DigitalSignature digitalSignature)
        {
            Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
        }
        else if (foundSignature is MetadataSignature metadataSignature)
        {
            Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
        }
    }
}
else
{
    Console.WriteLine("No signatures were found in the document.");
}
```

## 完整範例

這是一個完整的、可運行的範例，示範如何在文件中搜尋多種簽名類型：

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace MultiSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文件路徑
            string filePath = "sample_multiple_signatures.docx";
            
            // 初始化簽名實例
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // 定義文字簽名的搜尋選項
                    TextSearchOptions textOptions = new TextSearchOptions
                    {
                        AllPages = true,
                        MatchType = TextMatchType.Contains
                    };

                    // 定義數位簽章的搜尋選項
                    DigitalSearchOptions digitalOptions = new DigitalSearchOptions
                    {
                        AllPages = true
                    };

                    // 定義條碼簽名的搜尋選項
                    BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions
                    {
                        AllPages = true
                    };

                    // 定義二維碼簽名的搜尋選項
                    QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions
                    {
                        AllPages = true
                    };

                    // 定義元資料簽章的搜尋選項
                    MetadataSearchOptions metadataOptions = new MetadataSearchOptions();

                    // 建立一個清單來保存所有搜尋選項
                    List<SearchOptions> searchOptions = new List<SearchOptions>
                    {
                        textOptions,
                        digitalOptions,
                        barcodeOptions,
                        qrCodeOptions,
                        metadataOptions
                    };

                    // 搜尋所有簽名類型
                    SearchResult result = signature.Search(searchOptions);

                    // 檢查是否找到簽名
                    if (result.Signatures.Count > 0)
                    {
                        Console.WriteLine($"\nSource document ['{filePath}'] contains {result.Signatures.Count} signature(s):");
                        
                        // 按簽名類型處理結果
                        foreach (var foundSignature in result.Signatures)
                        {
                            Console.WriteLine($"Signature found: Type: {foundSignature.SignatureType}, Page: {foundSignature.PageNumber}");
                            
                            // 處理特定簽名類型
                            switch (foundSignature.SignatureType)
                            {
                                case SignatureType.Text:
                                    var textSignature = foundSignature as TextSignature;
                                    Console.WriteLine($"Text: '{textSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Barcode:
                                    var barcodeSignature = foundSignature as BarcodeSignature;
                                    Console.WriteLine($"Barcode Type: {barcodeSignature.EncodeType.TypeName}, Text: '{barcodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.QrCode:
                                    var qrCodeSignature = foundSignature as QrCodeSignature;
                                    Console.WriteLine($"QR Code Type: {qrCodeSignature.EncodeType.TypeName}, Text: '{qrCodeSignature.Text}'");
                                    break;
                                    
                                case SignatureType.Digital:
                                    var digitalSignature = foundSignature as DigitalSignature;
                                    Console.WriteLine($"Certificate: {digitalSignature.Certificate?.SubjectName}, Valid: {digitalSignature.IsValid}");
                                    break;
                                    
                                case SignatureType.Metadata:
                                    var metadataSignature = foundSignature as MetadataSignature;
                                    Console.WriteLine($"Metadata: Name: {metadataSignature.Name}, Value: {metadataSignature.Value}");
                                    break;
                            }
                            
                            Console.WriteLine(); // 在簽名之間加入換行符
                        }
                    }
                    else
                    {
                        Console.WriteLine("No signatures were found in the document.");
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

## 進階多重簽名搜尋技術

### 過濾搜尋結果

您可以實施進階過濾來縮小搜尋結果：

```csharp
// 按頁碼過濾結果
var signaturesOnFirstPage = result.Signatures.FindAll(s => s.PageNumber == 1);

// 按簽名類型過濾結果
var digitalSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.Digital);
var qrCodeSignatures = result.Signatures.FindAll(s => s.SignatureType == SignatureType.QrCode);

// 過濾包含特定內容的文字簽名
var approvalSignatures = result.Signatures
    .FindAll(s => s is TextSignature && ((TextSignature)s).Text.Contains("Approved"));
```

### 驗證多個簽名

針對不同的簽章類型實作驗證邏輯：

```csharp
bool ValidateAllSignatures(SearchResult result)
{
    bool isDocumentValid = true;
    
    // 檢查文件是否有有效的數位簽名
    bool hasValidDigitalSignature = result.Signatures
        .Any(s => s is DigitalSignature && ((DigitalSignature)s).IsValid);
    
    if (!hasValidDigitalSignature)
    {
        Console.WriteLine("Warning: Document does not contain a valid digital signature");
        isDocumentValid = false;
    }
    
    // 檢查文件是否具有所需的二維碼
    bool hasRequiredQRCode = result.Signatures
        .Any(s => s is QrCodeSignature && ((QrCodeSignature)s).Text.Contains("Auth-Code"));
    
    if (!hasRequiredQRCode)
    {
        Console.WriteLine("Warning: Document does not contain the required authentication QR code");
        isDocumentValid = false;
    }
    
    return isDocumentValid;
}
```

### 使用自訂處理進行搜尋

您可以為搜尋操作定義自訂處理邏輯：

```csharp
// 使用自訂處理建立搜尋選項
TextSearchOptions textOptions = new TextSearchOptions
{
    AllPages = true,
    
    // 使用委託定義自訂處理
    ProcessCompleted = (signature) =>
    {
        // 自訂驗證邏輯 - 僅接受指定頁面上的簽名
        TextSignature textSignature = signature as TextSignature;
        return textSignature != null && (textSignature.PageNumber == 1 || textSignature.PageNumber == 2);
    }
};
```

## 結論

在本指南中，我們探討如何使用 GroupDocs.Signature for .NET 在文件中搜尋多種簽章類型。從設定不同簽名類型的搜尋選項到處理和驗證結果，您現在掌握了在 .NET 應用程式中實現強大簽名搜尋功能的知識。

同時搜尋多種簽章類型的功能可增強文件驗證流程、強化安全措施並簡化文件驗證工作流程。 GroupDocs.Signature 提供了一個強大且靈活的框架，可用於處理不同文件格式的各種簽章類型，使其成為文件處理應用程式的理想選擇。

## 常見問題解答

### 我可以搜尋受密碼保護的文件中的簽名嗎？

是的，GroupDocs.Signature 支援在受密碼保護的文件中搜尋簽名。您可以在初始化時提供密碼 `Signature` 目的：

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // 搜尋簽名
}
```

### 簽名搜尋支援哪些文件格式？

GroupDocs.Signature 支援多種文件格式，包括 PDF、Microsoft Office 文件（Word、Excel、PowerPoint）、OpenOffice 格式、圖像等。

### 我可以將搜尋限制在文件中的特定頁面嗎？

是的，每種搜尋選項類型都有允許您指定要搜尋的頁面的屬性：

```csharp
TextSearchOptions options = new TextSearchOptions
{
    AllPages = false,  // 不要搜尋所有頁面
    PageNumber = 1,    // 僅搜尋第 1 頁
    
    // 或指定多個頁面
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } }
};
```

### 如何優化在大型文件中搜尋時的效能？

對於大型文檔，您可以透過以下方式優化效能：

1. 將搜尋限制在特定頁面或頁面範圍
2. 使用更具體的搜尋條件來減少潛在匹配的數量
3. 在結果顯示中實現分頁
4. 如果不需要同時獲得結果，則一次搜尋一種簽名類型

### 我可以擴展 GroupDocs.Signature 以支援自訂簽章類型嗎？

雖然 GroupDocs.Signature 為常見簽名類型提供了內建支持，但您可以透過以下方式擴展其功能：

1. 建立派生自的自訂搜尋選項類 `SearchOptions`
2. 使用實作自訂處理邏輯 `ProcessCompleted` 代表
3. 開發將多個簽章搜尋與高階業務邏輯結合的包裝類

## 參見

* [API 參考](https://reference.groupdocs.com/signature/net/)
* [GitHub 上的程式碼範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [產品文件](https://docs.groupdocs.com/signature/net/)
* [產品頁面](https://products.groupdocs.com/signature/net/)
* [下載最新版本](https://releases.groupdocs.com/signature/net/)
* [部落格文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [免費支援論壇](https://forum.groupdocs.com/c/signature/13)
* [臨時執照](https://purchase.groupdocs.com/temporary-license/)