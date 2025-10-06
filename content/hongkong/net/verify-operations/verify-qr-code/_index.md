---
"description": "了解如何使用 GroupDocs.Signature for .NET 驗證文件中的二維碼。完整的指南包含程式碼範例和文件身份驗證的最佳實踐。"
"linktitle": "驗證二維碼"
"second_title": "GroupDocs.簽署 .NET API"
"title": "驗證文檔中的二維碼"
"url": "/zh-hant/net/verify-operations/verify-qr-code/"
"weight": 12
type: docs
---
## 介紹

文件安全是現代商業營運的關鍵環節。二維碼已成為一種日益流行的在文件中嵌入可驗證資訊的方法。 GroupDocs.Signature for .NET 提供了一個強大且靈活的解決方案，用於驗證嵌入在各種格式文件中的二維碼。

本綜合教學將引導您完成在 .NET 應用程式中實作二維碼驗證的流程，確保您的文件保持其完整性和真實性。

## 先決條件

在實現二維碼驗證功能之前，請確保您符合以下先決條件：

1. GroupDocs.Signature for .NET：從下載並安裝程式庫 [下載頁面](https://releases。groupdocs.com/signature/net/).
2. 開發環境：Visual Studio 或任何相容的 .NET 開發環境。
3. 測試文件：包含用於驗證目的的二維碼簽章的文件。
4. 基礎知識：熟悉 C# 程式設計和 .NET 框架概念。

## 導入命名空間

首先匯入所需的命名空間以存取 GroupDocs.Signature 功能：

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

## QR 圖碼驗證步驟

請依照以下詳細步驟驗證文件中的二維碼：

### 步驟 1：指定文檔路徑

```csharp
// 提供包含二維碼簽名的文件的路徑
string filePath = "sample_multiple_signatures.docx";
```

確保將範例路徑替換為文件的實際路徑。

### 步驟2：初始化簽名對象

```csharp
// 透過傳遞文件路徑建立簽章實例
using (Signature signature = new Signature(filePath))
{
    // 驗證碼將在此處執行
}
```

Signature 類別是 GroupDocs.Signature API 中所有操作的主要入口點。

### 步驟3：設定二維碼驗證選項

```csharp
// 定義二維碼驗證選項
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, // 檢查文件的所有頁面
    Text = "John",   // 二維碼內需驗證的文字
    MatchType = TextMatchType.Contains // 指定文字匹配條件
};
```

驗證選項可讓您定義驗證過程的具體標準：
- `AllPages`：設定為 true 以檢查所有文件頁面（預設行為）
- `Text`：二維碼內需要匹配的文字內容
- `MatchType`：文字匹配的方法（Contains、Exact、StartsWith 等）

### 步驟4：執行驗證流程

```csharp
// 執行驗證
VerificationResult result = signature.Verify(options);
```

這將根據您指定的選項執行驗證過程。

### 步驟5：處理驗證結果

```csharp
// 查看驗證結果並進行相應處理
if (result.IsValid)
{
    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
    
    // 顯示成功簽署的訊息
    foreach (QrCodeSignature signature in result.Succeeded)
    {
        Console.WriteLine($"Found valid QR Code signature with text: {signature.Text}");
        Console.WriteLine($"QR Code type: {signature.EncodeType.TypeName}");
        Console.WriteLine($"Location: Page {signature.PageNumber}, {signature.Left}x{signature.Top}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    Console.WriteLine($"Number of failed signatures: {result.Failed.Count}");
}
```

正確處理驗證結果可以讓您的應用程式根據驗證結果採取適當的操作。

## 完整範例

這是一個完整的、可運行的範例，演示了二維碼驗證：

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
            
            // 初始化簽名實例
            using (Signature signature = new Signature(filePath))
            {
                // 設定驗證選項
                QrCodeVerifyOptions options = new QrCodeVerifyOptions()
                {
                    AllPages = true,
                    Text = "John",
                    MatchType = TextMatchType.Contains
                };
                
                // 驗證文件簽名
                VerificationResult result = signature.Verify(options);
                
                // 製程驗證結果
                if (result.IsValid)
                {
                    Console.WriteLine($"Document {filePath} contains valid QR code signature!");
                    
                    foreach (QrCodeSignature qrSignature in result.Succeeded)
                    {
                        Console.WriteLine($"Found valid QR Code with text: {qrSignature.Text}");
                    }
                }
                else
                {
                    Console.WriteLine($"Document {filePath} failed verification process.");
                }
            }
        }
    }
}
```

## 進階驗證選項

GroupDocs.Signature 為更複雜的驗證場景提供了附加選項：

### 驗證特定二維碼類型

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    EncodeType = QrCodeTypes.QR,  // 僅驗證標準二維碼
    Text = "Confidential",
    MatchType = TextMatchType.Exact
};
```

### 在特定頁面上驗證

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = false,
    PageNumber = 2,  // 僅驗證第 2 頁
    Text = "Approved"
};
```

### 使用正規表示式進行驗證

```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    Text = "INV-\\d{6}",  // 匹配發票號碼（例如，INV-123456）
    MatchType = TextMatchType.Regex
};
```

## QR碼驗證的最佳實踐

1. 始終驗證輸入：確保文件路徑和驗證標準在處理之前有效。
2. 實作錯誤處理：使用 try-catch 區塊來處理驗證期間可能出現的異常。
3. 考慮效能：對於大型文檔，考慮驗證特定頁面而不是整個文檔。
4. 記錄驗證結果：保留驗證過程的日誌以供審計目的。
5. 使用各種文件格式進行測試：確保您的驗證適用於所有必要的文件格式。

## 結論

驗證文件中的二維碼是確保文件真實性和完整性的重要環節。 GroupDocs.Signature for .NET 提供了一個全面且使用者友好的 API，用於在 .NET 應用程式中實作二維碼驗證。

透過學習本教程，您已經學會如何：
- 配置並初始化驗證過程
- 指定各種驗證標準
- 處理和解釋驗證結果
- 實施進階驗證選項

這些知識使您能夠增強文件管理系統的安全性和可靠性。

## 常見問題解答

### GroupDocs.Signature 可以在單一文件中驗證多個二維碼嗎？
是的，GroupDocs.Signature 可以驗證單一文件中的多個二維碼。驗證結果將包含所有符合的二維碼。

### 二維碼驗證支援哪些文檔格式？
GroupDocs.Signature 支援多種文件格式，包括 PDF、Word（DOC、DOCX）、Excel（XLS、XLSX）、PowerPoint（PPT、PPTX）、圖片等。

### 我可以驗證具有特定加密或格式的二維碼嗎？
是的，GroupDocs.Signature 提供了使用特定編碼類型和內容格式模式來驗證二維碼的選項。

### 是否可以驗證第三方應用程式創建的二維碼？
是的，GroupDocs.Signature 可以驗證大多數應用程式產生的標準二維碼，只要它們遵循標準二維碼格式。

### 如何處理包含二進位資料而不是文字的二維碼？
GroupDocs.Signature 提供透過以下方式驗證二維碼的選項： `BinaryData` 驗證選項的屬性。

### 相關資源
* [GroupDocs.Signature API 參考](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature 下載](https://releases.groupdocs.com/signature/net/)
* [GitHub 上的程式碼範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [文件](https://docs.groupdocs.com/signature/net/)
* [產品頁面](https://products.groupdocs.com/signature/net/)
* [部落格文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [支援論壇](https://forum.groupdocs.com/c/signature/13)
* [臨時執照](https://purchase.groupdocs.com/temporary-license/)