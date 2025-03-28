---
title: 驗證數位簽名
linktitle: 驗證數位簽名
second_title: GroupDocs.Signature .NET API
description: 使用 GroupDocs.Signature 輕鬆驗證 .NET 中的數位簽章。輕鬆確保文件的真實性和完整性。
weight: 11
url: /zh-hant/net/verify-operations/verify-digital/
---

# 驗證數位簽名

## 介紹
在數位文件領域，確保真實性和完整性至關重要。數位簽章相當於手寫簽名的數位形式，提供了一種驗證電子文件的來源和完整性的安全方法。 GroupDocs.Signature for .NET 提供了一個強大的工具包，可在 .NET 應用程式中處理數位簽名，從而輕鬆促進數位簽名的驗證。
## 先決條件
在深入使用 GroupDocs.Signature for .NET 進行驗證程序之前，請確保符合以下先決條件：
### 1. 安裝 .NET 的 GroupDocs.Signature
首先，下載並安裝適用於 .NET 的 GroupDocs.Signature。你可以找到下載鏈接[這裡](https://releases.groupdocs.com/signature/net/).
### 2. 取得數位簽章文件
您需要一個數位簽章文件（例如，YourSignature.pfx）用於驗證目的。確保您有權存取該文件及其關聯的密碼。

## 導入命名空間
在您的 .NET 專案中，匯入必要的命名空間以利用 GroupDocs.Signature 功能。

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 1.指定文檔路徑
```csharp
string filePath = "sample_multiple_signatures.docx";
```
指定要驗證的文檔的路徑。
## 2. 初始化簽名對象
```csharp
using (Signature signature = new Signature(filePath))
```
透過將文件路徑作為參數傳遞來建立新的 Signature 物件。
## 3. 設定驗證選項
```csharp
DigitalVerifyOptions options = new DigitalVerifyOptions("YourSignature.pfx")
{
    Contact = "Mr.Smith",
    Password = "1234567890"
};
```
建立 DigitalVerifyOptions 對象，指定數位簽章檔案（例如 YourSignature.pfx）的路徑，以及任何其他選項，例如聯絡資訊和密碼。
## 4. 驗證簽名
```csharp
VerificationResult result = signature.Verify(options);
```
呼叫 Signature 物件上的 verify 方法，傳遞驗證選項。
## 5. 處理驗證結果
```csharp
if (result.IsValid)
{
    //找到有效簽名
    foreach (DigitalSignature item in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature is found.");
    }
}
else
{
    //驗證失敗
    Helper.WriteError($"\nDocument {filePath} failed verification process.");
}
```
檢查驗證結果是否有效。如果有效，則遍歷成功簽署的清單。否則，處理驗證失敗。

## 結論
總之，GroupDocs.Signature for .NET 簡化了在 .NET 應用程式中驗證數位簽章的過程。透過遵循上述逐步指南並利用 GroupDocs.Signature 的強大功能，您可以放心地確保數位文件的真實性和完整性。
## 常見問題解答
### GroupDocs.Signature 可以驗證單一文件中的多個簽章嗎？
是的，GroupDocs.Signature 支援在單一文件中驗證多個簽名，提供全面的驗證功能。
### GroupDocs.Signature 是否與不同類型的數位簽章檔案相容？
GroupDocs.Signature 支援各種數位簽章檔案格式，包括 PFX、P12 等，確保驗證流程的靈活性。
### 我可以在驗證過程中自訂驗證選項，例如聯絡資訊嗎？
是的，GroupDocs.Signature 允許自訂驗證選項，使用戶能夠根據需要指定聯絡資訊、密碼和其他參數。
### GroupDocs.Signature 是否提供故障排除和協助支援？
是的，GroupDocs.Signature 透過其論壇提供專門支持，用戶可以在其中尋求幫助、分享見解並有效地解決問題。
### GroupDocs.Signature 是否有試用版？
是的，有興趣的使用者可以存取 GroupDocs.Signature 的免費試用版，在做出購買決定之前探索其特性和功能。