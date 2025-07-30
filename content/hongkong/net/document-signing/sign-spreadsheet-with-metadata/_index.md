---
"description": "使用 GroupDocs.Signature for .NET 嵌入元資料簽名，保護並增強 Excel 電子表格的功能。新增作者資訊、時間戳記和自訂數據，以提高文件的可追溯性和真實性。"
"linktitle": "使用元資料簽署電子表格"
"second_title": "GroupDocs.簽署 .NET API"
"title": "在 C# .NET 中向 Excel 電子表格新增元資料簽名"
"url": "/zh-hant/net/document-signing/sign-spreadsheet-with-metadata/"
"weight": 13
---

## 介紹

Excel 電子表格通常包含關鍵業務資料、財務資訊和重要計算。在許多專業環境中，確保其真實性、追蹤其來源並保護其完整性至關重要。增強電子表格安全性和可追溯性的一種有效方法是嵌入元資料簽章。

本教學將引導您使用 GroupDocs.Signature for .NET 為 Excel 電子表格新增元資料簽章。透過新增元資料簽名，您可以將有價值的資訊（例如作者詳細資料、建立時間戳記、文件識別碼和其他自訂屬性）直接嵌入到電子表格文件結構中。

## 先決條件

在繼續本教學之前，請確保您已具備以下條件：

1. [適用於 .NET 的 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - 下載並安裝庫
2. 開發環境 - Visual Studio 或任何其他與 .NET 相容的 IDE
3. Excel 電子表格 - 範例電子表格檔案（XLSX、XLS 等）
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

定義來源電子表格的路徑以及簽章輸出的儲存位置：

```csharp
// 指定 Excel 檔案的路徑
string filePath = "sample.xlsx";

// 定義簽名電子表格的輸出目錄和檔案名
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");

// 確保輸出目錄存在
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 步驟2：初始化簽名對象

使用來源電子表格檔案建立 Signature 類別的實例：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 其餘代碼將放在這裡
}
```

## 步驟 3：建立和設定元資料簽名

接下來，定義元資料選項並建立電子表格元資料簽名數組：

```csharp
// 建立元資料選項對象
MetadataSignOptions options = new MetadataSignOptions();

// 建立具有不同資料類型的電子表格元資料簽章數組
SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // 字串值
    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // 日期時間值
    new SpreadsheetMetadataSignature("DocumentId", 123456),           // 整數值
    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // 雙倍值
    new SpreadsheetMetadataSignature("Amount", 123.456M),             // 十進制值
    new SpreadsheetMetadataSignature("Total", 123.456F)               // 浮點數值
};

// 將簽名收集新增至選項
options.Signatures.AddRange(signatures);
```

## 步驟 4：使用元資料對電子表格進行簽名

將元資料簽名套用到電子表格並儲存結果：

```csharp
// 簽署文件並儲存到輸出文件路徑
SignResult result = signature.Sign(outputFilePath, options);

// 顯示成功訊息
Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} metadata signature(s).");
Console.WriteLine($"Signed spreadsheet saved at: {outputFilePath}");
```

## 完整範例

以下是將所有步驟整合在一起的完整程式碼範例：

```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SignSpreadsheetWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 指定檔案路徑
            string filePath = "sample.xlsx";
            string outputFilePath = Path.Combine("Your Document Directory", "SignSpreadsheetWithMetadata", "SignedWithMetadata.xlsx");
            
            // 確保輸出目錄存在
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // 使用元資料對電子表格進行簽名
            using (Signature signature = new Signature(filePath))
            {
                // 建立元資料選項對象
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 建立具有不同資料類型的電子表格元資料簽章數組
                SpreadsheetMetadataSignature[] signatures = new SpreadsheetMetadataSignature[]
                {
                    new SpreadsheetMetadataSignature("Author", "Mr.Sherlock Holmes"), // 字串值
                    new SpreadsheetMetadataSignature("CreatedOn", DateTime.Now),      // 日期時間值
                    new SpreadsheetMetadataSignature("DocumentId", 123456),           // 整數值
                    new SpreadsheetMetadataSignature("SignatureId", 123.456D),        // 雙倍值
                    new SpreadsheetMetadataSignature("Amount", 123.456M),             // 十進制值
                    new SpreadsheetMetadataSignature("Total", 123.456F)               // 浮點數值
                };
                
                // 將簽名收集新增至選項
                options.Signatures.AddRange(signatures);
                
                // 簽署文件並儲存到文件
                SignResult result = signature.Sign(outputFilePath, options);
                
                // 顯示結果
                Console.WriteLine($"\nSource spreadsheet signed successfully with {result.Succeeded.Count} signature(s).");
                Console.WriteLine($"File saved at {outputFilePath}.");
            }
        }
    }
}
```

## 進階電子表格元資料技術

### 使用自訂和內建電子表格屬性

Excel 電子表格具有內建屬性和自訂屬性，可透過檔案屬性對話方塊存取。 GroupDocs.Signature 讓您可以同時使用以下兩種屬性：

```csharp
// 新增內建屬性
signatures = new SpreadsheetMetadataSignature[]
{
    new SpreadsheetMetadataSignature("Company", "Sherlock Holmes Consulting"),
    new SpreadsheetMetadataSignature("Category", "Financial"),
    new SpreadsheetMetadataSignature("Keywords", "budget,forecast,analysis"),
    new SpreadsheetMetadataSignature("Comments", "This spreadsheet contains confidential information"),
    new SpreadsheetMetadataSignature("Manager", "John Watson")
};
options.Signatures.AddRange(signatures);

// 新增自訂屬性
options.Signatures.Add(new SpreadsheetMetadataSignature("Department", "Finance"));
options.Signatures.Add(new SpreadsheetMetadataSignature("SecurityLevel", "Confidential"));
```

### 在簽名的電子表格中搜尋元數據

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

您可以使用相同的屬性名稱更新電子表格中的現有元資料：

```csharp
// 更新現有元數據
options.Signatures.Add(new SpreadsheetMetadataSignature("Author", "Updated Author Name"));
```

## 結論

在本綜合教學中，您學習如何使用 GroupDocs.Signature for .NET 為 Excel 電子表格新增元資料簽章。將元資料嵌入電子表格文件可以增強文件的可追溯性，提供有價值的上下文信息，並有助於確認其真實性。

電子表格中的元資料簽章在商業環境中尤其有用，因為文件來源、作者身份和版本追蹤至關重要。嵌入的元資料可以包含與組織需求相關的作者、建立時間、文件標識符以及自訂屬性的資訊。

透過使用 GroupDocs.Signature 實現元資料簽名，您可以確保您的 Excel 電子表格在其整個生命週期中保持其完整性並提供可驗證的資訊。

## 常見問題解答

### 我可以為已經定義某些屬性的電子表格新增元資料嗎？

是的，您可以在電子表格中新增新的元資料或更新現有的元資料。 GroupDocs.Signature 將處理集成，方法是添加新的屬性或更新具有相同名稱的現有屬性。

### 元資料簽名支援哪些電子表格格式？

GroupDocs.Signature for .NET 支援各種電子表格格式的元資料簽名，包括 XLSX、XLS、XLSM、ODS 等。完整清單請參閱 [官方文檔](https://docs。groupdocs.com/signature/net/).

### 電子表格中的元資料簽章對使用者可見嗎？

元資料簽名在電子表格內容本身中不可見。但是，可以透過 Excel 或其他相容應用程式中的文件屬性面板查看。

### 新增元資料後，我可以透過程式驗證電子表格是否被竄改嗎？

是的，GroupDocs.Signature 提供驗證功能，可協助偵測文件在簽章後是否已修改，包括元資料的變更。

### 新增元資料會影響電子表格功能嗎？

新增元資料對檔案大小的影響極小，且不會影響電子表格的功能。這是一種增強文件屬性的輕量級方法，不會影響計算、公式或其他 Excel 功能。

### 我可以在哪裡找到更多資源和支援？

- [API 參考](https://reference.groupdocs.com/signature/net/)
- [下載](https://releases.groupdocs.com/signature/net/)
- [範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [文件](https://docs.groupdocs.com/signature/net/)
- [產品頁面](https://products.groupdocs.com/signature/net/)
- [部落格](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [支援論壇](https://forum.groupdocs.com/c/signature/13)
- [臨時執照](https://purchase.groupdocs.com/temporary-license/)