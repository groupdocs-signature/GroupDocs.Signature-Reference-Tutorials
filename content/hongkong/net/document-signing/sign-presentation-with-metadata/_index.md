---
title: 使用元資料簽署簡報
linktitle: 使用元資料簽署簡報
second_title: GroupDocs.Signature .NET API
description: 了解如何使用 GroupDocs.Signature for .NET 使用元資料對簡報文件進行簽署。增強文件完整性並添加有價值的資訊。
weight: 12
url: /zh-hant/net/document-signing/sign-presentation-with-metadata/
---
## 介紹
在本教程中，我們將學習如何使用 GroupDocs.Signature for .NET 程式庫對簡報檔案 (PPTX) 進行元資料簽署。使用元資料對簡報進行簽名會為文件添加有價值的信息，例如作者姓名、創建日期、文件 ID、簽名 ID 和各種數值。
## 先決條件
在我們開始之前，請確保您具備以下條件：
1.  GroupDocs.Signature for .NET Library：從以下位置下載並安裝該程式庫[這裡](https://releases.groupdocs.com/signature/net/).
2. 開發環境：確保您已設定 .NET 開發環境。
3. 示範文件：準備好範例示範文件（PPTX 格式）以供簽署。
4. 對 C# 的基本了解：熟悉 C# 程式語言將會很有幫助。

## 導入命名空間
在深入研究程式碼之前，讓我們先導入必要的名稱空間：
```csharp
using System;
using System.IO;
    using GroupDocs.Signature;
    using GroupDocs.Signature.Domain;
    using GroupDocs.Signature.Options;
```
## 第 1 步：載入示範文件
```csharp
string filePath = "sample.pptx";
```
代替`"sample.pptx"`以及簡報文件的路徑。
## 步驟2：指定輸出檔案路徑
```csharp
string outputFilePath = Path.Combine("Your Document Directory", "SignPresentationWithMetadata", "SignedWithMetadata.pptx");
```
指定要儲存已簽署的簡報檔案及其檔案名稱的目錄。
## 第三步：初始化簽名對象
```csharp
using (Signature signature = new Signature(filePath))
```
透過提供演示檔案的路徑來初始化 Signature 物件。
## 第 4 步：定義元資料簽章選項
```csharp
MetadataSignOptions options = new MetadataSignOptions();
```
建立 MetadataSignOptions 的實例來定義元資料簽章選項。
## 第 5 步：建立元資料簽名
```csharp
PresentationMetadataSignature[] signatures = new PresentationMetadataSignature[]
{
    new PresentationMetadataSignature("Author", "Mr.Scherlock Holmes"),
    new PresentationMetadataSignature("CreatedOn", DateTime.Now),
    new PresentationMetadataSignature("DocumentId", 123456),
    new PresentationMetadataSignature("SignatureId", 123.456D),
    new PresentationMetadataSignature("Amount", 123.456M),
    new PresentationMetadataSignature("Total", 123.456F)
};
```
建立一個PresentationMetadataSignature 物件數組，每個物件代表一個元資料簽章。您可以新增各種類型的元數據，包括字串、日期時間、整數、雙精確度、小數和浮點。
## 第 6 步：將簽名新增至選項
```csharp
options.Signatures.AddRange(signatures);
```
將建立的元資料簽章新增至 MetadataSignOptions 物件。
## 第 7 步：簽署文件
```csharp
SignResult result = signature.Sign(outputFilePath, options);
```
使用指定的選項使用元資料對簡報檔案進行簽名，並將簽署的檔案儲存到輸出路徑。
## 第8步：顯示結果
```csharp
Console.WriteLine($"\nSource document signed successfully with {result.Succeeded.Count} signature(s).\nFile saved at {outputFilePath}.");
```
顯示成功訊息以及套用的簽章數量以及簽章檔案的儲存路徑。

## 結論
在本教學中，我們學習如何使用 GroupDocs.Signature for .NET 函式庫使用元資料對簡報檔案進行簽署。新增元資料簽章可以增強文件的完整性並提供有關其內容的有價值的資訊。

## 常見問題解答
### 我可以使用 GroupDocs.Signature for .NET 對 PPTX 以外的其他文件格式使用元資料進行簽署嗎？
是的，GroupDocs.Signature 支援各種文件格式，包括 Word、Excel、PDF 等，以便使用元資料進行簽署。
### GroupDocs.Signature for .NET 是否與 .NET Core 相容？
是的，該程式庫與 .NET Framework 和 .NET Core 相容。
### 我可以自訂元資料簽章的外觀嗎？
是的，您可以根據您的要求自訂元資料簽署的外觀、位置和其他屬性。
### GroupDocs.Signature for .NET 是否為簽署文件提供加密？
是的，GroupDocs.Signature 提供加密選項來保護簽署文件免遭未經授權的存取。
### 購買前是否有試用版可供測試？
是的，您可以從以下位置免費試用 GroupDocs.Signature for .NET：[這裡](https://releases.groupdocs.com/).