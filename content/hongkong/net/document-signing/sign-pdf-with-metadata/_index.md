---
title: 使用元資料簽署 PDF
linktitle: 使用元資料簽署 PDF
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 使用元資料對 PDF 文件進行簽署。輕鬆增強文件的可追溯性和真實性。
weight: 11
url: /zh-hant/net/document-signing/sign-pdf-with-metadata/
---

# 使用元資料簽署 PDF

## 介紹
在本教程中，我們將學習如何使用 GroupDocs.Signature for .NET 使用元資料對 PDF 文件進行簽署。向 PDF 添加元數據可以提供有關文檔的附加信息，例如作者身份、創建日期、文檔 ID 等。
## 先決條件
在我們開始之前，請確保您具備以下條件：
1.  GroupDocs.Signature for .NET：您可以從下列位置下載：[這裡](https://releases.groupdocs.com/signature/net/).
2. PDF 文件：準備好範例 PDF 文件以供簽署。
3. C# 程式設計基礎：需要熟悉 C# 語法才能理解程式碼範例。
## 導入命名空間
首先，確保導入必要的命名空間來存取所需的類別和方法：
```csharp
using System;
using System.IO;
using GroupDocs.Signature;
using GroupDocs.Signature.Domain;
using GroupDocs.Signature.Options;
```
## 第 1 步：載入 PDF 文檔
載入您要簽署的 PDF 文件：
```csharp
string filePath = "sample.pdf";
```
## 步驟2：指定輸出檔案路徑
定義保存帶有元資料的簽章 PDF 的輸出檔路徑：
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPdfWithMetadata", "SignedWithMetadata.pdf");
```
## 步驟3：建立簽名實例
透過提供 PDF 文件的路徑來初始化 Signature 實例：
```csharp
using (Signature signature = new Signature(filePath))
{
    //簽名相關程式碼將放在這裡
}
```
## 第 4 步：定義元資料選項
建立 MetadataSignOptions 並新增元資料欄位及其各自的值：
```csharp
MetadataSignOptions options = new MetadataSignOptions();
options
    .Add(new PdfMetadataSignature("Author", "Mr.Sherlock Holmes")) //字串值
    .Add(new PdfMetadataSignature("CreatedOn", DateTime.Now))       //日期時間值
    .Add(new PdfMetadataSignature("DocumentId", 123456))            //整數值
    .Add(new PdfMetadataSignature("SignatureId", 123.456D))         //雙倍價值
    .Add(new PdfMetadataSignature("Amount", 123.456M))              //十進制值
    .Add(new PdfMetadataSignature("Total", 123.456F));              //浮動值
```
## 第 5 步：簽署文件
使用指定的元資料選項對 PDF 文件進行簽署並儲存簽署的文件：
```csharp
SignResult result = signature.Sign(outputFilePath, options);
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```

## 結論
在本教學中，我們介紹如何使用 GroupDocs.Signature for .NET 使用元資料對 PDF 文件進行簽署。透過遵循逐步指南，您可以輕鬆地將元資料資訊（例如作者身份、建立日期等）添加到 PDF 文件中，從而增強其實用性和可追溯性。
## 常見問題解答
### 我可以將自訂元資料欄位新增至我的 PDF 文件嗎？
是的，您可以透過使用 GroupDocs.Signature for .NET 指定欄位名稱及其對應值來新增自訂元資料欄位。
### GroupDocs.Signature for .NET 是否與所有版本的 .NET Framework 相容？
GroupDocs.Signature for .NET 與各種版本的 .NET Framework 相容，確保靈活性和易於整合。
### GroupDocs.Signature 是否支援簽署 PDF 以外的其他文件格式？
是的，GroupDocs.Signature 支援多種文件格式，包括 Word、Excel、PowerPoint 等。
### 我可以使用 GroupDocs.Signature for .NET 批次簽署多個文件嗎？
是的，您可以透過迭代文件清單並以程式設計方式應用簽名過程來批次簽署多個文件。
### GroupDocs.Signature 用戶可以獲得技術支援嗎？
是的，GroupDocs 透過其論壇提供專門的技術支援。您可以造訪支援論壇[這裡](https://forum.groupdocs.com/c/signature/13).