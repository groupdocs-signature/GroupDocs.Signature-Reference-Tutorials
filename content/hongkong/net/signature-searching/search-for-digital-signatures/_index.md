---
"description": "使用 GroupDocs.Signature for .NET 輕鬆搜尋文件中的數位簽章。使用我們詳細的逐步指南，增強文件安全性和驗證能力。"
"linktitle": "搜尋數位簽名"
"second_title": "GroupDocs.簽署 .NET API"
"title": "在文件中搜尋數位簽名"
"url": "/zh-hant/net/signature-searching/search-for-digital-signatures/"
"weight": 11
type: docs
---
## 介紹

在當今的數位環境中，確保文件的真實性和完整性對企業和組織至關重要。數位簽章提供了一種強大的機制來驗證文件的真實性和檢測未經授權的修改。 GroupDocs.Signature for .NET 提供了一個全面的解決方案，用於處理各種文件格式的數位簽名，使開發人員能夠將簽名功能無縫整合到他們的 .NET 應用程式中。

本教學將引導您使用 GroupDocs.Signature for .NET 在文件中搜尋數位簽章的流程，並提供詳細的解釋和實際的程式碼範例。

## 先決條件

在深入了解實作細節之前，請確保您符合以下先決條件：

1. GroupDocs.Signature for .NET：從以下位置下載並安裝該程式庫 [這裡](https://releases。groupdocs.com/signature/net/).
   
2. 開發環境：使用 Visual Studio 或您喜歡的 IDE 設定 .NET 開發環境。
   
3. 範例文件：準備包含數位簽章的範例文件以供測試目的。

4. 基礎知識：熟悉 C# 程式語言和 .NET 框架基礎知識。

## 導入命名空間

首先匯入所需的命名空間以存取 GroupDocs.Signature for .NET 提供的功能：

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

現在，讓我們將搜尋數位簽章的流程分解為清晰、易於管理的步驟：

## 步驟1：初始化簽名對象

首先建立一個實例 `Signature` 類，將路徑傳遞給您的文件：

```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    // 搜尋數位簽名的代碼將在此處添加
}
```

## 第 2 步：搜尋數位簽名

接下來，使用 `Search` 方法與 `SignatureType.Digital` 在文件中搜尋數位簽章的參數：

```csharp
// 在文件中搜尋數位簽名
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
```

## 步驟3：處理並顯示結果

最後，處理搜尋結果並顯示找到的數位簽章的相關資訊：

```csharp
Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
foreach (var digitalSignature in signatures)
{
    Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
    Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
    Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
    Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
    Console.WriteLine();
}
```

## 完整範例

這是一個完整的、可運行的範例，示範如何在文件中搜尋數位簽章：

```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;

namespace SearchDigitalSignatures
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
                // 在文件中搜尋數位簽名
                List<DigitalSignature> signatures = signature.Search<DigitalSignature>(SignatureType.Digital);
                
                // 顯示搜尋結果
                Console.WriteLine($"\nSource document ['{filePath}'] contains the following digital signatures:");
                
                if (signatures.Count > 0)
                {
                    foreach (var digitalSignature in signatures)
                    {
                        Console.WriteLine($"Digital signature found from {digitalSignature.SignTime} with validation status: {digitalSignature.IsValid}");
                        Console.WriteLine($"Certificate: Subject: {digitalSignature.Certificate?.SubjectName}");
                        Console.WriteLine($"Certificate: Issuer: {digitalSignature.Certificate?.IssuerName}");
                        Console.WriteLine($"Certificate: Serial Number: {digitalSignature.Certificate?.SerialNumber}");
                        Console.WriteLine();
                    }
                }
                else
                {
                    Console.WriteLine("No digital signatures found in the document.");
                }
            }
        }
    }
}
```

## 進階搜尋選項

如需更有針對性的搜索，您可以使用 `DigitalSearchOptions` 自訂搜尋條件：

```csharp
// 建立數位搜尋選項
DigitalSearchOptions options = new DigitalSearchOptions()
{
    // 僅搜尋特定頁面（例如第 1 頁和第 2 頁）
    PageNumber = 1,
    PagesSetup = new PagesSetup() { Pages = new List<int> { 1, 2 } },
    
    // 按數位簽名中的註釋進行過濾
    Comments = "Approved",
    
    // 設定搜尋的日期和時間範圍
    SignDateTimeFrom = new DateTime(2022, 1, 1),
    SignDateTimeTo = DateTime.Now
};

// 使用特定選項進行搜尋
List<DigitalSignature> signatures = signature.Search<DigitalSignature>(options);
```

## 使用證書資訊

數位簽章包含您可以存取和驗證的寶貴證書資訊：

```csharp
foreach (var digitalSignature in signatures)
{
    if (digitalSignature.Certificate != null)
    {
        // 存取憑證屬性
        Console.WriteLine($"Certificate Valid From: {digitalSignature.Certificate.NotBefore}");
        Console.WriteLine($"Certificate Valid To: {digitalSignature.Certificate.NotAfter}");
        
        // 檢查證書是否在有效日期範圍內
        bool isDateValid = DateTime.Now >= digitalSignature.Certificate.NotBefore && 
                          DateTime.Now <= digitalSignature.Certificate.NotAfter;
        
        Console.WriteLine($"Certificate Date Validity: {isDateValid}");
        
        // 訪問證書頒發者詳細信息
        Console.WriteLine($"Certificate Issuer: {digitalSignature.Certificate.IssuerName}");
    }
}
```

## 結論

GroupDocs.Signature for .NET 提供了一個強大且靈活的解決方案，用於在文件中搜尋和驗證數位簽章。在本教程中，我們逐步探索了在 .NET 應用程式中實現數位簽章搜尋功能的過程，為您提供了增強文件安全性和完整性驗證的知識。

透過利用 GroupDocs.Signature，您可以建立強大的文件管理系統，確保數位文件的真實性和完整性，從而在業務流程中建立信任和合規性。

## 常見問題解答

### GroupDocs.Signature 可以驗證數位簽章的有效性嗎？

是的，GroupDocs.Signature 在搜尋過程中自動驗證數位簽名，並透過 `IsValid` 的財產 `DigitalSignature` 班級。

### 哪些文件格式支援數位簽章搜尋？

GroupDocs.Signature 支援各種格式的數位簽章搜索，包括 PDF、Microsoft Office 文件（Word、Excel、PowerPoint）、OpenOffice 格式等。

### 我可以在受密碼保護的文件中搜尋數位簽章嗎？

是的，您可以在初始化時提供密碼，在受密碼保護的文件中搜尋數位簽名 `Signature` 目的：

```csharp
LoadOptions loadOptions = new LoadOptions() { Password = "your_password" };
using (Signature signature = new Signature(filePath, loadOptions))
{
    // 搜尋數位簽名
}
```

### 如何驗證數位簽章是否由特定的人創建？

您可以檢查憑證的主題名稱和其他屬性來驗證簽署者的身分：

```csharp
foreach (var signature in signatures)
{
    if (signature.Certificate?.SubjectName?.Contains("John Doe") == true)
    {
        Console.WriteLine("Found signature by John Doe");
    }
}
```

### 我可以從數位簽章憑證中提取公鑰嗎？

是的，您可以透過憑證屬性存取公鑰資訊：

```csharp
if (signature.Certificate != null)
{
    // 存取公鑰資訊
    Console.WriteLine($"Public Key: {signature.Certificate.GetPublicKeyString()}");
}
```

## 參見

* [API 參考](https://reference.groupdocs.com/signature/net/)
* [程式碼範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [產品文件](https://docs.groupdocs.com/signature/net/)
* [產品頁面](https://products.groupdocs.com/signature/net/)
* [下載最新版本](https://releases.groupdocs.com/signature/net/)
* [部落格文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [支援論壇](https://forum.groupdocs.com/c/signature/13)
* [臨時執照](https://purchase.groupdocs.com/temporary-license/)