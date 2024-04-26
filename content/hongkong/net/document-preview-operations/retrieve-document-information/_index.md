---
title: 檢索文件資訊
linktitle: 檢索文件資訊
second_title: GroupDocs.Signature .NET API
description: 使用 GroupDocs.Signature 增強 .NET 中的文件管理。逐步檢索文件資訊。支援各種格式。
type: docs
weight: 11
url: /zh-hant/net/document-preview-operations/retrieve-document-information/
---
## 介紹
在數位文件領域，確保真實性和完整性至關重要。 GroupDocs.Signature for .NET 提供了一個強大的解決方案，用於在 .NET 環境中管理文件簽章。在本教程中，我們將深入研究使用 GroupDocs.Signature for .NET 檢索文件資訊的過程，分解每個步驟以便全面理解。
## 先決條件
在深入學習本教程之前，請確保您具備以下先決條件：
1. 安裝：透過下載安裝 GroupDocs.Signature for .NET[這裡](https://releases.groupdocs.com/signature/net/).
2. .NET 環境：具備 .NET 架構的應用知識。
3. 文件：準備樣本文件（例如「sample_multiple_signatures.docx」）以用於測試目的。

## 導入命名空間
在繼續文件簽章檢索過程之前，導入必要的命名空間：
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
```

## 步驟1：設定文檔文件路徑：
定義要從中檢索資訊的文件的文件路徑。
```csharp
string filePath = "sample_multiple_signatures.docx";
```
## 第2步：實例化簽章物件：
建立一個實例`Signature`類別透過傳遞文檔文件路徑。
```csharp
using (Signature signature = new Signature(filePath))
{

}
```
## 步驟 3：檢索文件資訊：
利用`GetDocumentInfo()`取得有關文件的全面資訊的方法。
```csharp
IDocumentInfo documentInfo = signature.GetDocumentInfo();
```
## 步驟 4：顯示文檔屬性：
輸出文件的各種屬性，例如格式、副檔名、大小、頁數等。
```csharp
Console.WriteLine($"Document properties {Path.GetFileName(filePath)}:");
Console.WriteLine($" - format : {documentInfo.FileType.FileFormat}");
Console.WriteLine($" - extension : {documentInfo.FileType.Extension}");
Console.WriteLine($" - size : {documentInfo.Size}");
Console.WriteLine($" - page count : {documentInfo.PageCount}");
Console.WriteLine($" - Form Fields count : {documentInfo.FormFields.Count}");
Console.WriteLine($" - Text signatures count : {documentInfo.TextSignatures.Count}");
Console.WriteLine($" - Image signatures count : {documentInfo.ImageSignatures.Count}");
Console.WriteLine($" - Digital signatures count : {documentInfo.DigitalSignatures.Count}");
Console.WriteLine($" - Barcode signatures count : {documentInfo.BarcodeSignatures.Count}");
Console.WriteLine($" - QrCode signatures count : {documentInfo.QrCodeSignatures.Count}");
Console.WriteLine($" - FormField signatures count : {documentInfo.FormFieldSignatures.Count}");
foreach (PageInfo pageInfo in documentInfo.Pages)
{
   Console.WriteLine($" - page-{pageInfo.PageNumber} Width {pageInfo.Width}, Height {pageInfo.Height}");
}
```


## 結論
GroupDocs.Signature for .NET 提供了一套功能強大的工具，可在 .NET 框架內無縫管理文件簽章。透過遵循本指南中概述的步驟，您可以有效地檢索有關文件的全面信息，從而增強文件管理功能。

## 常見問題解答
### GroupDocs.Signature for .NET 可以處理多種文件格式嗎？
是的，GroupDocs.Signature 支援多種文件格式，包括但不限於 DOCX、PDF、PNG 和 JPEG。
### 是否有適用於 .NET 的 GroupDocs.Signature 試用版？
是的，您可以存取試用版[這裡](https://releases.groupdocs.com/).
### GroupDocs.Signature for .NET 是否提供數位簽章的支援？
當然，GroupDocs.Signature 為數位簽章提供強大的支持，確保文件的真實性和完整性。
### 在哪裡可以找到針對 .NET 的 GroupDocs.Signature 的其他文件和支援？
您可以參考綜合文檔[這裡](https://reference.groupdocs.com/signature/net/)，如需支持，請造訪 GroupDocs 論壇[這裡](https://forum.groupdocs.com/c/signature/13).
### 能否為 .NET 取得 GroupDocs.Signature 的臨時許可證？
是的，可以購買臨時許可證[這裡](https://purchase.groupdocs.com/temporary-license/).