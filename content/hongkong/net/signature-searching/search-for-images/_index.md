---
"description": "透過逐步範例和全面的實施指導，了解如何使用 GroupDocs.Signature for .NET 在文件中有效搜尋影像簽章。"
"linktitle": "搜尋圖片"
"second_title": "GroupDocs.簽署 .NET API"
"title": "在文件中搜尋圖像簽名"
"url": "/zh-hant/net/signature-searching/search-for-images/"
"weight": 13
type: docs
---
## 介紹

在當今的數位文件生態系統中，影像簽名是品牌推廣、授權和文件驗證的強大視覺標記。 GroupDocs.Signature for .NET 為開發人員提供了一個全面的框架，使他們能夠無縫地搜尋、識別和處理各種格式文件中的圖像簽名。此功能對於需要文件驗證、內容分析或自動處理簽署文件的應用程式至關重要。

本教學將引導您使用 GroupDocs.Signature 在 .NET 應用程式中實作影像簽章搜尋功能的過程，並提供清晰的解釋和實用的程式碼範例。

## 先決條件

在使用 GroupDocs.Signature for .NET 進行映像簽章搜尋之前，請確保您符合以下先決條件：

1. .NET 開發環境：一個功能齊全的 .NET 開發環境，例如 Visual Studio。

2. GroupDocs.Signature for .NET 函式庫：從下列位置下載並安裝 GroupDocs.Signature for .NET 函式庫 [這裡](https://releases。groupdocs.com/signature/net/).

3. 文件樣本：準備帶有影像簽名的測試文件以供驗證和測試。

4. 基本 C# 知識：了解 C# 程式設計基礎。

## 導入命名空間

首先匯入必要的命名空間來存取 GroupDocs.Signature 的功能：

```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

現在，讓我們將搜尋圖像簽名的過程分解為清晰、易於遵循的步驟：

## 步驟1：定義文檔路徑和文件訊息

首先，指定包含影像簽署的文件的路徑，並提取其檔案名稱以供參考：

```csharp
string filePath = "sample_multiple_signatures.docx";
string fileName = Path.GetFileName(filePath);
```

## 步驟2：初始化簽名對象

建立一個實例 `Signature` 透過將檔案路徑傳遞給建構函數來建立類別：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 圖像簽名搜尋代碼將在此處添加
}
```

## 步驟3：搜尋圖片簽名

使用 `Search` 方法使用適當的簽名類型來尋找文件中的影像簽名：

```csharp
// 在文件中搜尋圖像簽名
List<ImageSignature> signatures = signature.Search<ImageSignature>(SignatureType.Image);
```

## 步驟4：處理並顯示結果

迭代找到的圖像簽名並存取其屬性：

```csharp
// 顯示有關找到的圖像簽名的信息
Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} image signature(s).");

foreach (ImageSignature imageSignature in signatures)
{
    Console.WriteLine($"Found image signature at page {imageSignature.PageNumber} with size {imageSignature.Size}.");
    Console.WriteLine($"Location: X={imageSignature.Left}, Y={imageSignature.Top}");
    Console.WriteLine($"Dimensions: Width={imageSignature.Width}, Height={imageSignature.Height}");
}
```

## 完整範例

這是一個全面的工作範例，演示瞭如何在文件中搜尋圖像簽名：

```csharp
using System;
using System.IO;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace ImageSignatureSearch
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文件路徑
            string filePath = "sample_multiple_signatures.docx";
            string fileName = Path.GetFileName(filePath);
            
            // 初始化簽名實例
            using (Signature signature = new Signature(filePath))
            {
                try
                {
                    // 在文件中搜尋圖像簽名
                    List<ImageSignature> signatures = signature.Search<ImageSignature>(SignatureType.Image);
                    
                    // 顯示搜尋結果
                    Console.WriteLine($"\nSource document '{fileName}' contains {signatures.Count} image signature(s).");
                    
                    foreach (ImageSignature imageSignature in signatures)
                    {
                        Console.WriteLine($"Found image signature at page {imageSignature.PageNumber} with size {imageSignature.Size}.");
                        Console.WriteLine($"Location: X={imageSignature.Left}, Y={imageSignature.Top}");
                        Console.WriteLine($"Dimensions: Width={imageSignature.Width}, Height={imageSignature.Height}");
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

## 進階影像簽名搜尋技術

### 使用自訂搜尋選項

如需更有針對性的搜索，您可以使用 `ImageSearchOptions` 自訂您的搜尋條件：

```csharp
// 建立圖像搜尋選項
ImageSearchOptions options = new ImageSearchOptions
{
    // 在特定頁面中搜尋
    AllPages = false,
    PageNumber = 1,
    PagesSetup = new PagesSetup { Pages = new List<int> { 1, 3, 5 } },
    
    // 僅在特定頁面區域搜尋
    Rectangle = new Rectangle(100, 100, 400, 200),
    
    // 設定最小和最大影像尺寸以過濾結果
    MinWidth = 50,
    MinHeight = 50,
    MaxWidth = 300,
    MaxHeight = 300
};

// 使用自訂選項搜尋
List<ImageSignature> filteredSignatures = signature.Search<ImageSignature>(options);
```

### 處理影像簽名數據

您可以進一步處理找到的影像簽名，例如將它們儲存為單獨的檔案或分析其內容：

```csharp
foreach (ImageSignature imageSignature in signatures)
{
    // 存取影像數據
    byte[] imageData = imageSignature.ImageData;
    
    // 將圖像儲存到文件
    string outputPath = $"extracted_image_{imageSignature.PageNumber}_{Guid.NewGuid()}.png";
    File.WriteAllBytes(outputPath, imageData);
    
    Console.WriteLine($"Saved image signature to {outputPath}");
    
    // 您也可以使用第三方函式庫分析影像
    // 分析影像（影像資料）；
}
```

### 比較影像簽名

您可以實現比較邏輯來將圖像簽名與已知模板進行匹配：

```csharp
// 載入參考影像進行比較
byte[] referenceImage = File.ReadAllBytes("reference_signature.png");

foreach (ImageSignature foundSignature in signatures)
{
    // 將找到的簽名與參考影像進行比較
    // 這是一個簡化的範例 - 實際實作將使用影像處理演算法
    bool isMatch = CompareImages(foundSignature.ImageData, referenceImage);
    
    if (isMatch)
    {
        Console.WriteLine($"Found matching signature at page {foundSignature.PageNumber}!");
    }
}

// 簡單比較函數（用於說明目的）
static bool CompareImages(byte[] image1, byte[] image2)
{
    // 在實際應用中，您將實現適當的圖像比較
    // 使用特徵匹配、直方圖比較等技術。
    
    // 實際影像比較邏輯的佔位符
    return image1.Length == image2.Length;
}
```

## 結論

在本教學中，我們探討如何使用 GroupDocs.Signature for .NET 在文件中有效地搜尋影像簽章。從基本搜尋到高級技術（包括自訂搜尋條件和對找到的簽名的進一步處理），您現在掌握了在 .NET 應用程式中實現全面圖像簽名功能的知識。

GroupDocs.Signature 提供了一個強大且靈活的 API 來處理各種類型的簽名，使其成為需要簽名分析、驗證或提取功能的文件處理應用程式的絕佳選擇。

## 常見問題解答

### GroupDocs.Signature 可以偵測所有影像格式作為簽章嗎？

GroupDocs.Signature 可以偵測各種影像格式，包括 PNG、JPEG、BMP 和 GIF 作為文件中的簽名，前提是它們已正確添加為簽名元素而不是常規內容影像。

### 是否可以在文件的特定區域中搜尋影像簽名？

是的，透過使用 `Rectangle` 財產 `ImageSearchOptions`，您可以將搜尋限制在文件頁面的特定區域，這對於具有預定義簽名區域的文件很有用。

### 我可以在受密碼保護的文件中搜尋影像簽名嗎？

是的，GroupDocs.Signature 支援在受密碼保護的文件中搜索，只需在 `LoadOptions` 初始化時 `Signature` 目的：

```csharp
LoadOptions loadOptions = new LoadOptions { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // 搜尋圖片簽名
}
```

### 如何確定文件中的影像是簽名還是普通影像？

GroupDocs.Signature 專注於尋找已新增為簽名元素的圖像。如果您需要區分常規影像和簽名影像，可以使用影像位置等屬性（通常簽名會出現在特定區域），或根據您的業務邏輯實現自訂驗證。

### 我可以根據圖像簽名的大小或尺寸來過濾圖像簽名嗎？

是的， `ImageSearchOptions` 提供如下屬性 `MinWidth`， `MinHeight`， `MaxWidth`， 和 `MaxHeight` 讓您根據簽名的尺寸進行過濾，從而更容易區分不同類型的影像元素。

## 參見

* [API 參考](https://reference.groupdocs.com/signature/net/)
* [程式碼範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [產品文件](https://docs.groupdocs.com/signature/net/)
* [產品頁面](https://products.groupdocs.com/signature/net/)
* [下載最新版本](https://releases.groupdocs.com/signature/net/)
* [部落格文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [免費支援論壇](https://forum.groupdocs.com/c/signature/13)
* [臨時執照](https://purchase.groupdocs.com/temporary-license/)