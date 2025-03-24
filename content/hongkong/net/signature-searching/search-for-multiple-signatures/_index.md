---
title: 搜尋多重簽名
linktitle: 搜尋多重簽名
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature 在 .NET 文件中搜尋多個簽名，以實現高效的文件安全性和完整性。
weight: 14
url: /zh-hant/net/signature-searching/search-for-multiple-signatures/
---
## 介紹
GroupDocs.Signature for .NET 是一個功能強大的程式庫，可讓開發人員使用 .NET 應用程式新增、搜尋和刪除流行文件格式中的各種類型的簽章。在本教程中，我們將重點放在使用 GroupDocs.Signature for .NET 在文件中搜尋多個簽章。
## 先決條件
在我們開始之前，請確保您具備以下先決條件：
- Visual Studio 安裝在您的系統上。
- 對 C# 程式語言有基本了解。
- 專案中安裝的 .NET 程式庫的 GroupDocs.Signature。您可以從以下位置下載：[這裡](https://releases.groupdocs.com/signature/net/).

## 導入命名空間
首先，您需要匯入必要的命名空間來存取 GroupDocs.Signature for .NET 提供的類別和方法。
```csharp
using System;
using System.Collections.Generic;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：載入文檔
將文件載入到要搜尋多個簽章的位置。確保您提供正確的檔案路徑。
```csharp
string filePath = "sample_multiple_signatures.docx";
using (Signature signature = new Signature(filePath))
{
    //你的程式碼放在這裡
}
```
## 第 2 步：定義搜尋選項
定義各種類型簽署的搜尋選項，例如文字、數字、條碼、二維碼和元資料。您可以指定搜尋條件，例如要符合的文字、符合類型以及跨所有頁面進行搜尋。
```csharp
//定義搜尋選項
TextSearchOptions textOptions = new TextSearchOptions()
{
    AllPages = true
};
DigitalSearchOptions digitalOptions = new DigitalSearchOptions()
{
    AllPages = true
};
BarcodeSearchOptions barcodeOptions = new BarcodeSearchOptions()
{
    AllPages = true,
    Text = "123456",
    MatchType = TextMatchType.Exact
};
QrCodeSearchOptions qrCodeOptions = new QrCodeSearchOptions()
{
    AllPages = true,
    Text = "John",
    MatchType = TextMatchType.Contains
};
MetadataSearchOptions metadataOptions = new MetadataSearchOptions();
```
## 第 3 步：將搜尋選項新增至清單中
將定義的搜尋選項新增至清單。
```csharp
//將選項新增至列表
List<SearchOptions> listOptions = new List<SearchOptions>();
listOptions.Add(textOptions);
listOptions.Add(barcodeOptions);
listOptions.Add(qrCodeOptions);
listOptions.Add(metadataOptions);
listOptions.Add(digitalOptions);
```
## 第 4 步：搜尋簽名
使用定義的搜尋選項在文件中搜尋簽名。
```csharp
//搜尋文件中的簽名
SearchResult result = signature.Search(listOptions);
if (result.Signatures.Count > 0)
{
    Console.WriteLine($"\nSource document ['{filePath}'] contains following signatures.");
    foreach (var resSignature in result.Signatures)
    {
        Console.WriteLine($"Signature found at page {resSignature.PageNumber} with type {resSignature.SignatureType} and Id#: {resSignature.SignatureId}");
    }
}
else
{
    Helper.WriteError("No one signature was found.");
}
```

## 結論
在本教學中，我們學習如何使用 GroupDocs.Signature for .NET 在文件中搜尋多個簽章。透過遵循提供的步驟，您可以有效地找到文件中的各種類型的簽名，從而增強文件的安全性和完整性。
## 常見問題解答
### 我可以搜尋不同文件格式的簽名嗎？
是的，GroupDocs.Signature for .NET 支援多種文件格式，包括 Word、PDF、Excel 等。
### 是否可以自訂簽名的搜尋條件？
當然，您可以根據您的要求自訂搜尋條件，例如指定精確的文字匹配或跨所有頁面搜尋。
### GroupDocs.Signature for .NET 是否提供數位簽章支援？
是的，您可以搜尋數位簽名以及文字、條碼和二維碼簽名等其他類型。
### 我可以輕鬆地將簽名搜尋功能整合到我的 .NET 應用程式中嗎？
是的，GroupDocs.Signature for .NET 提供了一個簡單的 API，可以簡化整合流程。
### 我可以在哪裡找到額外的支援或協助？
您可以造訪 GroupDocs.Signature 論壇[這裡](https://forum.groupdocs.com/c/signature/13)如有任何疑問或幫助。