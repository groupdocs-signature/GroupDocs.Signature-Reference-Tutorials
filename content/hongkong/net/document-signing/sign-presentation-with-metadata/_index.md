---
"description": "了解如何使用 GroupDocs.Signature for .NET 將元資料簽章嵌入 PowerPoint 簡報。新增作者詳細資訊、時間戳記和自訂屬性，以提高簡報的真實性和可追溯性。"
"linktitle": "使用元資料進行簽署演示"
"second_title": "GroupDocs.簽署 .NET API"
"title": "使用 C# .NET 中的元資料簽章增強 PowerPoint 簡報"
"url": "/zh-hant/net/document-signing/sign-presentation-with-metadata/"
"weight": 12
type: docs
---
## 介紹

在當今的數位化工作場所中，簡報是溝通和分享資訊的重要工具。確保這些簡報文件的真實性和完整性變得越來越重要，尤其是在企業和教育環境中。增強簡報安全性和可追溯性的有效方法是嵌入元資料簽章。

本教學將引導您使用 GroupDocs.Signature for .NET 為 PowerPoint 簡報（PPTX、PPT）新增元資料簽章。透過新增元資料簽名，您可以將有價值的資訊（例如作者詳細資訊、建立時間戳記、文件識別碼和其他自訂屬性）直接嵌入到簡報文件結構中。

## 先決條件

在繼續本教學之前，請確保您已具備以下條件：

1. [適用於 .NET 的 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - 下載並安裝庫
2. 開發環境 - Visual Studio 或任何其他與 .NET 相容的 IDE
3. PowerPoint 簡報 - 範例簡報文件（PPTX 或 PPT 格式）
4. 基本 C# 知識 - 熟悉 C# 程式語言

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

定義來源簡報的路徑以及簽章輸出的儲存位置：

```csharp
// 指定簡報文件的路徑
string filePath = "sample.pptx";

// 定義簽章簡報的輸出目錄和檔名
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPresentationWithMetadata", "SignedWithMetadata.pptx");

// 確保輸出目錄存在
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 步驟2：初始化簽名對象

使用來源示範檔案建立 Signature 類別的實例：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 其餘代碼將放在這裡
}
```

## 步驟 3：建立和設定元資料簽名

接下來，定義元資料選項並建立演示元資料簽名數組：

```csharp
// 建立元資料選項對象
MetadataSignOptions options = new MetadataSignOptions();

// 建立具有不同資料類型的演示元資料簽章數組
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Sherlock Holmes"), // 字串值
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),      // 日期時間值
    new PresentationMetadataSignature("DocumentId", 123456),           // 整數值
    new PresentationMetadataSignature("SignatureId", 123.456D),        // 雙倍值
    new PresentationMetadataSignature("Amount", 123.456M),             // 十進制值
    new PresentationMetadataSignature("Total", 123.456F)               // 浮點數值
};

// 將簽名收集新增至選項
options.Signatures.AddRange(signatures);
```

## 步驟 4：使用元資料對簡報進行簽名

將元資料簽章套用至簡報並儲存結果：

```csharp
// 簽署文件並儲存到輸出文件路徑
SignResult result = signature.Sign(outputFilePath, options);

// 顯示成功訊息
Console.WriteLine($"\nSource presentation signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed presentation saved at: {outputFilePath}");
```

## 完整範例

以下是將所有步驟整合在一起的完整程式碼範例：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignPresentationWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 指定檔案路徑
            string filePath = "sample.pptx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
            
            // 確保輸出目錄存在
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // 使用元資料對簡報進行簽名
            using (Signature signature = new Signature(filePath))
            {
                // 建立元資料選項對象
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 建立具有不同資料類型的演示元資料簽章數組
                PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
                {
                    new PresentationMetadataSignature("Author", "Mr.Sherlock Holmes"), // 字串值
                    new PresentationMetadataSignature("CreatedOn", DateTime.Now),      // 日期時間值
                    new PresentationMetadataSignature("DocumentId", 123456),           // 整數值
                    new PresentationMetadataSignature("SignatureId", 123.456D),        // 雙倍值
                    new PresentationMetadataSignature("Amount", 123.456M),             // 十進制值
                    new PresentationMetadataSignature("Total", 123.456F)               // 浮點數值
                };
                
                // 將簽名收集新增至選項
                options.Signatures.AddRange(signatures);
                
                // 簽署文件並儲存到文件
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 顯示結果
                Console.WriteLine($"\nSource presentation signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 進階演示元資料技術

### 使用自訂和內建演示屬性

PowerPoint 簡報具有內建屬性和自訂屬性，可透過檔案屬性對話方塊存取。 GroupDocs.Signature 讓您可以同時使用以下兩種屬性：

```csharp
// 新增內建屬性
signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new PresentationMetadataSignature("Category", "Presentation"),
    new PresentationMetadataSignature("Keywords", "metadata,signing,groupdocs"),
    new PresentationMetadataSignature("Comments", "This document was signed with GroupDocs.Signature"),
    new PresentationMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// 新增自訂屬性
options.Signatures.Add(new PresentationMetadataSignature("CustomProperty1", "Custom Value 1"));
options.Signatures.Add(new PresentationMetadataSignature("CustomProperty2", "Custom Value 2"));
```

### 在簽署的簡報中搜尋元數據

簽名後，您可能需要驗證或提取元資料：

```csharp
// 建立元資料的搜尋選項
MetadataSearchOptions searchOptions = new MetadataSearchOptions();

// 搜尋元資料簽名
SearchResult searchResult = signature.Search(searchOptions);

// 顯示找到的簽名
Console.WriteLine($"Found {searchResult.Signatures.Count} metadata signatures:");
foreach (var foundSignature in searchResult.Signatures)
{
    MetadataSignature metadataSignature = foundSignature as MetadataSignature;
    if (metadataSignature != null)
    {
        Console.WriteLine($"- {metadataSignature.Name}: {metadataSignature.Value} ({metadataSignature.Value.GetType().Name})");
    }
}
```

### 更新現有元數據

您可以使用相同的屬性名稱來更新簡報中的現有元資料：

```csharp
// 更新現有元數據
options.Signatures.Add(new PresentationMetadataSignature("Author", "Updated Author Name"));
```

## 結論

在本綜合教學中，您學習如何使用 GroupDocs.Signature for .NET 為 PowerPoint 簡報新增元資料簽章。將元資料嵌入簡報文件可以增強文件的可追溯性，提供有價值的上下文信息，並有助於確認其真實性。

簡報中的元資料簽章在商業和教育環境中尤其有用，因為文件來源、作者身分和版本追蹤非常重要。嵌入的元資料可以包含與組織需求相關的作者、建立時間、文件標識符和自訂屬性的資訊。

透過使用 GroupDocs.Signature 實現元資料簽名，您可以確保您的 PowerPoint 簡報在其整個生命週期中保持其完整性並提供可驗證的資訊。

## 常見問題解答

### 我可以為已經定義某些屬性的簡報新增元資料嗎？

是的，您可以在簡報中新增新的元資料或更新現有的元資料。 GroupDocs.Signature 將處理集成，方法是添加新的屬性或更新具有相同名稱的現有屬性。

### 元資料簽章支援哪些表示格式？

GroupDocs.Signature for .NET 支援對 PPT、PPTX、PPTM、PPS、PPSX 和其他 PowerPoint 格式的簡報進行元資料簽署。完整清單請參閱 [官方文檔](https://docs。groupdocs.com/signature/net/).

### 簡報中的元資料簽章對觀眾可見嗎？

元資料簽章在簡報幻燈片本身中不可見。但是，可以透過 PowerPoint 或其他相容應用程式中的文件屬性面板查看。

### 我可以加密簡報中的敏感元資料嗎？

雖然無法加密單一元資料屬性，但 GroupDocs.Signature 提供了保護整個文件的選項。您可以套用密碼保護來限制對簡報及其元資料的存取。

### 新增元資料是否會影響演示效能？

新增元資料對檔案大小的影響極小，且不會影響呈現效能。這是一種輕量級的增強文件屬性的方法，不會影響使用者體驗。

### 我可以在哪裡找到更多資源和支援？

- [API 參考](https://reference.groupdocs.com/signature/net/)
- [下載](https://releases.groupdocs.com/signature/net/)
- [範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [文件](https://docs.groupdocs.com/signature/net/)
- [產品頁面](https://products.groupdocs.com/signature/net/)
- [部落格](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [支援論壇](https://forum.groupdocs.com/c/signature/13)
- [臨時執照](https://purchase.groupdocs.com/temporary-license/)