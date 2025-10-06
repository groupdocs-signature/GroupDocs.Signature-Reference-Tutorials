---
"description": "使用 GroupDocs.Signature for .NET 在 Word 文件中新增元資料簽章。嵌入作者詳細資訊、時間戳記和自訂屬性，以增強文件安全性和可追溯性。"
"linktitle": "使用元資料進行符號文字處理"
"second_title": "GroupDocs.簽署 .NET API"
"title": "使用 C# .NET 中的元資料簽章增強 Word 文檔"
"url": "/zh-hant/net/document-signing/sign-word-processing-with-metadata/"
"weight": 14
type: docs
---
## 介紹

文字處理文件是商業、教育和個人通訊中最常用的文件類型之一。在許多專業環境中，確保這些文件的真實性、追蹤來源並維護其完整性至關重要。增強文件安全性和可追溯性的一種有效方法是嵌入元資料簽章。

本教學將全面指導您使用 GroupDocs.Signature for .NET 為文字處理文件新增元資料簽章。透過新增元資料簽名，您可以將有價值的資訊（例如作者詳細資料、建立時間戳記、文件識別碼和其他自訂屬性）直接嵌入到文件文件結構中。

## 先決條件

在繼續本教學之前，請確保您已具備以下條件：

1. [適用於 .NET 的 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - 下載並安裝庫
2. 開發環境 - Visual Studio 或任何其他與 .NET 相容的 IDE
3. Word 文件 - 範例文件文件（DOCX、DOC 等）
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

定義來源 Word 文件的路徑以及簽章輸出的儲存位置：

```csharp
// 指定 Word 文件的路徑
string filePath = "sample.docx";

// 定義簽章文件的輸出目錄與檔名
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");

// 確保輸出目錄存在
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 步驟2：初始化簽名對象

使用來源 Word 文件建立 Signature 類別的實例：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 其餘代碼將放在這裡
}
```

## 步驟 3：建立和設定元資料簽名

接下來，定義元資料選項並新增不同類型的元資料簽章：

```csharp
// 建立元資料選項對象
MetadataSignOptions options = new MetadataSignOptions();

// 使用流暢的介面添加各種類型的元數據
options
    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // 字串值
    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // 日期時間值
    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // 整數值
    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // 雙倍值
    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // 十進制值
    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // 浮點數值
```

## 步驟 4：使用元資料簽署文檔

將元資料簽章套用到 Word 文件並儲存結果：

```csharp
// 簽署文件並儲存到輸出文件路徑
SignResult result = signature.Sign(outputFilePath, options);

// 顯示成功訊息
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed document saved at: {outputFilePath}");
```

## 完整範例

以下是將所有步驟整合在一起的完整程式碼範例：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignWordProcessingWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 指定檔案路徑
            string filePath = "sample.docx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignWordProcessingWithMetadata", "SignedWithMetadata.docx");
            
            // 確保輸出目錄存在
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // 使用元資料對 Word 文件進行簽名
            using (Signature signature = new Signature(filePath))
            {
                // 建立元資料選項對象
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 新增不同類型的元資料簽名
                options
                    .Add(new WordProcessingMetadataSignature("Author", "Mr.Sherlock Holmes")) // 字串值
                    .Add(new WordProcessingMetadataSignature("CreatedOn", DateTime.Now))      // 日期時間值
                    .Add(new WordProcessingMetadataSignature("DocumentId", 123456))           // 整數值
                    .Add(new WordProcessingMetadataSignature("SignatureId", 123.456D))        // 雙倍值
                    .Add(new WordProcessingMetadataSignature("Amount", 123.456M))             // 十進制值
                    .Add(new WordProcessingMetadataSignature("Total", 123.456F));             // 浮點數值
                
                // 簽署文件並儲存到文件
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 顯示結果
                Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 進階 Word 文件元資料技術

### 使用自訂和內建文件屬性

Word 文件具有內建屬性和自訂屬性，可透過文件屬性面板存取。 GroupDocs.Signature 讓您可以同時使用以下兩種屬性：

```csharp
// 新增內建屬性
options
    .Add(new WordProcessingMetadataSignature("Company", "Sherlock Holmes Consulting"))
    .Add(new WordProcessingMetadataSignature("Category", "Legal Document"))
    .Add(new WordProcessingMetadataSignature("Keywords", "contract,agreement,legal"))
    .Add(new WordProcessingMetadataSignature("Comments", "This document is confidential"))
    .Add(new WordProcessingMetadataSignature("Manager", "John Watson"));

// 新增自訂屬性
options.Add(new WordProcessingMetadataSignature("Department", "Legal"));
options.Add(new WordProcessingMetadataSignature("SecurityLevel", "Confidential"));
```

### 在簽署的 Word 文件中搜尋元數據

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

### 使用文件變數

Word 文件還支援文件變量，這是另一種形式的元資料：

```csharp
// 新增文件變數
options.Add(new WordProcessingMetadataSignature("DocVariable1", "Custom Value 1", true));
options.Add(new WordProcessingMetadataSignature("DocVariable2", DateTime.Now, true));
```

## 結論

在本綜合教學中，您學習如何使用 GroupDocs.Signature for .NET 為 Word 處理文件新增元資料簽章。將元資料嵌入 Word 文件可以增強文件的可追溯性，提供有價值的上下文信息，並有助於確認文件的真實性。

Word 文件中的元資料簽章在商業和法律環境中尤其有用，因為這些環境中文件來源、作者身份和版本追蹤非常重要。嵌入的元資料可以包含與組織需求相關的作者、建立時間、文件標識符和自訂屬性的資訊。

透過使用 GroupDocs.Signature 實現元資料簽名，您可以確保您的 Word 文件在其整個生命週期中保持其完整性並提供可驗證的資訊。

## 常見問題解答

### 我可以為已經定義某些屬性的 Word 文件新增元資料嗎？

是的，您可以在 Word 文件中新增新的元資料或更新現有的元資料。 GroupDocs.Signature 將處理集成，方法是添加新的屬性或更新具有相同名稱的現有屬性。

### 元資料簽章支援哪些文字處理格式？

GroupDocs.Signature for .NET 支援各種文字處理格式的元資料簽名，包括 DOCX、DOC、RTF、ODT 等。完整清單請參閱 [文件](https://docs。groupdocs.com/signature/net/).

### Word 文件中的元資料簽章對讀者可見嗎？

元資料簽名在文件內容本身中不可見。但是，可以透過 Microsoft Word 或其他相容應用程式中的文件屬性面板查看。

### 新增元資料後，我可以透過程式驗證 Word 文件是否被竄改嗎？

是的，GroupDocs.Signature 提供驗證功能，可協助偵測文件在簽章後是否已修改，包括元資料的變更。

### 是否可以從 Word 文件中刪除元資料？

是的，GroupDocs.Signature 提供了根據需要從文件中刪除元資料簽章的選項。這對於在外部共用文件之前清理敏感資訊非常有用。

### 我可以在哪裡找到更多資源和支援？

- [API 參考](https://reference.groupdocs.com/signature/net/)
- [下載](https://releases.groupdocs.com/signature/net/)
- [範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [文件](https://docs.groupdocs.com/signature/net/)
- [產品頁面](https://products.groupdocs.com/signature/net/)
- [部落格](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [支援論壇](https://forum.groupdocs.com/c/signature/13)
- [臨時執照](https://purchase.groupdocs.com/temporary-license/)