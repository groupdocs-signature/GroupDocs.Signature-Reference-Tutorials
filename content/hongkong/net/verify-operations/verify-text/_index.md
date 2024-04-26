---
title: 驗證文字
linktitle: 驗證文字
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 驗證文件中的文字。請按照我們的逐步教學進行無縫整合。
type: docs
weight: 13
url: /zh-hant/net/verify-operations/verify-text/
---
## 介紹
在本教學中，我們將引導您完成使用 GroupDocs.Signature for .NET 驗證文件中文字的流程。這個強大的程式庫可讓您將文字驗證功能無縫整合到您的 .NET 應用程式中，從而確保文件的完整性和真實性。
## 先決條件
在我們開始之前，請確保您符合以下先決條件：
1.  GroupDocs.Signature for .NET：確保您已安裝並設定 GroupDocs.Signature for .NET。您可以從以下位置下載該程式庫[這裡](https://releases.groupdocs.com/signature/net/).
2. 文件檔案：準備您要驗證的文件檔案（例如sample_multiple_signatures.docx）。

## 導入命名空間
首先，您需要將必要的命名空間匯入到您的專案中：
```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第1步：設定文檔文件路徑
定義要驗證的文件的文件路徑。代替`"sample_multiple_signatures.docx"`以及文檔文件的路徑。
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## 步驟2：初始化簽名對象
建立一個實例`Signature`類別並將檔案路徑傳遞給其建構函數。
```csharp
using (Signature signature = new Signature(filePath))
{
    //驗證碼將會寫在這裡
}
```
## 步驟 3：指定文字驗證選項
定義文字驗證選項，包括待驗證的文字、符合類型和其他參數。
```csharp
TextVerifyOptions options = new TextVerifyOptions()
{
    AllPages = true, //驗證所有頁面上的文本
    SignatureImplementation = TextSignatureImplementation.Native,
    Text = "signature", //待驗證文本
    MatchType = TextMatchType.Contains //指定匹配類型
};
```
## 第 4 步：驗證文件簽名
呼叫`Verify`方法上的`Signature`反對並通過驗證選項。
```csharp
VerificationResult result = signature.Verify(options);
```
## 第五步：處理驗證結果
檢查驗證結果的有效性並進行相應處理。
```csharp
if(result.IsValid)
{
    Console.WriteLine($"\nDocument {filePath} was verified successfully!");
    foreach (TextSignature item in result.Succeeded)
    {
        Console.WriteLine($"\nValid signature is found with text: {item.Text}");
    }
}
else
{
    Helper.WriteError($"\nDocument {filePath} failed verification process.");
}
```

## 結論
總之，GroupDocs.Signature for .NET 提供了一種無縫方式來驗證文件中的文本，確保文件的完整性和真實性。透過遵循本教學中概述的步驟，您可以輕鬆地將文字驗證功能整合到您的 .NET 應用程式中。
## 常見問題解答
### GroupDocs.Signature for .NET 是否與所有文件格式相容？
是的，GroupDocs.Signature for .NET 支援多種文件格式，包括 DOCX、PDF、XLSX 等。
### 我可以自訂文字驗證標準嗎？
當然，您可以自訂各種參數，例如符合類型、頁面範圍等，以滿足您的驗證要求。
### GroupDocs.Signature for .NET 是否提供數位簽章的支援？
是的，GroupDocs.Signature for .NET 支援文字和數位簽名，提供全面的文件驗證功能。
### GroupDocs.Signature for .NET 是否有免費試用版？
是的，您可以免費試用[這裡](https://releases.groupdocs.com/).
### 我可以在哪裡獲得 GroupDocs.Signature for .NET 的協助或支援？
您可以訪問[GroupDocs.Signature 論壇](https://forum.groupdocs.com/c/signature/13)尋求社會各界的幫助與支持。