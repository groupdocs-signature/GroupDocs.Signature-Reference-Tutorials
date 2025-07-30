---
"description": "使用 GroupDocs.Signature 在 .NET 應用程式中實現安全的數位簽章驗證。提供文件身份驗證的逐步指南和完整的程式碼範例。"
"linktitle": "驗證數位簽名"
"second_title": "GroupDocs.簽署 .NET API"
"title": "驗證文件中的數位簽名"
"url": "/zh-hant/net/verify-operations/verify-digital/"
"weight": 11
---

## 介紹

在現代商業流程中，數位簽章在確保文件的真實性、完整性和不可否認性方面發揮著至關重要的作用。與傳統的手寫簽名不同，數位簽名使用加密技術來驗證簽名者的身份，並確保文件自簽名以來未被更改。

GroupDocs.Signature for .NET 提供了一個全面的工具包，使開發人員能夠在其 .NET 應用程式中實現強大的數位簽章驗證。本詳細教學將引導您完成使用 GroupDocs.Signature for .NET 驗證文件中數位簽章的流程。

## 先決條件

在實施數位簽章驗證功能之前，請確保您已滿足以下先決條件：

1. GroupDocs.Signature for .NET：從以下位置下載並安裝該程式庫 [GroupDocs.Signature for .NET 版本](https://releases。groupdocs.com/signature/net/).
2. .NET 開發環境：Visual Studio 或任何相容的 .NET 開發環境。
3. 數位憑證：用於簽署文件的數位憑證檔案（例如 .pfx）或屬於受信任鏈的憑證。
4. 待驗證文件：包含需要驗證的數位簽章的文件。

## 導入所需的命名空間

首先匯入必要的命名空間來存取 GroupDocs.Signature 功能：

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```

讓我們將驗證數位簽章的過程分解為清晰、易於管理的步驟：

## 步驟 1：指定文檔路徑

```csharp
// 包含數位簽章的文件的路徑
string filePath = "sample_multiple_signatures.docx";
```

將範例路徑替換為包含數位簽章的文件的實際路徑。

## 步驟2：初始化簽名對象

```csharp
// 透過傳遞文件路徑建立 Signature 類別的實例
using (Signature signature = new Signature(filePath))
{
    // 驗證碼將在此處執行
}
```

Signature 類別是 GroupDocs.Signature API 中所有操作的主要入口點。

## 步驟 3：設定數位驗證選項

```csharp
// 設定驗證選項
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",     // 預期簽署者聯絡方式
    Password = "1234567890",  // 如果需要，證書密碼
    AllPages = true           // 檢查所有頁面的簽名
};
```

驗證選項可讓您指定：
- 數位憑證檔案路徑
- 預期簽署者聯絡資訊
- 如果憑證受密碼保護，則輸入憑證的密碼
- 驗證頁面範圍（預設為所有頁面）

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
    Console.WriteLine($"Document {filePath} contains valid digital signatures!");
    
    // 顯示有效簽名的詳細信息
    foreach (DigitalSignature digitalSignature in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature found:");
        Console.WriteLine($"Signer: {digitalSignature.Subject}");
        Console.WriteLine($"Issuer: {digitalSignature.Issuer}");
        Console.WriteLine($"Valid From: {digitalSignature.ValidFrom}");
        Console.WriteLine($"Valid To: {digitalSignature.ValidTo}");
    }
}
else
{
    Console.WriteLine($"Document {filePath} failed verification process.");
    
    // 如果需要，顯示有關失敗簽名的信息
    foreach (DigitalSignature failedSignature in result.Failed)
    {
        Console.WriteLine($"Failed signature reason: {failedSignature.Comments}");
    }
}
```

此程式碼檢查驗證是否成功並提供有關已驗證簽名的詳細資訊。

## 完整範例

以下是演示數位簽章驗證的完整工作範例：

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
                    DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
                    {
                        Contact = "Mr.Smith",
                        Password = "1234567890"
                    };
                    
                    // 驗證文件簽名
                    VerificationResult result = signature.Verify(options);
                    
                    // 製程驗證結果
                    if (result.IsValid)
                    {
                        Console.WriteLine($"Document {filePath} contains valid digital signatures!");
                        
                        foreach (DigitalSignature item in result.Succeeded)
                        {
                            Console.WriteLine($"\nValid signature found.");
                            Console.WriteLine($"Subject: {item.Subject}");
                            Console.WriteLine($"Comments: {item.Comments}");
                            Console.WriteLine($"Sign Time: {item.SignTime}");
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

### 驗證多個數位簽名

```csharp
// 建立驗證選項列表
List<VerifyOptions> listOptions = new List<VerifyOptions>();

// 新增第一個憑證驗證選項
listOptions.Add(new DigitalVerifyOptions("Certificate1.pfx")
{
    Contact = "John Smith"
});

// 新增第二個證書驗證選項
listOptions.Add(new DigitalVerifyOptions("Certificate2.pfx")
{
    Contact = "Jane Doe"
});

// 使用多個選項進行驗證
VerificationResult result = signature.Verify(listOptions);
```

### 驗證特定頁面上的簽名

```csharp
// 僅驗證第一頁的數位簽名
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    AllPages = false,
    PageNumber = 1
};
```

### 使用時間戳記和證書頒發機構驗證

```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    ValidateTimeStampOnly = true,   // 僅驗證時間戳
    CertificateAuth = CertificateAuthType.Standard  // 驗證簽署者的證書
};
```

## 數位簽章驗證的最佳實踐

1. 適當的證書管理：安全地儲存證書文件並適當管理密碼。
2. 憑證驗證：實施憑證鏈驗證以確保憑證本身有效。
3. 錯誤處理：實作強大的錯誤處理，以優雅地管理驗證失敗。
4. 日誌記錄：記錄驗證嘗試和結果以供審計和合規目的。
5. 定期證書更新：確保證書在到期前更新。

## 常見問題故障排除

### 證書無效
- 驗證證書檔案路徑是否正確
- 確保證書密碼正確
- 檢查憑證是否已過期

### 未找到簽名
- 確認文件確實包含數位簽名
- 確認您正在檢查正確的頁面

### 驗證失敗
- 檢查文件在簽名後是否已修改
- 驗證簽署者的憑證是否在受信任的憑證鏈中

## 結論

GroupDocs.Signature for .NET 提供了一個強大且靈活的解決方案，用於驗證文件中的數位簽章。按照本逐步指南，您可以在 .NET 應用程式中實現強大的數位簽章驗證，確保文件的真實性和完整性。

數位簽章驗證是現代商業環境中安全文件工作流程的關鍵組成部分。透過 GroupDocs.Signature，您可以輕鬆自信地實現此功能，並利用全面的 API 處理各種驗證場景。

## 常見問題解答

### GroupDocs.Signature 能否驗證使用 Adobe Acrobat 簽署的 PDF 文件中的簽章？
是的，GroupDocs.Signature 可以驗證由 Adobe Acrobat 和其他相容 PDF 軟體建立的 PDF 文件中的標準數位簽章。

### GroupDocs.Signature 是否支援文件時間戳驗證？
是的，API 提供了驗證文件時間戳記的選項，作為數位簽章驗證過程的一部分。

### 我可以驗證多頁文件中特定頁面上的簽名嗎？
是的，您可以配置驗證選項來檢查特定頁面而不是整個文件上的簽名。

### GroupDocs.Signature 是否支援驗證單一文件中的多個簽章？
是的，GroupDocs.Signature 可以驗證單一文件中的多個數位簽名，並為每個簽名提供詳細的結果。

### 是否可以驗證使用來自不同憑證授權單位的憑證所建立的簽章？
是的，GroupDocs.Signature 支援驗證使用來自不同憑證授權單位的憑證建立的簽名，只要它們位於受信任的憑證鏈中。

### 相關資源
* [GroupDocs.Signature API 參考](https://reference.groupdocs.com/signature/net/)
* [GroupDocs.Signature 下載](https://releases.groupdocs.com/signature/net/)
* [GitHub 上的程式碼範例](https://github.com/groupdocs-signature/GroupDocs.Signature-for-.NET/tree/master/Examples)
* [文件](https://docs.groupdocs.com/signature/net/)
* [產品頁面](https://products.groupdocs.com/signature/net/)
* [部落格文章](https://blog.groupdocs.com/categories/groupdocs.signature-product-family/)
* [支援論壇](https://forum.groupdocs.com/c/signature/13)
* [臨時執照](https://purchase.groupdocs.com/temporary-license/)