---
"description": "了解如何使用 GroupDocs.Signature for .NET 在映像中簽署並嵌入元資料。新增作者資訊、時間戳記和自訂數據，以增強影像的真實性和可追溯性。"
"linktitle": "使用元資料對影像進行簽名"
"second_title": "GroupDocs.簽署 .NET API"
"title": "使用 C# .NET 中的元資料對影像進行簽名"
"url": "/zh-hant/net/document-signing/sign-image-with-metadata/"
"weight": 10
type: docs
---
## 介紹

使用元資料進行數位影像簽名對於確立真實性、所有權和可追溯性正變得越來越重要。 GroupDocs.Signature for .NET 提供了一個強大且易於使用的解決方案，用於為各種影像格式新增元資料簽章。本教學將引導您使用 C# 完成使用元資料對影像進行簽名的完整過程。

元資料簽名可讓您將有價值的資訊直接嵌入到影像檔案中，例如作者資訊、建立時間戳記、唯一識別碼等。這些資訊將成為影像檔案本身的一部分，從而提供一種可靠的方法來追蹤和驗證影像的真實性。

## 先決條件

在繼續本教學之前，請確保您已具備以下條件：

1. [適用於 .NET 的 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - 下載並安裝庫
2. 開發環境 - Visual Studio 或任何支援 .NET 的相容 IDE
3. 圖像檔案 - 支援格式（PNG、JPG、TIFF 等）的範例圖像文件
4. 基本 C# 程式設計知識 - 熟悉 C# 程式設計概念

## 導入命名空間

首先匯入必要的命名空間來存取 GroupDocs.Signature 功能：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## 步驟 1：設定檔案路徑

定義來源影像的路徑以及簽章輸出的儲存位置：

```csharp
// 指定來源影像檔案的路徑
string filePath = "sample.png";

// 定義簽名影像的輸出目錄和檔名
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignImageWithMetadata", "SignedWithMetadata.png");

// 確保輸出目錄存在
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 步驟2：初始化簽名對象

使用來源圖像檔案建立 Signature 類別的實例：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 其餘代碼將放在這裡
}
```

## 步驟 3：建立和設定元資料簽名

接下來，定義要嵌入影像的元資料。 GroupDocs.Signature 支援多種元資料資料類型：

```csharp
// 初始化元資料ID（特定於影像格式）
ushort imgsMetadataId = 41996;

// 建立元資料選項對象
MetadataSignOptions options = new MetadataSignOptions();

// 新增各種類型的元資料簽名
options
    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes"))  // 字串值
    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // 日期時間值
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // 整數值
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // 雙倍值
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // 十進制值
    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // 浮點數值
```

## 步驟 4：使用元資料對影像進行簽名

將元資料簽名套用至影像並儲存結果：

```csharp
// 簽署文件並儲存到輸出文件路徑
SignResult result = signature.Sign(outputFilePath, options);

// 顯示成功訊息
Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed image saved at: {outputFilePath}");
```

## 完整範例

以下是將所有步驟整合在一起的完整程式碼範例：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignImageWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 指定檔案路徑
            string filePath = "sample.png";            
            string outputFilePath = Path.Combine("Your Document Directory", "SignImageWithMetadata", "SignedWithMetadata.png");
            
            // 確保輸出目錄存在
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // 使用元資料對影像進行簽名
            using (Signature signature = new Signature(filePath))
            {
                // 初始化元資料ID（特定於影像格式）
                ushort imgsMetadataId = 41996;
                
                // 建立元資料選項
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 新增不同類型的元資料簽名
                options
                    .Add(new ImageMetadataSignature(imgsMetadataId++, "Mr.Sherlock Holmes")) // 字串值
                    .Add(new ImageMetadataSignature(imgsMetadataId++, DateTime.Now))          // 日期時間值
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123456))                // 整數值
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456D))              // 雙倍值
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456M))              // 十進制值
                    .Add(new ImageMetadataSignature(imgsMetadataId++, 123.456F));             // 浮點數值
                
                // 簽署文件並儲存到文件
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 顯示結果
                Console.WriteLine($"\nSource image signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 進階元資料簽章技術

### 使用自訂元數據

您也可以建立具有特定 ID 的自訂元資料欄位：

```csharp
// 使用特定 ID 建立自訂元數據
options.Add(new ImageMetadataSignature(42000, "CustomValue"));
```

### 驗證元資料簽名

簽名後，您可能需要驗證元資料簽章：

```csharp
// 建立驗證選項
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// 搜尋元資料簽名
SearchResult result = signature.Search(searchOptions);

// 顯示找到的簽名
Console.WriteLine($"Found {result.Signatures.Count} metadata signatures:");
foreach(var metadataSignature in result.Signatures)
{
    Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value}");
}
```

## 結論

在本教學中，您學習如何使用 GroupDocs.Signature for .NET 為映像新增元資料簽章。將元資料嵌入影像是增強影像真實性、添加關鍵資訊以及改善文件管理工作流程的絕佳方法。流程簡單易用，功能強大，可依您的特定需求進行客製化。

圖像檔案中嵌入的元資料可用於各種目的，例如版權保護、追蹤圖像來源、添加描述性資訊以及建立數位保管鏈。透過實施元資料簽名，您可以確保影像在整個生命週期中保持完整性和真實性。

## 常見問題解答

### 我可以為現有的簽名影像添加元資料嗎？

是的，您可以為已包含元資料簽署的影像新增額外的元資料。現有元資料將被保留，新的元資料也會相應地添加。

### 元資料簽名支援哪些影像格式？

GroupDocs.Signature for .NET 支援多種影像格式的元資料簽名，包括 PNG、JPEG、TIFF、BMP、GIF 等。完整清單請參閱 [官方文檔](https://docs。groupdocs.com/signature/net/).

### 是否可以加密影像中的元資料？

是的，GroupDocs.Signature 提供了加密元資料的選項，以增強安全性。您可以使用該庫提供的加密選項來保護敏感的元資料資訊。

### 我可以透過程式驗證簽名影像的真實性嗎？

當然。您可以使用 GroupDocs.Signature 中的驗證方法來驗證元資料簽章並確認簽章影像的真實性。

### 使用元資料對影像進行簽名時，檔案大小是否有限制？

該庫本身沒有特定的檔案大小限制，但處理非常大的檔案可能需要更多處理時間和記憶體。建議在處理超大影像時考慮系統資源。

### 我如何獲得用於測試的臨時許可證？

您可以獲得 [臨時執照](https://purchase.groupdocs.com/temporary-license/) 用於在購買之前測試 GroupDocs.Signature。

### 我可以在哪裡找到更多資源和支援？

- [API 參考](https://reference.groupdocs.com/signature/net/)
- [下載](https://releases.groupdocs.com/signature/net/)
- [範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [文件](https://docs.groupdocs.com/signature/net/)
- [產品頁面](https://products.groupdocs.com/signature/net/)
- [部落格](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [支援論壇](https://forum.groupdocs.com/c/signature/13)