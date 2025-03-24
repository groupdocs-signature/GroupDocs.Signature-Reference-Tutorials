---
title: 驗證二維碼
linktitle: 驗證二維碼
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 驗證文件中的 QR 碼。帶有逐步指南的綜合教程。
weight: 12
url: /zh-hant/net/verify-operations/verify-qr-code/
---

# 驗證二維碼

## 介紹
在文件管理和身份驗證領域，確保簽名的完整性和有效性至關重要。 GroupDocs.Signature for .NET 提供了驗證文件中嵌入的 QR 程式碼的全面解決方案。在本教程中，我們將深入研究使用 GroupDocs.Signature for .NET 驗證 QR 碼的逐步流程。
## 先決條件
在深入驗證過程之前，請確保滿足以下先決條件：
1. 安裝 GroupDocs.Signature for .NET：從下列位置下載並安裝 GroupDocs.Signature for .NET[下載連結](https://releases.groupdocs.com/signature/net/).
2. 存取包含 QR 碼的文件：準備包含 QR 碼的範例文件以進行驗證。 

## 導入命名空間
首先，您需要匯入必要的命名空間以利用 GroupDocs.Signature for .NET 提供的功能。按著這些次序：

```csharp
using System;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```


現在，讓我們分解一下使用 GroupDocs.Signature for .NET 驗證文件中嵌入的二維碼的過程：
## 第1步：指定文檔路徑
```csharp
string filePath = "sample_multiple_signatures.docx";
```
確保更換`"sample_multiple_signatures.docx"`以及您的文件的路徑。
## 步驟2：初始化簽名對象
```csharp
using (Signature signature = new Signature(filePath))
{
    //驗證碼在這裡
}
```
初始化一個`Signature`物件透過提供文檔的路徑。
## 步驟 3：指定驗證選項
```csharp
QrCodeVerifyOptions options = new QrCodeVerifyOptions()
{
    AllPages = true, //該值是預設設定的
    Text = "John",
    MatchType = TextMatchType.Contains
};
```
定義驗證選項，例如`AllPages`驗證所有頁面，`Text`指定 QR 碼中要匹配的文本，以及`MatchType`定義匹配標準。
## 第 4 步：驗證文件簽名
```csharp
VerificationResult result = signature.Verify(options);
```
呼叫`Verify`的方法`Signature`對象，傳遞驗證選項。
## 步驟5：處理驗證結果
```csharp
if (result.IsValid)
{
    //找到有效簽名
}
else
{
    //發現無效簽名
}
```
根據驗證結果，對成功或失敗的場景進行相應的處理。

## 結論
在本教程中，我們探索了使用 GroupDocs.Signature for .NET 驗證文件中的 QR 碼的流程。透過執行這些步驟，您可以將 QR 碼驗證功能無縫整合到您的 .NET 應用程式中，從而確保文件的完整性和真實性。
## 常見問題解答
### GroupDocs.Signature for .NET 可以在不同文件格式之間驗證 QR 碼嗎？
是的，GroupDocs.Signature for .NET 支援多種文件格式，包括 DOCX、PDF 等用於 QR 碼驗證的格式。
### GroupDocs.Signature for .NET 是否有免費試用版？
是的，您可以從以下網站獲得免費試用[發布頁面](https://releases.groupdocs.com/).
### .NET 使用者的 GroupDocs.Signature 可以使用哪些支援選項？
用戶可以透過以下方式獲得支持[論壇](https://forum.groupdocs.com/c/signature/13)對於 GroupDocs.Signature。
### 我可以購買適用於 .NET 的 GroupDocs.Signature 臨時授權嗎？
是的，臨時許可證可以從[GroupDocs 購買頁面](https://purchase.groupdocs.com/temporary-license/).
### 是否有適用於 .NET 的 GroupDocs.Signature 的大量文件？
完全可以，你可以參考提供的詳細文檔[這裡](https://tutorials.groupdocs.com/signature/net/)使用 GroupDocs.Signature for .NET 功能的綜合指南。