---
"description": "使用 GroupDocs.Signature 掌握 .NET 應用程式中的文字簽章驗證。提供包含完整程式碼範例和最佳實踐的逐步實施指南。"
"linktitle": "驗證文字"
"second_title": "GroupDocs.簽署 .NET API"
"title": "驗證文件中的文字簽名"
"url": "/zh-hant/net/verify-operations/verify-text/"
"weight": 13
type: docs
---
## 介紹

文字簽名雖然通常比數位或電子簽名更簡單，但在文件管理和驗證中卻起著至關重要的作用。無論是浮水印、頁尾文字或特定的內容模式，驗證文字簽章的存在性和完整性都是文件驗證流程中的重要環節。

GroupDocs.Signature for .NET 提供了一個強大的 API，用於驗證各種格式文件中的文字簽章。本教學將指導您在 .NET 應用程式中實作文字驗證功能，確保您的文件保持完整性和真實性。

## 先決條件

在實現文字驗證功能之前，請確保您已滿足以下先決條件：

1. GroupDocs.Signature for .NET：從下載並安裝程式庫 [下載頁面](https://releases。groupdocs.com/signature/net/).
2. .NET 開發環境：Visual Studio 或任何相容的 .NET 開發環境。
3. 基礎知識：熟悉 C# 程式設計和 .NET 框架概念。
4. 測試文件：包含用於驗證目的的文字簽章的文件。

## 導入所需的命名空間

首先匯入必要的命名空間來存取 GroupDocs.Signature 功能：

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

讓我們將文字驗證過程分解為清晰、易於管理的步驟：

## 步驟 1：指定文檔路徑

```csharp
// 包含文字簽署的文件的路徑
string filePath = "sample_multiple_signatures.docx";
```

確保將範例路徑替換為包含文字簽署的文件的實際路徑。

## 步驟2：初始化簽名對象

```csharp
// 透過傳遞文件路徑建立 Signature 類別的實例
using (Signature signature = new Signature(filePath))
{
    // 驗證碼將在此處執行
}
```

Signature 類別是 GroupDocs.Signature API 中所有操作的主要入口點。

## 步驟 3：設定文字驗證選項

```csharp
// 定義文字驗證選項
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true,                               // 檢查文件的所有頁面
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature",                            // 待驗證的文本
    MatchType = TextMatchType.Contains             // 指定匹配條件
};
```

驗證選項可讓您定義驗證過程的具體標準：
- `AllPages`：設定為 true 則檢查所有文件頁面
- `SignatureImplementation`：指定文字的實作方式（原生或貼圖）
- `Text`：文件中要匹配的文字內容
- `MatchType`：文字匹配的方法（Contains、Exact、StartsWith 等）

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
    Console.WriteLine($"Document {filePath} contains valid text signatures!");
    
    // 顯示成功簽署的訊息
    foreach (TextSignature textSignature in result.Succeeded)
    {
        Console.WriteLine($"\nFound valid text signature:");
        Console.WriteLine($"Text: {textSignature.Text}");
        Console.WriteLine($"Location: Page {textSignature.PageNumber}, {textSignature.Left}x{textSignature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

此程式碼檢查驗證是否成功並提供有關已驗證的文字簽名的詳細資訊。

## 完整範例

以下是演示文字簽名驗證的完整工作範例：

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
                    TextVerifyOptions options = new TextVerifyOptions()
                    {
                        AllPages = true,
                        SignatureImplementation = TextSignatureImplementation.Native,
                        Text = "signature",
                        MatchType = TextMatchType.Contains
                    };
                    
                    // 驗證文件簽名
                    VerificationResult result = signature.Verify(options);
                    
                    // 製程驗證結果
                    if(result.IsValid)
                    {
                        Console.WriteLine($"\nDocument {filePath} was verified successfully!");
                        foreach (TextSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature is found with text: {item.Text}");
                            Console.WriteLine($"Location: Page {item.PageNumber}, position {item.Left}x{item.Top}");
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

### 使用正規表示式進行驗證

為了更靈活的模式匹配，您可以使用正規表示式：

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "Invoice\\s+#\\d{5,6}",  // 匹配諸如“發票 #12345”之類的模式
    MatchType = TextMatchType.Regex
};
```

### 驗證特定文檔區域中的文本

您可以將驗證限制在文件的特定區域：

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = false,
    PageNumber = 1,  // 僅在第一頁驗證
    
    // 定義搜尋區域（以點為單位的座標）
    PagesSetup = new PagesSetup() 
    { 
        FirstPage = true,
        LastPage = false,
        OddPages = false,
        EvenPages = false 
    },
    
    // 矩形面積（以毫米為單位）
    Rectangle = new Rectangle(10, 10, 100, 30),
    
    Text = "Confidential"
};
```

### 同時驗證多個文字模式

您可以建立多個驗證選項來檢查不同的文字模式：

```csharp
// 建立驗證選項列表
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// 新增第一個文字驗證
listOptions.Add(new TextVerifyOptions()
{
    Text = "Confidential",
    MatchType = TextMatchType.Exact
});

// 新增二次文字驗證
listOptions.Add(new TextVerifyOptions()
{
    Text = "Do not copy",
    MatchType = TextMatchType.Contains
});

// 使用多個選項進行驗證
VerificationResult result = signature.Verify(listOptions);
```

### 驗證具有特定外觀的文本

您也可以驗證具有特定格式特徵的文字：

```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    Text = "APPROVED",
    MatchType = TextMatchType.Exact,
    
    // 驗證特定外觀屬性
    ForegroundColorRGB = System.Drawing.Color.Green,
    Font = new SignatureFont() { FontFamily = "Arial", FontSize = 12, Bold = true }
};
```

## 文字驗證的最佳實踐

1. 選擇適當的符合類型：根據您的驗證要求選擇正確的符合類型（包含、精確、正規表示式）。
2. 最佳化效能：對於大型文檔，請考慮驗證特定頁面而不是整個文檔。
3. 錯誤處理：實作適當的錯誤處理，以優雅地管理意外情況。
4. 考慮大小寫敏感性：在文字匹配中要注意大小寫敏感性，特別是對於關鍵驗證。
5. 徹底測試：使用各種文件格式和文字模式進行測試驗證，以確保相容性。

## 常見問題故障排除

### 未偵測到文字
- 檢查文字格式或編碼是否會影響偵測
- 確保文字確實以常規文字（而非圖像）的形式存在於文件中
- 嘗試不同的匹配條件（包含而不是精確）

### 效能問題
- 透過定位特定頁面或區域來優化驗證
- 使用更具體的文本模式來減少誤報

### 驗證失敗
- 檢查空格、特殊字元或格式是否影響匹配
- 驗證文字不是掃描影像的一部分（需要 OCR）
- 確保文件自新增文字以來未被修改

## 結論

文字驗證是一種多功能且實用的文件驗證方法，可以單獨使用，也可以與其他驗證方法結合使用。 GroupDocs.Signature for .NET 提供了一個全面且易於使用的 API，可用於在 .NET 應用程式中實現強大的文字驗證功能。

透過遵循本逐步指南，您學會瞭如何：
- 配置並初始化文字驗證過程
- 指定各種驗證標準
- 處理和解釋驗證結果
- 實施進階驗證場景

這些功能使您能夠建立安全可靠的文件處理系統，以驗證各種文件格式的文字的真實性。

## 常見問題解答

### GroupDocs.Signature 可以驗證掃描文件中的文字嗎？
GroupDocs.Signature 主要用於數位文字驗證。對於掃描文檔，您需要先使用 OCR（光學字元辨識）技術將掃描影像轉換為文字。

### 文字驗證支援哪些文檔格式？
GroupDocs.Signature 支援多種文件格式，包括 PDF、Word 文件（DOC、DOCX）、Excel 試算表（XLS、XLSX）、PowerPoint 簡報（PPT、PPTX）、圖片等。

### 我可以驗證格式化的文字（粗體、斜體、特定字體）嗎？
是的，GroupDocs.Signature 提供了驗證具有特定格式特徵的文字的選項，包括字體系列、大小、樣式（粗體、斜體）和顏色。

### 是否可以驗證受密碼保護的文件中的文字？
是的，GroupDocs.Signature 提供了在開啟受保護的文件進行驗證時指定文件密碼的選項。

### 我可以驗證浮水印和背景文字嗎？
是的，GroupDocs.Signature 可以驗證各種類型的文字簽名，包括浮水印和背景文本，具體取決於它們在文件中的實作方式。

### 相關資源
* [GroupDocs.Signature API 參考](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature 下載](https://releases.groupdocs.com/signature/net/)
* [GitHub 上的程式碼範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [文件](https://docs.groupdocs.com/signature/net/)
* [產品頁面](https://products.groupdocs.com/signature/net/)
* [部落格文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [支援論壇](https://forum.groupdocs.com/c/signature/13)
* [臨時執照](https://purchase.groupdocs.com/temporary-license/)