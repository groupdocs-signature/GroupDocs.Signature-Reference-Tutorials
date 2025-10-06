---
"description": "使用 GroupDocs.Signature for .NET 將元資料簽章整合到 PDF 文件中。學習如何嵌入作者資訊、時間戳記和自訂數據，以增強 PDF 的真實性和可追溯性。"
"linktitle": "使用元資料簽署 PDF"
"second_title": "GroupDocs.簽署 .NET API"
"title": "在 C# .NET 中為 PDF 文件新增元資料簽名"
"url": "/zh-hant/net/document-signing/sign-pdf-with-metadata/"
"weight": 11
type: docs
---
## 介紹

PDF（可移植文件格式）文件因其一致性和平台獨立性而廣泛應用於各行各業。在許多專業環境中，確保這些文件的真實性和可追溯性至關重要。實現這一點的一個有效方法是將元資料嵌入 PDF 檔案中。

在本綜合教學中，我們將探討如何使用 GroupDocs.Signature for .NET 為 PDF 文件新增元資料簽章。元資料簽名可讓您在文件中嵌入其他信息，例如作者詳細資料、建立時間戳記、文件識別碼和自訂值，而不會明顯改變文件的外觀。

## 先決條件

在開始之前，請確保您已準備好以下事項：

1. [適用於 .NET 的 GroupDocs.Signature](https://releases.groupdocs.com/signature/net/) - 下載並安裝庫
2. 開發環境 - Visual Studio 或任何其他與 .NET 相容的 IDE
3. PDF 文件 - 用於簽名的範例 PDF 文件
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

首先，定義 PDF 文件的路徑並指定要儲存簽章輸出的位置：

```csharp
// 指定 PDF 文件的路徑
string filePath = "sample.pdf";

// 定義輸出目錄和檔案路徑
string outputDirectory = "Your Document Directory";
string outputFilePath = Path.Combine(outputDirectory, "SignPdfWithMetadata", "SignedWithMetadata.pdf");

// 確保輸出目錄存在
Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));
```

## 步驟2：初始化簽名對象

使用來源 PDF 文件建立 Signature 類別的實例：

```csharp
using (Signature signature = new Signature(filePath))
{
    // 簽名代碼將放在這裡
}
```

## 步驟 3：定義元資料選項

建立並配置元資料選項，新增各種類型的元資料簽章：

```csharp
// 建立元資料選項對象
MetadataSignOptions options = new MetadataSignOptions();

// 使用流暢的介面添加各種類型的元數據
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // 字串值
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // 日期時間值
    .Add(new PdfMetadataSignature("DocumentId", 123456))            // 整數值
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // 雙倍值
    .Add(new PdfMetadataSignature("Amount", 123.456M))              // 十進制值
    .Add(new PdfMetadataSignature("Total", 123.456F));              // 浮點數值
```

## 步驟 4：使用元資料簽署 PDF

將元資料簽章套用到 PDF 文件並儲存結果：

```csharp
// 簽署文件並儲存到輸出路徑
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

namespace SignPdfWithMetadataExample
{
    class Program
    {
        static void Main(string[] args)
        {
            // 指定檔案路徑
            string filePath = "sample.pdf";
            string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
            
            // 確保輸出目錄存在
            Directory.CreateDirectory(Path.GetDirectoryName(outputFilePath));

            // 使用元資料對 PDF 進行簽名
            using (Signature signature = new Signature(filePath))
            {
                // 建立元資料選項對象
                MetadataSignOptions options = new MetadataSignOptions();
                
                // 新增不同類型的元資料簽名
                options
                    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) // 字串值
                    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       // 日期時間值
                    .Add(new PdfMetadataSignature("DocumentId", 123456))            // 整數值
                    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         // 雙倍值
                    .Add(new PdfMetadataSignature("Amount", 123.456M))              // 十進制值
                    .Add(new PdfMetadataSignature("Total", 123.456F));              // 浮點數值
                
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

## 進階 PDF 元資料操作

### 新增具有命名空間支援的自訂元數據

PDF 文件支援具有 XML 命名空間支援的自訂元資料：

```csharp
// 使用命名空間新增自訂元數據
options.Add(new PdfMetadataSignature("CustomProperty", "Custom Value")
{
    NamespaceUri = "http://your-namespace.com/schema”
});
```

### 在簽署的 PDF 中搜尋元數據

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

### 使用標準 PDF 元數據

PDF 文件具有可存取和修改的標準元資料欄位：

```csharp
// 設定標準 PDF 元資料字段
options
    .Add(new PdfMetadataSignature("Title", "Important Contract"))
    .Add(new PdfMetadataSignature("Subject", "Legal Agreement"))
    .Add(new PdfMetadataSignature("Keywords", "contract, agreement, legal, binding"))
    .Add(new PdfMetadataSignature("Creator", "Legal Department"))
    .Add(new PdfMetadataSignature("Producer", "GroupDocs.Signature"));
```

## 結論

在本教學中，您學習如何使用 GroupDocs.Signature for .NET 為 PDF 文件新增元資料簽章。將元資料嵌入 PDF 文件，可有效增強文件真實性、添加關鍵訊息，並改善文件管理工作流程。

PDF 中的元資料簽章在商業環境中尤其重要，因為文件的可追溯性和真實性驗證至關重要。嵌入的元資料可以包含文件來源、作者、建立時間、版本以及與組織工作流程相關的自訂屬性的資訊。

透過使用 GroupDocs.Signature 實現元資料簽名，您可以確保您的 PDF 文件在其整個生命週期中保持其完整性並提供可驗證的資訊。

## 常見問題解答

### 我可以修改 PDF 文件中現有的元資料嗎？

是的，您可以修改 PDF 文件中現有的元資料。當您套用與現有元資料簽章同名的新元資料簽章時，其值將會隨之更新。

### PDF 文件中的元資料簽章對最終使用者可見嗎？

元資料簽名在文件內容本身中不可見。但是，可以透過 Adobe Acrobat 等 PDF 閱讀器的文件屬性面板或使用專門的元資料檢視工具來檢視它們。

### 我可以加密或保護 PDF 中的元資料嗎？

GroupDocs.Signature 提供文件安全選項，包括加密。您可以套用文件級加密來保護整個 PDF，包括其元資料。

### 我可以為 PDF 添加多少元資料有限制嗎？

雖然 PDF 規範沒有嚴格限制，但添加過多的元資料可能會增加檔案大小。建議在元資料中僅包含相關且必要的資訊。

### 新增元資料後，我可以透過程式驗證 PDF 是否被竄改嗎？

是的，GroupDocs.Signature 提供驗證功能，可協助偵測文件在簽章後是否已修改，包括元資料的變更。

### 我可以在哪裡找到更多資源和支援？

- [API 參考](https://reference.groupdocs.com/signature/net/)
- [下載](https://releases.groupdocs.com/signature/net/)
- [範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
- [文件](https://docs.groupdocs.com/signature/net/)
- [產品頁面](https://products.groupdocs.com/signature/net/)
- [部落格](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
- [支援論壇](https://forum.groupdocs.com/c/signature/13)
- [臨時執照](https://purchase.groupdocs.com/temporary-license/)