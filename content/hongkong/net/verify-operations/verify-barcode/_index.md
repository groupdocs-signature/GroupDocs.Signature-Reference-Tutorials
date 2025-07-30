---
"description": "使用 GroupDocs.Signature 在 .NET 應用程式中實現強大的條碼驗證。完整的程式碼範例和最佳實踐，確保文件真實性。"
"linktitle": "驗證條碼"
"second_title": "GroupDocs.簽署 .NET API"
"title": "驗證文件中的條碼簽名"
"url": "/zh-hant/net/verify-operations/verify-barcode/"
"weight": 10
---

## 介紹

條碼已成為現代文件管理系統不可或缺的一部分，它不僅能夠快速存取編碼訊息，還能起到安全保護的作用。 GroupDocs.Signature for .NET 提供了強大的 API，用於驗證文件中的條碼簽名，確保其真實性和完整性。

本教學全面探討如何使用 GroupDocs.Signature 在 .NET 應用程式中實作條碼驗證。無論您處理的是商業文件、憑證、合同，或是任何使用條碼進行身份驗證的文件類型，本指南都能協助您實現強大的驗證功能。

## 先決條件

在實施條碼驗證功能之前，請確保您已滿足以下先決條件：

1. GroupDocs.Signature for .NET：從下載並安裝程式庫 [下載頁面](https://releases。groupdocs.com/signature/net/).
2. .NET 開發環境：Visual Studio 或任何相容的 .NET 開發環境。
3. 基礎知識：熟悉 C# 程式設計和 .NET 框架概念。
4. 測試文件：包含用於驗證目的的條碼簽章的文件。

## 導入所需的命名空間

首先匯入必要的命名空間來存取 GroupDocs.Signature 功能：

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

讓我們將條碼驗證流程分解為清晰、易於管理的步驟：

## 步驟 1：指定文檔路徑

```csharp
// 包含條碼簽名的文件的路徑
string filePath = "sample_multiple_signatures.docx";
```

確保將範例路徑替換為包含條碼簽署的文件的實際路徑。

## 步驟2：初始化簽名對象

```csharp
// 透過傳遞文件路徑建立 Signature 類別的實例
using (Signature signature = new Signature(filePath))
{
    // 驗證碼將在此處執行
}
```

Signature 類別是 GroupDocs.Signature API 中所有操作的主要入口點。

## 步驟3：設定條碼驗證選項

```csharp
// 定義條碼驗證選項
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = true,           // 檢查文件的所有頁面
    Text = "12345",            // 條碼內相符的文本
    MatchType = TextMatchType.Contains // 指定文字匹配條件
};
```

驗證選項可讓您定義驗證過程的具體標準：
- `AllPages`：設定為 true 則檢查所有文件頁面
- `Text`：條碼中需要匹配的文字內容
- `MatchType`：文字匹配的方法（Contains、Exact、StartsWith、EndsWith）

## 步驟4：執行驗證流程

```csharp
// 執行驗證
VerificationResult result = signature.Verify(options);
```

這將根據您指定的選項執行驗證過程。

## 步驟5：處理驗證結果

```csharp
// 查看驗證結果並進行相應處理
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
    
    // 顯示成功簽署的訊息
    foreach (BarcodeSignature barcodeSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid barcode signature:");
        Console.WriteLine($"Text: {barcodeSignature.Text}");
        Console.WriteLine($"Type: {barcodeSignature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {barcodeSignature.PageNumber}, {barcodeSignature.Left}x{barcodeSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

此程式碼檢查驗證是否成功並提供有關已驗證的條碼簽名的詳細資訊。

## 完整範例

以下是演示條碼驗證的完整工作範例：

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace GroupDocs.Signature.Examples
{
    class Program
    {
        static void Main(string[] args)
        {
            // 文件路徑
            string filePath = "sample_multiple_signatures.docx";
            
            try
            {
                // 初始化簽名實例
                using (Signature signature = new Signature(filePath))
                {
                    // 設定驗證選項
                    BarcodeVerifyOptions options = new BarcodeVerifyOptions()
                    {
                        AllPages = true,
                        Text = "12345",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // 驗證文件簽名
                    VerificationResult result = signature.Verify(options);
                    
                    // 製程驗證結果
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid barcode signatures!");
                        
                        foreach (BarcodeSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found with text: {item.Text}");
                            Console.WriteLine($"Barcode type: {item.EncodeType.TypeName}");
                            Console.WriteLine($"Page: {item.PageNumber}");
                        }
                    }
                    else
                    {
                        Console.WriteLine($"\nDocument {filePath} failed verification process.");
                    }
                }
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Error: {ex.Message}");
            }
        }
    }
}
```

## 進階驗證場景

GroupDocs.Signature 為更複雜的驗證場景提供了附加選項：

### 驗證特定條碼類型

如果您知道要尋找的特定條碼類型，則可以將驗證限制為該類型：

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,  // 僅驗證 Code128 條碼
    Text = "PROD-12345",
    MatchType = TextMatchType.Exact
};
```

### 驗證特定頁面上的條碼

對於多頁文檔，您可以將驗證限制在特定頁面：

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // 僅驗證第 2 頁
    Text = "INV-2023"
};
```

### 使用正規表示式進行驗證

為了更靈活的模式匹配，您可以使用正規表示式：

```csharp
BarcodeVerifyOptions options = new BarcodeVerifyOptions()
{
    Text = "INV-\\d{4}-\\d{2}",  // 匹配發票號碼，例如 INV-2023-01
    MatchType = TextMatchType.Regex
};
```

### 同時驗證多種條碼類型

您可以建立多個驗證選項來檢查不同的條碼類型：

```csharp
// 建立驗證選項列表
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// 新增二維碼驗證
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.QR,
    Text = "Security"
});

// 新增Code128驗證
listOptions.Add(new BarcodeVerifyOptions()
{
    EncodeType = BarcodeTypes.Code128,
    Text = "12345"
});

// 使用多個選項進行驗證
VerificationResult result = signature.Verify(listOptions);
```

## 條碼驗證的最佳實踐

1. 錯誤處理：始終實作適當的錯誤處理，以優雅地管理意外情況。
2. 效能最佳化：對於大型文檔，考慮驗證特定頁面而不是整個文檔。
3. 日誌記錄：實施日誌記錄以追蹤驗證嘗試和結果，以供審計目的。
4. 安全注意事項：安全地儲存驗證標準，尤其是當它們是您的安全基礎架構的一部分時。
5. 測試：使用各種文件格式和條碼類型進行測試驗證，以確保相容性。

## 常見問題故障排除

### 未偵測到條碼
- 確保文件中的條碼清晰可見
- 檢查 GroupDocs.Signature 是否支援條碼類型
- 確認條碼沒有扭曲或損壞

### 驗證失敗
- 確認驗證標準（文字、條碼類型）正確
- 檢查 MatchType 是否適合您的用例
- 驗證文件自套用條碼以來未被修改

### 效能問題
- 透過定位需要條碼的特定頁面來優化驗證
- 如果事先知道，則將驗證限制為特定的條碼類型

## 結論

條碼驗證是現代文件管理系統中確保文件真實性和完整性的重要工具。 GroupDocs.Signature for .NET 提供了一個全面且易於使用的 API，用於在您的 .NET 應用程式中實現強大的條碼驗證功能。

透過遵循本逐步指南，您學會瞭如何：
- 配置並初始化驗證過程
- 指定各種驗證標準
- 處理和解釋驗證結果
- 實施進階驗證場景

這些功能使您能夠建立安全可靠的文件處理系統，以驗證各種文件格式的條碼的真實性。

## 常見問題解答

### 條碼驗證支援哪些文檔格式？
GroupDocs.Signature 支援多種文件格式，包括 PDF、Word 文件（DOC、DOCX）、Excel 試算表（XLS、XLSX）、PowerPoint 簡報（PPT、PPTX）、圖片等。

### GroupDocs.Signature 可以在單一文件中驗證多個條碼嗎？
是的，GroupDocs.Signature 可以驗證單一文件中的多個條碼。驗證結果將包含所有符合的條碼。

### 支援哪些條碼類型驗證？
GroupDocs.Signature 支援多種條碼類型，包括 Code39、Code128、EAN13、EAN8、QR Code、DataMatrix、PDF417 等。

### 我可以驗證受密碼保護的文件中的條碼嗎？
是的，GroupDocs.Signature 提供了在開啟受保護的文件進行驗證時指定文件密碼的選項。

### 是否可以驗證包含二進位資料而不是文字的條碼？
是的，GroupDocs.Signature 提供了透過以下方式驗證帶有二進位資料的條碼的選項： `BinaryData` 驗證選項的屬性。

### 相關資源
* [GroupDocs.Signature API 參考](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature 下載](https://releases.groupdocs.com/signature/net/)
* [GitHub 上的程式碼範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [文件](https://docs.groupdocs.com/signature/net/)
* [產品頁面](https://products.groupdocs.com/signature/net/)
* [部落格文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [支援論壇](https://forum.groupdocs.com/c/signature/13)
* [臨時執照](https://purchase.groupdocs.com/temporary-license/)